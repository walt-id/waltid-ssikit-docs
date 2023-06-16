# Verifiable credentials

The following credentials management functions are available:

* [list](#list-credentials) - list verifiable credentials
* [load](#load-credential) - load the verifiable credential
* [delete](#delete-credential) - delete the verifiable credential
* [create](#create-credential) - create a verifiable credential
* [present](#present-credentials) - create a verifiable presentation from the supplied credentials
* [verify](#verifiable-credentials) - verify credential / presentation
* [import](#import-credential) - import the verifiable credential

## List credentials

The `/v1/vc` endpoint lists the available credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc' \
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
The list of credential names (file names)
```
{% endtab %}
{% endtabs %}

E.g. List the available credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    ""
]
```
{% endtab %}
{% endtabs %}

## Load credential

The `/v1/vc/{id}` endpoint loads a credential specified by:

* id - path parameter (required) - the credential id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc/{id}' \
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
  'https://core.ssikit.walt.id/v1/vc/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
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

## Delete credential

The `/v1/vc/{id}` deletes a credential by:

* id - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/vc/{id}' \
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

E.g. Delete the credential with id = `urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270`.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/vc/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

## Create credential

The `/v1/vc/create` endpoint creates a credential.

{% tabs %}
{% tab title="Request body schema" %}
```
{
    "issuerDid": "string",
    "subjectDid": "string",
    "credentialOffer": "string",
    "templateId": "string",
    "domain": "string",
    "nonce": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
The verifiable credential
```
{% endtab %}
{% endtabs %}

E.g. Create a credential from the _UniveristyDegree_ template, having issuer = `did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa` and holder = `did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX`.

{% tabs %}
{% tab title="Request body" %}
```
{
    "issuerDid": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
    "subjectDid": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "templateId": "UniversityDegree"
}
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

## Present credentials

The `/v1/vc/present` endpoint creates a verifiable presentation from the supplied credential. Only _JSON-LD_ format is supported.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vc": "string",
    "holderDid": "string",
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

E.g. Create a verifiable presentation from the provided _VeriafiableID_ credential for a holder with did = `did:web:my.domain`.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vc": "{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"credentialSchema\":{\"id\":\"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Libert\u00E9, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"],\"proof\":{\"type\":\"JsonWebSignature2020\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"created\":\"2022-10-11T10:19:32Z\",\"proofPurpose\":\"assertionMethod\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\"}}",
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vc": "{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"credentialSchema\":{\"id\":\"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Liberté, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"],\"proof\":{\"type\":\"JsonWebSignature2020\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"created\":\"2022-10-11T10:19:32Z\",\"proofPurpose\":\"assertionMethod\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\"}}",
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
    "id": "urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d",
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
                "id": "did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR",
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
            "id": "urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90",
            "issued": "2022-10-11T10:19:31Z",
            "issuer": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL",
            "proof":
            {
                "created": "2022-10-11T10:19:32Z",
                "creator": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL"
            },
            "validFrom": "2022-10-11T10:19:31Z",
            "issuanceDate": "2022-10-11T10:19:31Z",
            "type":
            [
                "VerifiableCredential",
                "VerifiableAttestation",
                "VerifiableId"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-11T10:23:26Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ"
    }
}
```
{% endtab %}
{% endtabs %}

## Verify credentials

The `/v1/vc/verify` endpoint verifies the supplied credential or presentation against the signature policy.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vcOrVp": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
{
    "verificationType": "string",
    "verified": boolean
}
```
{% endtab %}
{% endtabs %}

E.g. Verify a presentation.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcOrVp": "{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"holder\":\"did:web:my.domain\",\"id\":\"urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d\",\"type\":[\"VerifiablePresentation\"],\"verifiableCredential\":[{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"credentialSchema\":{\"id\":\"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Libert\u00E9, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"proof\":{\"created\":\"2022-10-11T10:19:32Z\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\",\"proofPurpose\":\"assertionMethod\",\"type\":\"JsonWebSignature2020\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\"},\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"]}],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:my.domain\",\"created\":\"2022-10-11T10:23:26Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"proofPurpose\":\"authentication\",\"verificationMethod\":\"did:web:my.domain#c5b11445be0e4d37863170df3328630b\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ\"}}"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vcOrVp": "{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"holder\":\"did:web:my.domain\",\"id\":\"urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d\",\"type\":[\"VerifiablePresentation\"],\"verifiableCredential\":[{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"credentialSchema\":{\"id\":\"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Liberté, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"proof\":{\"created\":\"2022-10-11T10:19:32Z\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\",\"proofPurpose\":\"assertionMethod\",\"type\":\"JsonWebSignature2020\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\"},\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"]}],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:my.domain\",\"created\":\"2022-10-11T10:23:26Z\",\"domain\":\"https://api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"proofPurpose\":\"authentication\",\"verificationMethod\":\"did:web:my.domain#c5b11445be0e4d37863170df3328630b\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ\"}}"
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "verificationType": "VERIFIABLE_PRESENTATION",
    "verified": true
}
```
{% endtab %}
{% endtabs %}

## Import credential

The `/v1/vc/import` endpoint imports a verifiable credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
The credential string
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Import the _UniversityDegree_ credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '"{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\",\"https:\/\/www.w3.org\/2018\/credentials\/examples\/v1\"],\"credentialSubject\":{\"degree\":{\"name\":\"Bachelor of Science and Arts\",\"type\":\"BachelorDegree\"},\"id\":\"did:web:my.domain\"},\"id\":\"urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270\",\"issued\":\"2022-10-07T09:53:41.369913097Z\",\"issuer\":{\"id\":\"did:web:walt.id\"},\"validFrom\":\"2022-10-07T09:53:41.369917079Z\",\"issuanceDate\":\"2022-10-07T09:53:41.369917079Z\",\"type\":[\"VerifiableCredential\",\"UniversityDegreeCredential\"],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:walt.id\",\"created\":\"2022-10-07T09:53:41Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ\"}}"'
```
{% endtab %}

{% tab title="Request body" %}
```
"{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\",\"https:\/\/www.w3.org\/2018\/credentials\/examples\/v1\"],\"credentialSubject\":{\"degree\":{\"name\":\"Bachelor of Science and Arts\",\"type\":\"BachelorDegree\"},\"id\":\"did:web:my.domain\"},\"id\":\"urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270\",\"issued\":\"2022-10-07T09:53:41.369913097Z\",\"issuer\":{\"id\":\"did:web:walt.id\"},\"validFrom\":\"2022-10-07T09:53:41.369917079Z\",\"issuanceDate\":\"2022-10-07T09:53:41.369917079Z\",\"type\":[\"VerifiableCredential\",\"UniversityDegreeCredential\"],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:walt.id\",\"created\":\"2022-10-07T09:53:41Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ\"}}"
```
{% endtab %}
{% endtabs %}