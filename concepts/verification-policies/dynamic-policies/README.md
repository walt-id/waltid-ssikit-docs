# Dynamic/Custom Policies

SSI Kit supports custom policies, written in any of the supported policy engine languages. A dynamic policy can either be executed on the fly (if all required parameters are provided) or saved under a specific name for later reference in the verify command or REST API.

This section uses a simple policy written in the Rego language for the Open Policy Agent engine as an example.

{% hint style="danger" %}
_Note: To use dynamic policies with Open Policy Agent, setup of the OPA Engine is required. Refer to the_ [_OPA Engine configuration_](../../../usage-examples/open-policy-agent/configure-opa-engine.md) _for more details._
{% endhint %}

### Dynamic Policy Argument

A dynamic policy requires an argument of the `DynamicPolicyArg` type, defined as follows:

```kotlin
data class DynamicPolicyArg (
    val name: String = "DynamicPolicy",
    val description: String? = null,
    val input: Map<String, Any?>,
    val policy: String,
    val dataPath: String = "\$",
    val policyQuery: String = "data.system.main",
    val policyEngine: PolicyEngineType = PolicyEngineType.OPA,
    val applyToVC: Boolean = true,
    val applyToVP: Boolean = false
)
```

The properties are as follows:

* **`name`**: The policy name. Defaults to "DynamicPolicy".
* **`description`**: An optional description of the policy.
* **`input`**: A generic map (JSON object) holding the input data required by the policy. If no input is required, this can be an empty map.
* **`policy`**: The policy definition. Can be a file path, URL, JSON Path (if policy is defined in a credential property), or the policy script directly.
* **`dataPath`**: The path to the credential data to be verified. Defaults to the entire credential object ($). If you want to use only the credential subject as verification data, specify the JSON path like this: `$.credentialSubject`.
* **`policyQuery`**: The query string in the policy engine language. Defaults to "data.system.main".
* **`policyEngine`**: The engine used for policy execution. Defaults to OPA (Open Policy Agent).
* **`applyToVC`**: Determines whether this policy should apply to verifiable credentials. Defaults to true.
* **`applyToVP`**: Determines whether this policy should apply to verifiable presentations. Defaults to false.

## Policy Execution and Input Data

The policy is executed by the specified policy engine, with the Open Policy Agent currently being the only supported engine. OPA receives an input object containing the dynamic policy's input parameter and the credential data configured in the policy argument.

The input object for the policy engine is structured as follows:

```kotlin
data class PolicyEngineInput(
    val credentialData: Map<String, Any?>,
    val parameter: Map<String, Any?>?
)
```

This structure allows the REGO policy definition to access the `input` properties as follows:

* **`input.parameter`**: The input object defined in the `DynamicPolicyArg`'s input property.
* **`input.credentialData`**: The credential data selected by the JSON path provided in the `DynamicPolicyArg`'s `dataPath` property.

### Creating and Using Dynamic Policies

Here, we guide you through the process of creating and using dynamic policies, demonstrating both on-the-fly execution and how to save policies for future use.

We will also show you how to update or remove dynamic policies and provide some additional tips and considerations.

### Sample policy

This simple rego policy takes a credential subject as input and verifies the subject DID against a given parameter.

```
package system

default main = false

main {
    input.parameter.user == input.credentialData.credentialSubject.id
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

#### Update or remove dynamic policies

To update an existing policy use the `--force` flag of the create command like so:

```
ssikit vc policies create -n "ItsMePolicy" -D "Verifies credential subject against my DID" -p src/test/resources/rego/subject-policy.rego -i '{ "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" }' --force
```

To remove a previously created policy, use the remove command:

```
ssikit vc policies remove -n ItsMePolicy
```

**Note**: You can update and remove only dynamic policies that have been manually created. You cannot override existing predefined, static policies.

The list command indicates mutable policies, by a leading `*`, and provides the `-m, --mutable` flags to filter by mutable policies only:

```
> ssikit vc policies list -m
[...]

* GaiaXPolicy    - no description -,     Argument: JsonObject
* SubjectPolicy  Verifies credential subject,    Argument: JsonObject

(*) ... mutable dynamic policy
```
