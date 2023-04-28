# Check the status of a verifiable credential

Checking the status of a verifiable credential can be done using the REST API interface by supplying the
credential as the body to the following `POST` request `https://signatory.ssikit.walt.id/v1/revocations/check`. 

e.g. Execute the status check for a credential with a _credentialStatus_ property

{% tabs %}
{% tab title="Request" %}
```shell
curl -X 'POST' \
  'https://signatory.ssikit.walt.id/v1/revocations/check' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ],
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
    ],
    "id": "urn:uuid:3c89d819-49b0-41b0-a5c3-4386eb0cddbf",
    "issuer":
    {
        "id": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK"
    },
    "issuanceDate": "2023-04-28T15:35:36Z",
    "issued": "2023-04-28T15:35:36Z",
    "validFrom": "2023-04-28T15:35:36Z",
    "credentialSubject":
    {
        "id": "did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X",
        "degree":
        {
            "name": "Bachelor of Science and Arts",
            "type": "BachelorDegree"
        }
    },
    "credentialStatus":
    {
        "id": "https://signatory.ssikit.walt.id/v1/credentials/status/revocation#12",
        "statusListCredential": "https://signatory.ssikit.walt.id/v1/credentials/status/revocation",
        "statusListIndex": "12",
        "statusPurpose": "revocation",
        "type": "StatusList2021Entry"
    },
    "proof":
    {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "created": "2023-04-28T15:35:38Z",
        "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Im6fYtggnBdooYMj0SNUEEZ6OGLfj7OHW6ZBaOusOR4HL6AqRdK7Sbm9vya8H_g6XQR8aeH1VXM5OTh5_P-eAA"
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
  'https://signatory.ssikit.walt.id/v1/revocations/check' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ],
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
    ],
    "id": "urn:uuid:22eefe7d-8467-46dc-9036-29d2d7597829",
    "issuer":
    {
        "id": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK"
    },
    "issuanceDate": "2023-04-28T15:42:31Z",
    "issued": "2023-04-28T15:42:31Z",
    "validFrom": "2023-04-28T15:42:31Z",
    "credentialSubject":
    {
        "id": "did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X",
        "degree":
        {
            "name": "Bachelor of Science and Arts",
            "type": "BachelorDegree"
        }
    },
    "proof":
    {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "created": "2023-04-28T15:42:31Z",
        "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..HDFwEbkhGCOUGUUYikbf-NfSokResd2vz1YGfJ_MpWb_Z0vqjJO4EGjw2FFtmpTOn66bFV_n4Y0aRKvaVkIvBg"
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