# Check the status of a verifiable credential

Checking the status of a verifiable credential can be done using the REST API interface by supplying the
credential as the body to the following `POST` request `{signatory.ssikithost}/v1/revocations/check`. 

e.g. Execute the status check for a credential with a _credentialStatus_ property

{% tabs %}
{% tab title="Request" %}
```shell
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/revocations/check' \
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
    "id": "urn:uuid:07f73ca8-6277-4335-a3ec-05152c16b841",
    "issuer": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
    "issuanceDate": "2023-04-28T09:50:00Z",
    "issued": "2023-04-28T09:50:00Z",
    "validFrom": "2023-04-28T09:50:00Z",
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
        "firstName": "Jane",
        "gender": "FEMALE",
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
    "proof":
    {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "created": "2023-04-28T09:50:02Z",
        "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9.._ed-3UyXh-Km9xanh0H2J_HJr9WRIH0dyJg-uKXAz3cvQVk1WSeMv-QdApNvXuaMUKEvtBakVc5NzhcoBA9hBw"
    }
}'
```
{% endtab %}
{% tab title="Status result" %}
```json
{
  "isRevoked": false
}
```
{% endtab %}
{% endtabs %}

e.g. Execute the status check for a credential without a _credentialStatus_ property

{% tabs %}
{% tab title="Request" %}
```shell
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/revocations/check' \
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
{% tab title="Status result" %}
```json
"Verifiable credential has no credential-status property"
```
{% endtab %}
{% endtabs %}