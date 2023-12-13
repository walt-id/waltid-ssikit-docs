---
description: Signatory REST API functions.
---

# Signatory API - For Issuers

[Swagger](https://signatory.ssikit.walt.id/v1/swagger) | [Redoc](https://signatory.ssikit.walt.id/v1/redoc)

The _Signatory API_ exposes the "issuance" endpoint, which provides flexible integration possibilities for anyone intending to act as an "Issuer" (i.e. create, sign and issue Verifiable Credentials), as follows:

* [Credentials](signatory-api.md#credentials) - issue credentials
* [Templates](signatory-api.md#templates) - create and mange credential templates
* [Revocations](signatory-api.md#revocations) - revocation related functions

## Credentials

If you're new to VCs, check out the [intro section](../../ssi-kit/ssi-kit/what-is-ssi/technologies-and-concepts/verifiable-credentials-vcs-and-verifiable-presentations-vps.md) for an overview.

The `/v1/credentials/issue` endpoint issues a specified credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://signatory.ssikit.walt.id/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "templateId": "string",
    "config":
    {
        "issuerDid": "string",
        "subjectDid": "string",
        "verifierDid": "string",
        "issuerVerificationMethod": "string",
        "proofType": "JWT",
        "domain": "string",
        "nonce": "string",
        "proofPurpose": "string",
        "credentialId": "string",
        "issueDate": "2022-10-06T18:09:14.570Z",
        "validDate": "2022-10-06T18:09:14.570Z",
        "expirationDate": "2022-10-06T18:09:14.570Z",
        "dataProviderIdentifier": "string",
        "ldSignatureType": "string",
        "creator": "string",
        "ecosystem": "string",
        "statusType": "string"
    },
    "credentialData":
    {
        "additionalProp1":
        {},
        "additionalProp2":
        {},
        "additionalProp3":
        {}
    }
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
The issued credential displayed either in JSON-LD or JWT format
```
{% endtab %}
{% endtabs %}

E.g. Issue a `UniversityDegree` credential in the default JSON-LD format. In case you don't have the DID for the Issuer and or the Holder, you can create one [here](custodian-api/#create-did).

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://signatory.ssikit.walt.id/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "templateId": "UniversityDegree",
    "config":
    {
        "issuerDid": "did:web:walt.id",
        "subjectDid": "did:web:my.domain"
    },
    "credentialData":
    {
        "credentialSubject":
        {
            "degree":
            {
                "name": "Bachelor of Science and Arts",
                "type": "BachelorDegree"
            }
        }
    }
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "templateId": "UniversityDegree",
    "config":
    {
        "issuerDid": "did:web:walt.id",
        "subjectDid": "did:web:my.domain"
    },
    "credentialData":
    {
        "credentialSubject":
        {
            "degree":
            {
                "name": "Bachelor of Science and Arts",
                "type": "BachelorDegree"
            }
        }
    }
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

\
Check out the [Issue with status](../../concepts/credential-statuses/issue-with-status.md) section to learn about how to issue a verifiable credential with a _credentialStatus_ property.

## Templates

The currently available template functions are:

* [list](signatory-api.md#list-templates) - display the list of Templates
* [import](signatory-api.md#import-template) - import a custom template
* [load](signatory-api.md#load-template) - display the content of the template having the specified `id`

### List templates

The `/v1/templates` endpoint returns the list of the available template `id`s

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://signatory.ssikit.walt.id/v1/templates' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
No parameter
{% endtab %}

{% tab title="Response body schema" %}
```
[
    "string"
]
```
{% endtab %}
{% endtabs %}

E.g. List the templates

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://signatory.ssikit.walt.id/v1/templates' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    "DataSelfDescription",
    "VerifiableDiploma",
    "VerifiableVaccinationCertificate",
    "LegalPerson",
    "VerifiableAuthorization",
    "Europass",
    "KybMonoCredential",
    "KycCredential",
    "VerifiableMandate",
    "VerifiablePresentation",
    "EuropeanBankIdentity",
    "KybCredential",
    "VerifiableAttestation",
    "OpenBadgeCredential",
    "PeerReview",
    "DataConsortium",
    "ProofOfResidence",
    "AmletCredential",
    "ParticipantCredential",
    "PermanentResidentCard",
    "UniversityDegree",
    "VerifiableId",
    "DataServiceOffering",
    "GaiaxCredential",
    "Iso27001Certificate"
]
```
{% endtab %}
{% endtabs %}

### Import template

The `/v1/templates/{id}` endpoint to import your custom credential template

* id path parameter (required) - `id` of the template, e.g. `MyCustomCredential`

{% tabs %}
{% tab title="curl" %}
```bash
curl -X 'POST' \
  'https://signatory.ssikit.walt.id/v1/templates/{id}' \
  -H 'accept: application/json'
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```json
{
  "type": [
    "VerifiableCredential",
    "MyCustomCredential"
  ],
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "string",
  "issuer": {
    "id": "string"
  },
  "issued": "2020-03-10T04:24:12.164Z",
  ... // custom data in json
}

```
{% endtab %}

{% tab title="Request body example" %}
```json
{
  "type": [
    "VerifiableCredential",
    "MyCustomCredential"
  ],
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.gov/credentials/3732",
  "issuer": {
    "id": "did:example:456"
  },
  "issued": "2020-03-10T04:24:12.164Z",
  "credentialSubject": {
    "id": "did:example:123",
    "firstName": "",
    "lastName": "",
    "country": "Austria"
  }
}

```
{% endtab %}

{% tab title="Response body schema" %}
```json
null
```
{% endtab %}
{% endtabs %}

### Load template

The `/v1/templates/{id}` endpoint displays the content of the template having the parameters:

* id path parameter (required) - `id` of the template

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://signatory.ssikit.walt.id/v1/templates/{id}' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Request body schema" %}
No parameter
{% endtab %}

{% tab title="Response body schema" %}
```
The template content as JSON
```
{% endtab %}
{% endtabs %}

E.g. Load the template for the `id` set to _UniversityDegree_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://signatory.ssikit.walt.id/v1/templates/UniversityDegree' \
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
        "id": "did:example:123"
    },
    "id": "http://example.gov/credentials/3732",
    "issued": "2020-03-10T04:24:12.164Z",
    "issuer":
    {
        "id": "did:example:456"
    },
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ]
}
```
{% endtab %}
{% endtabs %}

## Revocations

Refer to [Credential Statuses](../../concepts/credential-statuses/) section for more details on verifiable credential revocations.
