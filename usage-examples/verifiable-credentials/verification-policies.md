# Verification Policies

For verification of verifiable credentials, the SSIKit provides several predefined, static verification policies. Additionally, it provides a way to create custom policies dynamically, using a policy execution engine, such as **Open Policy Agent**.

To list the available verification policies and their descriptions, run:

```
ssikit vc policies list
```

The output will show the available policies, where static, predefined policies are indicated by the leading `-`, whereas dynamically created policies are indicated by `*`:

```
ssikit vc policies list
walt.id SSI Kit 1.11.0-SNAPSHOT (running on Java 16.0.2+7-suse-lp153.30.15-x8664)

- SignaturePolicy       Verify by signature,    Argument: None
- JsonSchemaPolicy       Verify by JSON schema,  Argument: None
- TrustedSchemaRegistryPolicy    Verify by EBSI Trusted Schema Registry,         Argument: None
- TrustedIssuerDidPolicy         Verify by trusted issuer did,   Argument: None
- TrustedIssuerRegistryPolicy    Verify by trusted EBSI Trusted Issuer Registry record,  Argument: None
- TrustedSubjectDidPolicy        Verify by trusted subject did,  Argument: None
- IssuedDateBeforePolicy         Verify by issuance date,        Argument: None
- ValidFromBeforePolicy  Verify by valid from,   Argument: None
- ExpirationDateAfterPolicy      Verify by expiration date,      Argument: None
- GaiaxTrustedPolicy     Verify Gaiax trusted fields,    Argument: None
- GaiaxSDPolicy  Verify Gaiax SD fields,         Argument: None
- ChallengePolicy        Verify challenge,       Argument: ChallengePolicyArg
- VpTokenClaimPolicy     Verify verifiable presentation by OIDC/SIOPv2 VP token claim,   Argument: VpTokenClaim
- CredentialStatusPolicy         Verify by credential status,    Argument: None
- DynamicPolicy  Verify credential by rego policy,       Argument: DynamicPolicyArg
- VerifiableMandatePolicy        Predefined policy for verifiable mandates,      Argument: JsonObject
* GaiaXPolicy    - no description -,     Argument: JsonObject
* ItsMePolicy    Check that credential is mine,  Argument: JsonObject

(*) ... mutable dynamic policy
```

## Parameterized Policies

Some policies may require a parameter or argument for execution. The parameter is indicated in the policy list output, together with the expected data type.

The **CLI** allows for specifying a parameter with the verification policy, by this special syntax:

```
ssikit vc verify -p ChallengePolicy='{ "challenges": [ "362df5ec-37ab-46a7-aa71-767d8f277b69" ] }' src/test/resources/rego/VerifiableId.json
```

In above example, we verify the challenge of the credential to be one of the challenges given in the ChallengePolicyArg argument.

An example using the Auditor REST API, with the parameterless **SignaturePolicy** and the parameterized **ChallengePolicy** would look like this:

`POST /v1/verify`

```
{
  "policies": [
    {
      "policy": "SignaturePolicy"
    },
    {
      "policy": "ChallengePolicy",
      "argument": {
        "challenges": [ "362df5ec-37ab-46a7-aa71-767d8f277b69" ]
      }
    }
  ],
  "credentials": [
    {
      "@context" : [ "https://www.w3.org/2018/credentials/v1" ],
      [...]
    }
  ]
}
```

_Response_

```
{
  "valid": true,
  "results": [
    {
      "valid": true,
      "policyResults": {
        "SignaturePolicy": true,
        "ChallengePolicy": true
      }
    }
  ]
}
```

## Dynamic Policies

The SSIKit allows for specifying custom policies written in one of the supported policy engine lingos.

A dynamic policy can be executed on the fly, if all required parameters are given, or saved with a name, by which it can be referenced in the verify command or REST API lateron.

In this example I'm going to use a very simple policy written in the Rego language, for the **Open Policy Agent** engine.

### Dynamic policy argument

The dynamic policy requires an argument of the DynamicPolicyArg type, which is defined like follows:

```
data class DynamicPolicyArg (
    val name: String = "DynamicPolicy",
    val description: String? = null,
    val input: Map<String, Any?>,
    val policy: String,
    val dataPath: String = "\$.credentialSubject",
    val policyQuery: String = "data.system.main",
    val policyEngine: PolicyEngineType = PolicyEngineType.OPA,
    val applyToVC: Boolean = true,
    val applyToVP: Boolean = false
)
```

**Properties:**

- `name`: policy name, defaults to "DynamicPolicy"
- `description`: Optional description of the policy
- `input`: A generic map (JSON object), holding the input data required by the policy (or an empty map if no input is required)
- `policy`: the policy definition (e.g. rego file), which can be a file path, URL, JSON Path (if policy is defined in a credential property) or the code/script directly.
- `dataPath`: The path to the credential data, which should be verified, by default it's the credential subject: `$.credentialSubject`. To use the entire credential as verification data, specify the path `$`.
- `policyQuery`: The query string in the policy engine lingo, defaults to "data.system.main"
- `policyEngine`: The engine to use for execution of the policy. By default `OPA` (Open Policy Agent) is used.
- `applyToVC`: Apply this policy to verifiable credentials (Default: true)
- `applyToVP`: Apply this policy to verifiable presentations (Default: false)

### Sample policy

This simple rego policy takes a credential subject as input and verifies the subject DID against a given parameter.

```
package system

import future.keywords.in
import future.keywords.every

default main = false

# all inputs must contain user and actions

main {
    input.user == data.id
}
```

This policy file is located in the SSIKit test resources:

`src/test/resources/rego/subject-policy.rego`

### On the fly execution

To execute the sample policy on the fly, without saving it as custom policy, simply run this command:

```
ssikit vc verify -p DynamicPolicy='{ "policy": "src/test/resources/rego/subject-policy.rego",  "input": { "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" } }' src/test/resources/rego/VerifiableId.json
```

This command uses the DynamicPolicy to execute the rego policy specified in the policy property, with the input specified in the input property.

### Saved dynamic policy

To save the policy by name, so that it can be used more easily lateron, use the command

```
ssikit vc policies create
```

Let's save the above sample policy as `SubjectPolicy`, like so:

```
ssikit vc policies create -n "SubjectPolicy" -D "Verifies credential subject" -p src/test/resources/rego/subject-policy.rego
```

Now we can simplify the above verify command like this:

```
ssikit vc verify -p SubjectPolicy='{ "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" }' src/test/resources/rego/VerifiableId.json
```

This policy requires the user did as input.

#### Predefined policy input argument
It's possible to include the policy input argument in the saved policy, to pre-define the input or use it as a default, which can be overridden on execution.

Let's create a saved policy named `ItsMePolicy`, which checks all credentials against my predefined subject DID:

```
ssikit vc policies create -n "ItsMePolicy" -D "Verifies credential subject against my DID" -p src/test/resources/rego/subject-policy.rego -i '{ "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" }'
```

Now we can further simplify the above verify command like this:

```
ssikit vc verify -p ItsMePolicy src/test/resources/rego/VerifiableId.json
```

Note, that we can still override the predefined input data like shown here:

```
ssikit vc verify -p ItsMePolicy='{ "user": "did:key:xxxxxxxxx" }' src/test/resources/rego/VerifiableId.json
```
