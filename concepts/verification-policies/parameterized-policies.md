# Parameterized Policies

Some policies may require a parameter or argument for execution. The parameter is indicated in the policy list output, together with the expected data type.

**CLI**

The **CLI** allows for specifying a parameter with the verification policy, using the syntax: `PolicyName='{...}'`, where the argument is given as a JSON Object, shown here as `{...}`.

In this example we verify a credential by the parameterless **SignaturePolicy** and the parameterized **ChallengePolicy**:

```
ssikit vc verify -p SignaturePolicy -p ChallengePolicy='{ "challenges": [ "362df5ec-37ab-46a7-aa71-767d8f277b69" ] }' src/test/resources/rego/VerifiableId.json
```

The challenge policy checks that the challenge of the credential is one of the challenges given in the ChallengePolicyArg argument.

**REST API**

The same example using the **Auditor REST API**, with the parameterless **SignaturePolicy** and the parameterized **ChallengePolicy** would look like this:

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

