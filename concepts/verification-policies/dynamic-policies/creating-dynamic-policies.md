---
description: Example of a Rego policy
---

# Creating Dynamic Policies

### Creating a Sample Policy using [R](../../../usage-examples/open-policy-agent.md)[ego](../../../usage-examples/open-policy-agent.md)

A simple Rego policy that takes a credential subject as input and verifies the subject DID against a given parameter would look like this:

```rego
package system

default main = false

main {
    input.parameter.user == input.credentialData.credentialSubject.id
}
```

{% hint style="info" %}
This policy file is located in the SSIKit test resources: `src/test/resources/rego/subject-policy.rego`
{% endhint %}

### &#x20;Executing a Policy On-The-Fly&#x20;

{% tabs %}
{% tab title="CLI" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/cli-command-line-interface.md) to exectute the command successfully.

```bash
ssikit vc verify -p DynamicPolicy='{ "policy": "src/test/resources/rego/subject-policy.rego", \
  "input": { "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" } }' \
  src/test/resources/rego/VerifiableId.json

```
{% endtab %}
{% endtabs %}

### &#x20;Saving a Dynamic Policy

You can save the policy by name, which simplifies its usage in future verifications.

{% tabs %}
{% tab title="CLI" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/cli-command-line-interface.md) to exectute the command successfully.\
\
**Example**

```bash
ssikit vc policies create \
    -n "MyCustomPolicy" \
    -D "Verifies credential subject against a provided DID" \
    -p src/test/resources/rego/subject-policy.rego \
    -i '{ "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" }'
```

**Flags:**&#x20;

* `-n, --name`:  Policy name, must not conflict with existing policies
* `-D, --description`: Optional policy description
* `-p, --policy`: Path or URL to policy definition. e.g.: rego file for OPA policy engine
* `-i, --input`: Input JSON object for rego query, which can be overridden/extended on verification. Can be a JSON string or JSON file
* `-d, --data-path`: JSON path to the data in the credential which should be verified, default: "$" (whole credential object)
* `-s, --save-policy`: Downloads and/or saves the policy definition locally, rather than keeping the reference to the original URL
* `-f, --force`: Override existing policy with that name (static policies cannot be overridden!)
* `-e, --policy-engine`: Policy engine type, default: OPA. Options, OPA
* `--vc / --no-vc`: Apply/Don't apply to verifiable credentials (default: apply)
* `--vp / --no-vp`: Apply/Don't apply to verifiable presentations (default: don't apply)
{% endtab %}

{% tab title="REST" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/rest-apis.md) to serve the API.

```bash
curl -X 'POST' \
  'http://127.0.0.1:7003/v1/create/{{policyName}}?update=true&downloadPolicy=true' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "MyCustomPolicy",
    "description": "Test",
    "input": {},
    "policy": "package system

default main = false

main {
    input.parameter.user == input.credentialData.credentialSubject.id
}
",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}'
```

**Path parameters:**&#x20;

* `policyName`: _**\[string]**_ Name of the policy, e.g. MyCustomPolicy

**Query parameters:**&#x20;

* `update`: _**\[boolean]**_ Specifies if existing policy with same name should be overridden (if mutable)
* `downloadPolicy`: _**\[boolean]**_ When using an URL to reference the to created policy. Downloads and/or saves the policy definition locally, rather than keeping the reference to the original URL\


**Body**

<pre class="language-json"><code class="lang-json">{
    "name": "MyCustomPolicy",
    "description": "Test",
    "input": {},
    "policy": "package system

               default main = false

<strong>               main {
</strong>                 input.parameter.user == input.credentialData.credentialSubject.id
               }",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}
</code></pre>

* `name`: _**\[string]**_ Policy name, must not conflict with existing policies
* `description`: _**\[string]**_ Optional policy description
* `input`: _**\[JSON]**_ Input JSON object for rego query, which can be overridden/extended on verification. Can be a JSON string or JSON file
* `policy`: _**\[URL, REGO]**_ Whole Policy or URL to policy definition.
* `dataPath`: _**\[JSON path]**_ JSON path to the data in the credential which should be verified, default: "$" (whole credential object)
* `policyQuery`: _**\[string]**_ The query string in the policy engine language. Defaults to\
  "data.system.main".
* `policyEngine`: _**\[string]**_ Policy engine type, default: OPA. Options, OPA
* `applyToVC`: _**\[boolean]**_ Apply/Don't apply to verifiable credentials (default: apply)
* `applyToVP`: _**\[boolean]**_ Apply/Don't apply to verifiable presentaion (default: don't apply)
{% endtab %}
{% endtabs %}
