---
description: Auditor REST API functions.
---

# Auditor API - For Verifiers

[Swagger](https://auditor.ssikit.walt.id/v1/swagger) | [ReDoc](https://auditor.ssikit.walt.id/v1/redoc)

The _Auditor API_ enables anybody to act as a "Verifier" (i.e. verify Verifiable Credentials or Verifiable Presentations). The validation steps can be easily configured by existing or custom _policies_.

The following functionality is available:

* [Verification](auditor-api.md#verification) - credential / presentation verification
* [Policy](auditor-api.md#policies) - policy related functions

## Verification

The `/v1/verify` endpoint verifies a list of credentials / presentations specified in the `JSON-LD` format against a set of policies. Each of the policy should be registered with the Auditor before being used in the verification. If at least one of the listed policies fails the verification, then the entire credential is considered to be invalid.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://auditor.ssikit.walt.id/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "policies":
    [
        {
            "policy": "string",
            "argument":
            {
                "additionalProp1":
                {},
                "additionalProp2":
                {},
                "additionalProp3":
                {}
            }
        }
    ],
    "credentials":
    [
        {
            "json": "string",
            "issuanceDate": "string",
            "dateFormat":
            {
                "locale":
                {
                    "language": "string",
                    "script": "string",
                    "variant": "string",
                    "displayName": "string",
                    "country": "string",
                    "unicodeLocaleAttributes":
                    [
                        "string"
                    ],
                    "unicodeLocaleKeys":
                    [
                        "string"
                    ],
                    "displayLanguage": "string",
                    "displayScript": "string",
                    "displayCountry": "string",
                    "displayVariant": "string",
                    "extensionKeys":
                    [
                        "string"
                    ],
                    "iso3Language": "string",
                    "iso3Country": "string"
                },
                "decimalStyle":
                {
                    "zeroDigit": "string",
                    "positiveSign": "string",
                    "negativeSign": "string",
                    "decimalSeparator": "string"
                },
                "resolverStyle": "STRICT",
                "resolverFields":
                [
                    {
                        "baseUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "rangeUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "dateBased": true,
                        "timeBased": true
                    }
                ],
                "zone":
                {
                    "id": "string",
                    "rules":
                    {
                        "fixedOffset": true,
                        "transitions":
                        [
                            {
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "duration":
                                {
                                    "seconds": 0,
                                    "nano": 0,
                                    "negative": true,
                                    "zero": true,
                                    "units":
                                    [
                                        {
                                            "dateBased": true,
                                            "timeBased": true,
                                            "durationEstimated": true
                                        }
                                    ]
                                },
                                "gap": true,
                                "dateTimeBefore": "2022-10-06T14:45:20.119Z",
                                "dateTimeAfter": "2022-10-06T14:45:20.119Z",
                                "overlap": true,
                                "instant": "2022-10-06T14:45:20.119Z"
                            }
                        ],
                        "transitionRules":
                        [
                            {
                                "month": "JANUARY",
                                "timeDefinition": "UTC",
                                "standardOffset":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "dayOfWeek": "MONDAY",
                                "dayOfMonthIndicator": 0,
                                "localTime":
                                {
                                    "hour": 0,
                                    "minute": 0,
                                    "second": 0,
                                    "nano": 0
                                },
                                "midnightEndOfDay": true
                            }
                        ]
                    }
                },
                "chronology":
                {
                    "id": "string",
                    "calendarType": "string"
                }
            },
            "jwt": "string",
            "id": "string",
            "type":
            [
                "string"
            ],
            "subject": "string",
            "expirationDate": "string",
            "credentialSchema":
            {
                "id": "string",
                "type": "string"
            },
            "proof":
            {
                "type": "string",
                "creator": "string",
                "created": "string",
                "domain": "string",
                "proofPurpose": "string",
                "verificationMethod": "string",
                "jws": "string",
                "nonce": "string"
            },
            "challenge": "string",
            "validFrom": "string",
            "issued": "string",
            "issuer": "string"
        }
    ]
}
```
{% endtab %}

{% tab title="Response body" %}
```
[
    {
        "valid": true,
        "results":
        [
            {
                "valid": true,
                "policyResults":
                {
                    "additionalProp1": true,
                    "additionalProp2": true,
                    "additionalProp3": true
                }
            }
        ]
    }
]
```
{% endtab %}
{% endtabs %}

E.g Verification of a UniversityDegree credential against Signature and JsonSchema policies, where SignaturePolicy is failing.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://auditor.ssikit.walt.id/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "policies":
    [
        {
            "policy": "SignaturePolicy"
        }
    ],
    "credentials":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://www.w3.org/2018/credentials/examples/v1"
            ],
            "credentialSubject":
            {
                "degree":
                {
                    "name": "Bachelor of Science and Arts",
                    "type": "BachelorDegree"
                },
                "id": "did:key:z6Mkv58vGsBMwbiyQ3P93MRnYfRgGvn4STEEsj5hFHYe51wu"
            },
            "id": "urn:uuid:7c9d7748-1b66-4361-98eb-c8aab625d9d6",
            "issued": "2022-10-06T15:49:20Z",
            "issuer":
            {
                "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
            },
            "validFrom": "2022-10-06T15:49:20Z",
            "issuanceDate": "2022-10-06T15:49:20Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ],
            "proof":
            {
                "type": "JsonWebSignature2020",
                "creator": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
                "created": "2022-10-06T15:49:20Z",
                "proofPurpose": "assertionMethod",
                "verificationMethod": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..iOAli2QhHpp0jZeF2tUj5H4gi_rwaWeypKE4gVdSePp-747gwDCm-bLFjE1MBOFSILZYBWtVWCitrTUmUDfUBw"
            }
        }
    ]
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "policies":
    [
        {
            "policy": "SignaturePolicy"
        },
    ],
    "credentials":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://www.w3.org/2018/credentials/examples/v1"
            ],
            "credentialSubject":
            {
                "degree":
                {
                    "name": "Bachelor of Science and Arts",
                    "type": "BachelorDegree"
                },
                "id": "did:key:z6Mkv58vGsBMwbiyQ3P93MRnYfRgGvn4STEEsj5hFHYe51wu"
            },
            "id": "urn:uuid:7c9d7748-1b66-4361-98eb-c8aab625d9d6",
            "issued": "2022-10-06T15:49:20Z",
            "issuer":
            {
                "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
            },
            "validFrom": "2022-10-06T15:49:20Z",
            "issuanceDate": "2022-10-06T15:49:20Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ],
            "proof":
            {
                "type": "JsonWebSignature2020",
                "creator": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
                "created": "2022-10-06T15:49:20Z",
                "proofPurpose": "assertionMethod",
                "verificationMethod": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..iOAli2QhHpp0jZeF2tUj5H4gi_rwaWeypKE4gVdSePp-747gwDCm-bLFjE1MBOFSILZYBWtVWCitrTUmUDfUBw"
            }
        }
    ]
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "valid": false,
    "results":
    [
        {
            "valid": false,
            "policyResults":
            {
                "SignaturePolicy": true
            }
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Policies

The Auditor Rest API also enables policy management with the following methods:

* [list](auditor-api.md#list-policies) - display the available verification policies
* [create](auditor-api.md#create-policy) - create a dynamic verification policy
* [delete](auditor-api.md#delete-policy) - remove a dynamic verification policy

### List policies

The `/v1/policies` endpoint lists the available verification policies. The policy `id` field is used to reference the policy during verification.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://auditor.ssikit.walt.id/v1/policies' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body" %}
```
No parameters
```
{% endtab %}

{% tab title="Response body " %}
```
[
    {
        "applyToVC": true,
        "applyToVP": true,
        "id": "string",
        "description": "string"
    }
]
```
{% endtab %}
{% endtabs %}

E.g. Listing of the verification policies

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://auditor.ssikit.walt.id/v1/policies' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    {
        "id": "SignaturePolicy",
        "description": "Verify by signature",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "JsonSchemaPolicy",
        "description": "Verify by JSON schema",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "TrustedSchemaRegistryPolicy",
        "description": "Verify by EBSI Trusted Schema Registry",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "TrustedIssuerDidPolicy",
        "description": "Verify by trusted issuer did",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "TrustedIssuerRegistryPolicy",
        "description": "Verify by trusted EBSI Trusted Issuer Registry record",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "TrustedSubjectDidPolicy",
        "description": "Verify by trusted subject did",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "IssuedDateBeforePolicy",
        "description": "Verify by issuance date",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "ValidFromBeforePolicy",
        "description": "Verify by valid from",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "ExpirationDateAfterPolicy",
        "description": "Verify by expiration date",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "GaiaxTrustedPolicy",
        "description": "Verify Gaiax trusted fields",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "GaiaxSDPolicy",
        "description": "Verify Gaiax SD fields",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "ChallengePolicy",
        "description": "Verify challenge",
        "argumentType": "ChallengePolicyArg",
        "isMutable": false
    },
    {
        "id": "VpTokenClaimPolicy",
        "description": "Verify verifiable presentation by OIDC/SIOPv2 VP token claim",
        "argumentType": "VpTokenClaim",
        "isMutable": false
    },
    {
        "id": "CredentialStatusPolicy",
        "description": "Verify by credential status",
        "argumentType": "None",
        "isMutable": false
    },
    {
        "id": "DynamicPolicy",
        "description": "Verify credential by rego policy",
        "argumentType": "DynamicPolicyArg",
        "isMutable": false
    },
    {
        "id": "VerifiableMandatePolicy",
        "description": "Predefined policy for verifiable mandates",
        "argumentType": "JsonObject",
        "isMutable": false
    }
]
```
{% endtab %}
{% endtabs %}

## Create policy

The `/v1/create/{name}` creates a dynamic policy. The following parameters can be specified:

* `name` path parameter (required) - specifies the value to be used as the policy `id`
* `update` query parameter (optional, defualts to `false`) - accepts `boolean` values and specifies whether it should override an existing policy with the same `name` (only if the policy is mutable)
* `downloadPolicy` query parameter (optional, defaults to `false`) - accepts `boolean` values and identifies the scope of the `policy` field:
  * specifies a remote source that should be resolved to a policy
  * specifies the actual policy content

More details on creating verification policies and fields definitions can be found at [Verification Policies](https://docs.walt.id/v/ssikit/concepts/verification-policies).

{% tabs %}
{% tab title="Request body schema" %}
```
{
    "name": "string",
    "description": "string",
    "input":
    {
        "additionalProp1":
        {},
        "additionalProp2":
        {},
        "additionalProp3":
        {}
    },
    "policy": "string",
    "dataPath": "string",
    "policyQuery": "string",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}
```
{% endtab %}
{% endtabs %}

E.g. Creating a Rego policy that checks if a credential subject id is not null or empty

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://auditor.ssikit.walt.id/v1/create/MyPolicy?update=false&downloadPolicy=true' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "MyPolicy",
    "description": "my policy",
    "input": {},
    "policy": "package system\r\nimport future.keywords.if\r\ndefault allow := false\r\nallow if regex.match(\".+\", data.credentialSubject.id)",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "name": "MyPolicy",
    "description": "my policy",
    "policy": "package system\r\nimport future.keywords.if\r\ndefault allow := false\r\nallow if regex.match(\".+\", data.credentialSubject.id)",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}
```
{% endtab %}

{% tab title="Response body" %}
Code 200
{% endtab %}
{% endtabs %}

## Delete policy

The `/v1/delete/{name}` endpoint deletes a dynamic policy. The following parameters can be specified:

* `name` path parameter (required) - specifies the `id` value of the policy

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://auditor.ssikit.walt.id/v1/delete/{name}' \
  -H 'accept: */*'
```
{% endtab %}

{% tab title="Response body" %}
Policy removed / Policy not found
{% endtab %}
{% endtabs %}

E.g. Removing the policy having 'MyPolicy' name

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://auditor.ssikit.walt.id/v1/delete/MyPolicy' \
  -H 'accept: */*'
```
{% endtab %}

{% tab title="Response body" %}
Policy removed / Policy not found
{% endtab %}
{% endtabs %}
