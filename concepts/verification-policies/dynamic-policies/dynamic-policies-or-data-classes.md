# Dynamic Policies | Data Classes

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
