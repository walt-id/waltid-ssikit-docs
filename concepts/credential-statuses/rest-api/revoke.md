# Revoke a verifiable credential

Revoking a verifiable credential can be done using the REST API interface by supplying the
credential as the body to the following `POST` request `<ssikit-host>/v1/revocations/revoke`.

e.g. Execute the status check for a credential with a _credentialStatus_ property

{% tabs %}
{% tab title="Request" %}
```shell
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/revocations/revoke' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "type":
    [
        "VerifiableCredential",
        "VerifiableAttestation",
        "VerifiableId"
    ],
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
    ],
    "id": "urn:uuid:f85f6758-8de4-4c4c-8a08-a7d4ed3574fb",
    "issuer": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
    "issuanceDate": "2023-04-28T10:15:16Z",
    "issued": "2023-04-28T10:15:16Z",
    "validFrom": "2023-04-28T10:15:16Z",
    "credentialSchema":
    {
        "id": "https://raw.githubusercontent.com/walt-id/waltid-ssikit-vclib/master/src/test/resources/schemas/VerifiableId.json",
        "type": "FullJsonSchemaValidator2021"
    },
    "credentialSubject":
    {
        "id": "did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X",
        "currentAddress":
        [
            "1 Boulevard de la Liberté, 59800 Lille"
        ],
        "dateOfBirth": "1993-04-08",
        "familyName": "DOE",
        "firstName": "John",
        "gender": "MALE",
        "nameAndFamilyNameAtBirth": "John DOE",
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
    "credentialStatus":
    {
        "id": "http://127.0.0.1:7001/v1/credentials/status/revocation#7",
        "statusListCredential": "http://127.0.0.1:7001/v1/credentials/status/revocation",
        "statusListIndex": "7",
        "statusPurpose": "revocation",
        "type": "StatusList2021Entry"
    },
    "proof":
    {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "created": "2023-04-28T10:15:16Z",
        "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..PBOY-LMZ1zX4WlNBRbrjJ5JC8rrP9ZJJatjcDe72_pIIP7ggbSr1pMx9PMJKwKyLIt0-M0VF3pCZssVs_Sa8AA"
    }
}'
```
{% endtab %}
{% tab title="Revocation result" %}
Http.Code = 200
{% endtab %}
{% endtabs %}

e.g. Execute the status check for a credential without a _credentialStatus_ property

{% tabs %}
{% tab title="Request" %}
```shell
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/revocations/revoke' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "type":
    [
        "VerifiableCredential",
        "VerifiableAttestation",
        "VerifiableId"
    ],
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
    ],
    "id": "urn:uuid:0decd79e-362e-4587-8fe9-ed058435dfb4",
    "issuer": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
    "issuanceDate": "2023-04-28T10:28:20Z",
    "issued": "2023-04-28T10:28:20Z",
    "validFrom": "2023-04-28T10:28:20Z",
    "credentialSchema":
    {
        "id": "https://raw.githubusercontent.com/walt-id/waltid-ssikit-vclib/master/src/test/resources/schemas/VerifiableId.json",
        "type": "FullJsonSchemaValidator2021"
    },
    "credentialSubject":
    {
        "id": "did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X",
        "currentAddress":
        [
            "1 Boulevard de la Liberté, 59800 Lille"
        ],
        "dateOfBirth": "1993-04-08",
        "familyName": "DOE",
        "firstName": "John",
        "gender": "MALE",
        "nameAndFamilyNameAtBirth": "John DOE",
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
    "proof":
    {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "created": "2023-04-28T10:28:20Z",
        "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..lypagZfI0-fLjUMMpvXjzJOe0L0J3yivnHsXAVswRJ4quDiGILP1yu5Djy2kFwyVABNKN6XLhZ4IJBR1jnzIAQ"
    }
}'
```
{% endtab %}
{% tab title="Revocation result" %}
Http.Code = 404
```json
"Verifiable credential has no credential-status property"
```
{% endtab %}
{% endtabs %}