# Dynamic Policies

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
    val dataPath: String = "\$",
    val policyQuery: String = "data.system.main",
    val policyEngine: PolicyEngineType = PolicyEngineType.OPA,
    val applyToVC: Boolean = true,
    val applyToVP: Boolean = false
)
```

**Properties:**

* `name`: policy name, defaults to "DynamicPolicy"
* `description`: Optional description of the policy
* `input`: A generic map (JSON object), holding the input data required by the policy (or an empty map if no input is required)
* `policy`: the policy definition (e.g. rego file), which can be a file path, URL, JSON Path (if policy is defined in a credential property) or the code/script directly.
* `dataPath`: The path to the credential data, which should be verified, by default it's the whole credential object `$`. To use e.g. only the credential subject as verification data, specify the JSON path like this: `$.credentialSubject`.
* `policyQuery`: The query string in the policy engine lingo, defaults to "data.system.main"
* `policyEngine`: The engine to use for execution of the policy. By default `OPA` (Open Policy Agent) is used.
* `applyToVC`: Apply this policy to verifiable credentials (Default: true)
* `applyToVP`: Apply this policy to verifiable presentations (Default: false)

### Sample policy

This simple rego policy takes a credential subject as input and verifies the subject DID against a given parameter.

```
package system

default main = false

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
