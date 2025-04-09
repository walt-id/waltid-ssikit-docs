---
noIndex: true
---

# Credentials management

The following functions are available for credentials management:

* [List](credentials-management.md#list-credentials) - lists the available credentials
* [List compact](credentials-management.md#list-credentials-compact) - lists credential ids
* [Load](credentials-management.md#load-credential) - loads a credential by id
* [Store](credentials-management.md#store-credential) - store a credential
* [Delete](credentials-management.md#delete-credential) - delete a credential by id
* [Present](credentials-management.md#present-credential) - create a verifiable presentation from specific credentials
* [Present stored](credentials-management.md#present-stored-credential) - create a verifiable presentation from specific stored credential ids

## List credentials

The `/credentials` endpoint lists the available credentials:

* id - query parameter (optional) - the list of credentials ids

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}

{% tab title="Response body schema" %}
```
The list of credentials
```
{% endtab %}
{% endtabs %}

E.g. List the the credentials having ids _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_ and _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84271_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials?id=urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270&id=urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84271' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "list":
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
                "id": "did:web:my.domain"
            },
            "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
            "issued": "2022-10-07T09:53:41.369913097Z",
            "issuer":
            {
                "id": "did:web:walt.id"
            },
            "proof":
            {
                "created": "2022-10-07T09:53:41Z",
                "creator": "did:web:walt.id",
                "domain": "https://api.preprod.ebsi.eu",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
                "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
                "type": "Ed25519Signature2018"
            },
            "validFrom": "2022-10-07T09:53:41.369917079Z",
            "issuanceDate": "2022-10-07T09:53:41.369917079Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## List credentials compact

The `/credentials/list/credentialIds` lists the available credentials ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/list/credentialIds' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}

{% tab title="Response body schema" %}
```
The list of credentials ids
```
{% endtab %}
{% endtabs %}

E.g. List the available credentials ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/list/credentialIds' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "list":
    [
        "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
    ]
}
```
{% endtab %}
{% endtabs %}

## Load credential

The `/credentials/{id}` loads a credential specified by:

* id - path parameter (required) - the credential id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/{id}' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}

{% tab title="Response body schema" %}
```
The credential string
```
{% endtab %}
{% endtabs %}

E.g. Load the credential having id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
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
        "id": "did:web:my.domain"
    },
    "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
    "issued": "2022-10-07T09:53:41.369913097Z",
    "issuer":
    {
        "id": "did:web:walt.id"
    },
    "proof":
    {
        "created": "2022-10-07T09:53:41Z",
        "creator": "did:web:walt.id",
        "domain": "https://api.preprod.ebsi.eu",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "type": "Ed25519Signature2018"
    },
    "validFrom": "2022-10-07T09:53:41.369917079Z",
    "issuanceDate": "2022-10-07T09:53:41.369917079Z",
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ]
}
```
{% endtab %}
{% endtabs %}

## Store credential

The `/credentials/{alias}` endpoint stores a verifiable credential by:

* alias - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'PUT' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
The body should contain, the VC to be store. If no adjustments are required to VC, then the body can be the VC itself (e.g. the one received from the create VC endpoint).

```
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
                        "dateTimeBefore": "2022-10-09T09:09:41.896Z",
                        "dateTimeAfter": "2022-10-09T09:09:41.896Z",
                        "overlap": true,
                        "instant": "2022-10-09T09:09:41.896Z"
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
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 201
```
{% endtab %}
{% endtabs %}

E.g. Store the `UniversityDegree` verifiable credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'PUT' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "@context" : [ "https://www.w3.org/2018/credentials/v1", "https://www.w3.org/2018/credentials/examples/v1" ],
  "credentialSubject" : {
    "degree" : {
      "name" : "Bachelor of Science and Arts",
      "type" : "BachelorDegree"
    },
    "id" : "did:web:my.domain"
  },
  "id" : "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
  "issued" : "2022-10-07T09:53:41.369913097Z",
  "issuer" : {
    "id" : "did:web:walt.id"
  },
  "validFrom" : "2022-10-07T09:53:41.369917079Z",
  "issuanceDate" : "2022-10-07T09:53:41.369917079Z",
  "type" : [ "VerifiableCredential", "UniversityDegreeCredential" ],
  "proof" : {
    "type" : "Ed25519Signature2018",
    "creator" : "did:web:walt.id",
    "created" : "2022-10-07T09:53:41Z",
    "domain" : "https://api.preprod.ebsi.eu",
    "nonce" : "dc2be572-cca4-43dc-9903-0fec1dcf786f",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ"
  }
}'
```
{% endtab %}

{% tab title="Request body" %}
```
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
        "id": "did:web:my.domain"
    },
    "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
    "issued": "2022-10-07T09:53:41.369913097Z",
    "issuer":
    {
        "id": "did:web:walt.id"
    },
    "validFrom": "2022-10-07T09:53:41.369917079Z",
    "issuanceDate": "2022-10-07T09:53:41.369917079Z",
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:walt.id",
        "created": "2022-10-07T09:53:41Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ"
    }
}
```
{% endtab %}
{% endtabs %}

## Delete credential

The `/credentials/{alias}` deletes a credential by:

* alias - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/credentials/{alias}' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Delete the credential with id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

## Present credential

The `/credentials/present` endpoint creates a verifiable presentation from the specified credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vcs":
    [
        "string"
    ],
    "holderDid": "string",
    "verifierDid": "string",
    "domain": "string",
    "challenge": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
{
    "context":
    [
        "string"
    ],
    "id": "string",
    "holder": "string",
    "verifiableCredential":
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
                                "dateTimeBefore": "2022-10-09T11:30:48.206Z",
                                "dateTimeAfter": "2022-10-09T11:30:48.206Z",
                                "overlap": true,
                                "instant": "2022-10-09T11:30:48.206Z"
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
    ],
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
    "issued": "string",
    "validFrom": "string",
    "expirationDate": "string",
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
                        "dateTimeBefore": "2022-10-09T11:30:48.207Z",
                        "dateTimeAfter": "2022-10-09T11:30:48.207Z",
                        "overlap": true,
                        "instant": "2022-10-09T11:30:48.207Z"
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
    "type":
    [
        "string"
    ],
    "subject": "string",
    "credentialSchema":
    {
        "id": "string",
        "type": "string"
    },
    "issuer": "string",
    "challenge": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Create a verifiable presentation from the provided _VeriafiableID_ and _OpenBadgeCredential_ credentials for a holder with did = _did:web:my.domain_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcs": [
"{\r\n    \"@context\":\r\n    [\r\n        \"https:\/\/www.w3.org\/2018\/credentials\/v1\"\r\n    ],\r\n    \"credentialSchema\":\r\n    {\r\n        \"id\": \"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\r\n        \"type\": \"FullJsonSchemaValidator2021\"\r\n    },\r\n    \"credentialSubject\":\r\n    {\r\n        \"currentAddress\":\r\n        [\r\n            \"1 Boulevard de la Libert\u00E9, 59800 Lille\"\r\n        ],\r\n        \"dateOfBirth\": \"1993-04-08\",\r\n        \"familyName\": \"DOE\",\r\n        \"firstName\": \"Jane\",\r\n        \"gender\": \"FEMALE\",\r\n        \"id\": \"did:web:my.domain\",\r\n        \"nameAndFamilyNameAtBirth\": \"Jane DOE\",\r\n        \"personalIdentifier\": \"0904008084H\",\r\n        \"placeOfBirth\": \"LILLE, FRANCE\"\r\n    },\r\n    \"evidence\":\r\n    [\r\n        {\r\n            \"documentPresence\":\r\n            [\r\n                \"Physical\"\r\n            ],\r\n            \"evidenceDocument\":\r\n            [\r\n                \"Passport\"\r\n            ],\r\n            \"subjectPresence\": \"Physical\",\r\n            \"type\":\r\n            [\r\n                \"DocumentVerification\"\r\n            ],\r\n            \"verifier\": \"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"\r\n        }\r\n    ],\r\n    \"id\": \"urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a\",\r\n    \"issued\": \"2022-10-09T10:11:51Z\",\r\n    \"issuer\": \"did:web:walt.id\",\r\n    \"validFrom\": \"2022-10-09T10:11:51Z\",\r\n    \"issuanceDate\": \"2022-10-09T10:11:51Z\",\r\n    \"type\":\r\n    [\r\n        \"VerifiableCredential\",\r\n        \"VerifiableAttestation\",\r\n        \"VerifiableId\"\r\n    ],\r\n    \"proof\":\r\n    {\r\n        \"type\": \"JsonWebSignature2020\",\r\n        \"creator\": \"did:web:walt.id\",\r\n        \"created\": \"2022-10-09T10:11:52Z\",\r\n        \"proofPurpose\": \"assertionMethod\",\r\n        \"verificationMethod\": \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n        \"jws\": \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA\"\r\n    }\r\n}",
"{\r\n  \"@context\" : [ \"https:\/\/www.w3.org\/2018\/credentials\/v1\", \"https:\/\/w3c-ccg.github.io\/vc-ed\/plugfest-1-2022\/jff-vc-edu-plugfest-1-context.json\" ],\r\n  \"credentialSubject\" : {\r\n    \"achievement\" : {\r\n      \"criteria\" : {\r\n        \"narrative\" : \"The first cohort of the JFF Plugfest 1 in May\/June of 2021 collaborated to push interoperability of VCs in education forward.\",\r\n        \"type\" : \"Criteria\"\r\n      },\r\n      \"description\" : \"This wallet can display this Open Badge 3.0\",\r\n      \"image\" : \"https:\/\/w3c-ccg.github.io\/vc-ed\/plugfest-1-2022\/images\/plugfest-1-badge-image.png\",\r\n      \"name\" : \"Our Wallet Passed JFF Plugfest #1 2022\",\r\n      \"type\" : \"Achievement\"\r\n    },\r\n    \"id\" : \"did:web:my.domain\",\r\n    \"type\" : \"AchievementSubject\"\r\n  },\r\n  \"id\" : \"urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25\",\r\n  \"issuanceDate\" : \"2020-03-10T04:24:12.164Z\",\r\n  \"issued\" : \"2022-10-09T10:12:50Z\",\r\n  \"issuer\" : {\r\n    \"id\" : \"did:web:walt.id\",\r\n    \"image\" : \"https:\/\/kayaelle.github.io\/vc-ed\/plugfest-1-2022\/images\/JFF_LogoLockup.png\",\r\n    \"name\" : \"Jobs for the Future (JFF)\",\r\n    \"type\" : \"Profile\",\r\n    \"url\" : \"https:\/\/kayaelle.github.io\/vc-ed\/plugfest-1-2022\/images\/JFF_LogoLockup.png\"\r\n  },\r\n  \"validFrom\" : \"2022-10-09T10:12:50Z\",\r\n  \"type\" : [ \"VerifiableCredential\", \"OpenBadgeCredential\" ],\r\n  \"proof\" : {\r\n    \"type\" : \"JsonWebSignature2020\",\r\n    \"creator\" : \"did:web:walt.id\",\r\n    \"created\" : \"2022-10-09T10:12:50Z\",\r\n    \"proofPurpose\" : \"assertionMethod\",\r\n    \"verificationMethod\" : \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n    \"jws\" : \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg\"\r\n  }\r\n}"
  ],
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vcs":
    [
        "{\r\n    \"@context\":\r\n    [\r\n        \"https://www.w3.org/2018/credentials/v1\"\r\n    ],\r\n    \"credentialSchema\":\r\n    {\r\n        \"id\": \"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\r\n        \"type\": \"FullJsonSchemaValidator2021\"\r\n    },\r\n    \"credentialSubject\":\r\n    {\r\n        \"currentAddress\":\r\n        [\r\n            \"1 Boulevard de la Liberté, 59800 Lille\"\r\n        ],\r\n        \"dateOfBirth\": \"1993-04-08\",\r\n        \"familyName\": \"DOE\",\r\n        \"firstName\": \"Jane\",\r\n        \"gender\": \"FEMALE\",\r\n        \"id\": \"did:web:my.domain\",\r\n        \"nameAndFamilyNameAtBirth\": \"Jane DOE\",\r\n        \"personalIdentifier\": \"0904008084H\",\r\n        \"placeOfBirth\": \"LILLE, FRANCE\"\r\n    },\r\n    \"evidence\":\r\n    [\r\n        {\r\n            \"documentPresence\":\r\n            [\r\n                \"Physical\"\r\n            ],\r\n            \"evidenceDocument\":\r\n            [\r\n                \"Passport\"\r\n            ],\r\n            \"subjectPresence\": \"Physical\",\r\n            \"type\":\r\n            [\r\n                \"DocumentVerification\"\r\n            ],\r\n            \"verifier\": \"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"\r\n        }\r\n    ],\r\n    \"id\": \"urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a\",\r\n    \"issued\": \"2022-10-09T10:11:51Z\",\r\n    \"issuer\": \"did:web:walt.id\",\r\n    \"validFrom\": \"2022-10-09T10:11:51Z\",\r\n    \"issuanceDate\": \"2022-10-09T10:11:51Z\",\r\n    \"type\":\r\n    [\r\n        \"VerifiableCredential\",\r\n        \"VerifiableAttestation\",\r\n        \"VerifiableId\"\r\n    ],\r\n    \"proof\":\r\n    {\r\n        \"type\": \"JsonWebSignature2020\",\r\n        \"creator\": \"did:web:walt.id\",\r\n        \"created\": \"2022-10-09T10:11:52Z\",\r\n        \"proofPurpose\": \"assertionMethod\",\r\n        \"verificationMethod\": \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n        \"jws\": \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA\"\r\n    }\r\n}",
        "{\r\n  \"@context\" : [ \"https://www.w3.org/2018/credentials/v1\", \"https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/jff-vc-edu-plugfest-1-context.json\" ],\r\n  \"credentialSubject\" : {\r\n    \"achievement\" : {\r\n      \"criteria\" : {\r\n        \"narrative\" : \"The first cohort of the JFF Plugfest 1 in May/June of 2021 collaborated to push interoperability of VCs in education forward.\",\r\n        \"type\" : \"Criteria\"\r\n      },\r\n      \"description\" : \"This wallet can display this Open Badge 3.0\",\r\n      \"image\" : \"https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/images/plugfest-1-badge-image.png\",\r\n      \"name\" : \"Our Wallet Passed JFF Plugfest #1 2022\",\r\n      \"type\" : \"Achievement\"\r\n    },\r\n    \"id\" : \"did:web:my.domain\",\r\n    \"type\" : \"AchievementSubject\"\r\n  },\r\n  \"id\" : \"urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25\",\r\n  \"issuanceDate\" : \"2020-03-10T04:24:12.164Z\",\r\n  \"issued\" : \"2022-10-09T10:12:50Z\",\r\n  \"issuer\" : {\r\n    \"id\" : \"did:web:walt.id\",\r\n    \"image\" : \"https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png\",\r\n    \"name\" : \"Jobs for the Future (JFF)\",\r\n    \"type\" : \"Profile\",\r\n    \"url\" : \"https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png\"\r\n  },\r\n  \"validFrom\" : \"2022-10-09T10:12:50Z\",\r\n  \"type\" : [ \"VerifiableCredential\", \"OpenBadgeCredential\" ],\r\n  \"proof\" : {\r\n    \"type\" : \"JsonWebSignature2020\",\r\n    \"creator\" : \"did:web:walt.id\",\r\n    \"created\" : \"2022-10-09T10:12:50Z\",\r\n    \"proofPurpose\" : \"assertionMethod\",\r\n    \"verificationMethod\" : \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n    \"jws\" : \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg\"\r\n  }\r\n}"
    ],
    "holderDid": "did:web:my.domain"
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1"
    ],
    "holder": "did:web:my.domain",
    "id": "urn:uuid:0f9a8692-badf-4f0c-aa07-a4c3279e3470",
    "type":
    [
        "VerifiablePresentation"
    ],
    "verifiableCredential":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1"
            ],
            "credentialSchema":
            {
                "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
                "type": "FullJsonSchemaValidator2021"
            },
            "credentialSubject":
            {
                "currentAddress":
                [
                    "1 Boulevard de la Liberté, 59800 Lille"
                ],
                "dateOfBirth": "1993-04-08",
                "familyName": "DOE",
                "firstName": "Jane",
                "gender": "FEMALE",
                "id": "did:web:my.domain",
                "nameAndFamilyNameAtBirth": "Jane DOE",
                "personalIdentifier": "0904008084H",
                "placeOfBirth": "LILLE, FRANCE"
            },
            "evidence":
            [
                {
                    "documentPresence":
                    [
                        "Physical"
                    ],
                    "evidenceDocument":
                    [
                        "Passport"
                    ],
                    "subjectPresence": "Physical",
                    "type":
                    [
                        "DocumentVerification"
                    ],
                    "verifier": "did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
                }
            ],
            "id": "urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a",
            "issued": "2022-10-09T10:11:51Z",
            "issuer": "did:web:walt.id",
            "proof":
            {
                "created": "2022-10-09T10:11:52Z",
                "creator": "did:web:walt.id",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:web:walt.id#c1672b42f846471eb2c22fd601169566"
            },
            "validFrom": "2022-10-09T10:11:51Z",
            "issuanceDate": "2022-10-09T10:11:51Z",
            "type":
            [
                "VerifiableCredential",
                "VerifiableAttestation",
                "VerifiableId"
            ]
        },
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/jff-vc-edu-plugfest-1-context.json"
            ],
            "credentialSubject":
            {
                "achievement":
                {
                    "criteria":
                    {
                        "narrative": "The first cohort of the JFF Plugfest 1 in May/June of 2021 collaborated to push interoperability of VCs in education forward.",
                        "type": "Criteria"
                    },
                    "description": "This wallet can display this Open Badge 3.0",
                    "image": "https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/images/plugfest-1-badge-image.png",
                    "name": "Our Wallet Passed JFF Plugfest #1 2022",
                    "type": "Achievement"
                },
                "id": "did:web:my.domain",
                "type": "AchievementSubject"
            },
            "id": "urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25",
            "issuanceDate": "2020-03-10T04:24:12.164Z",
            "issued": "2022-10-09T10:12:50Z",
            "issuer":
            {
                "id": "did:web:walt.id",
                "image": "https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png",
                "name": "Jobs for the Future (JFF)",
                "type": "Profile",
                "url": "https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png"
            },
            "proof":
            {
                "created": "2022-10-09T10:12:50Z",
                "creator": "did:web:walt.id",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:web:walt.id#c1672b42f846471eb2c22fd601169566"
            },
            "validFrom": "2022-10-09T10:12:50Z",
            "type":
            [
                "VerifiableCredential",
                "OpenBadgeCredential"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-09T10:21:11Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..2S3aHQISbL81Dbe1yOakXBFGvUJjxEZ7zGZZZ3XOJibtAON5v9lr5Q9NGt1c8h0zSrTLQDl2-fQ7A6HA9KL9Cw"
    }
}
```
{% endtab %}
{% endtabs %}

