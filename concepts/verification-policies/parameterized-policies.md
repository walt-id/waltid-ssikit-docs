---
noIndex: true
---

# Parameterized Policies

Some policies may require a parameter or argument for execution. The parameter is indicated in the policy list output, together with the expected data type.

### Using A Parameterized Policy&#x20;

{% tabs %}
{% tab title="CLI" %}
Please refer to the [SSI-Kit setup section](../../getting-started/cli-command-line-interface.md) to exectute the command successfully.\
\
Let's verify a credential using the parameterless SignaturePolicy and ChallengePolicy which taks a paramter.

```
ssikit vc verify \
-p SignaturePolicy \
-p ChallengePolicy='{"challenges": ["362df5ec-37ab-46a7-aa71-767d8f277b69"]}' \
src/test/resources/rego/VerifiableId.json
```

**Flags**

* `-p, --policy`: Verification policy. Can be specified multiple times. By default, SignaturePolicy is used. To specify a policy argument (if required), use the format PolicyName='{"myParam": "myValue", ...}', to specify the JSON object directly, or PolicyName=path/to/arg.json, to read the argument from a JSON file.

\
**The Challange Policy**

It checks that the challenge of the credential is one of the challenges given in the ChallengePolicyArg argument.
{% endtab %}

{% tab title="REST" %}
Please refer to the [SSI-Kit setup section](../../getting-started/rest-apis.md) to serve the API.\
\
Using the `/v1/verify` enpoint in the Auditor API to verify a credential

```bash
curl -X 'POST' \
  'http://127.0.0.1:7003/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
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
}'
```

**Body**

```json
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

* `policies`: _**\[array]**_ A list of policy definitions to verify against
  * `policy`: _**\[string]**_ The name/id of the policy
  * `argument`: _**\[JSON]**_ The argument needed by the policy (if required)
* `credentials`: _**\[array]**_ An array of credentials in JWT, or LD\_PROOF format
{% endtab %}
{% endtabs %}