## Present stored credential

The `/credentials/presentIds` endpoint creates a verifiable presentation from the specified credential ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/presentIds' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vcIds":
    [
        "string"
    ],
    "holderDid": "string",
    "verifierDid": "string",
    "domain": "string",
    "challenge": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
{
    "context":
    [
        "string"
    ],
    "id": "string",
    "holder": "string",
    "verifiableCredential":
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
                                "dateTimeBefore": "2022-10-09T09:52:44.738Z",
                                "dateTimeAfter": "2022-10-09T09:52:44.738Z",
                                "overlap": true,
                                "instant": "2022-10-09T09:52:44.738Z"
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
    ],
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
    "issued": "string",
    "validFrom": "string",
    "expirationDate": "string",
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
                        "dateTimeBefore": "2022-10-09T09:52:44.739Z",
                        "dateTimeAfter": "2022-10-09T09:52:44.739Z",
                        "overlap": true,
                        "instant": "2022-10-09T09:52:44.739Z"
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
    "type":
    [
        "string"
    ],
    "subject": "string",
    "credentialSchema":
    {
        "id": "string",
        "type": "string"
    },
    "issuer": "string",
    "challenge": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Create a verifiable presentation from the stored credential having id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_ for the holder with did = _did:web:my.domain_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/presentIds' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcIds": [
    "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
  ],
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vcIds":
    [
        "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
    ],
    "holderDid": "did:web:my.domain"
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1"
    ],
    "holder": "did:web:my.domain",
    "id": "urn:uuid:35e627b2-297c-4d33-85cd-a4dfc40bab32",
    "type":
    [
        "VerifiablePresentation"
    ],
    "verifiableCredential":
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
                "id": "did:web:my.domain"
            },
            "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
            "issued": "2022-10-07T09:53:41.369913097Z",
            "issuer":
            {
                "id": "did:web:walt.id"
            },
            "proof":
            {
                "created": "2022-10-07T09:53:41Z",
                "creator": "did:web:walt.id",
                "domain": "https://api.preprod.ebsi.eu",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
                "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
                "type": "Ed25519Signature2018"
            },
            "validFrom": "2022-10-07T09:53:41.369917079Z",
            "issuanceDate": "2022-10-07T09:53:41.369917079Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-09T09:52:44Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..KCfytKgejnjdW_D632lugaj08E9yO8DcDmNcAoGHywld7twcUf1QqKoidfGNW3j2un4ywqRnjSIiYzK8ZxoXDg"
    }
}
```
{% endtab %}
{% endtabs %}
