# Revoke a verifiable credential

Revoking a verifiable credential can be done using the command-line interface with the
following command:

```shell
ssikit vc revocation revoke {vc-filepath}
```

where _{vc-filepath}_ is the path to the verifiable credential to be checked.

e.g. Verifiable Credential - vc.json

```json
{
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
    "id": "http://127.0.0.1:7001/v1/credentials/status/revocation#12",
    "statusListCredential": "http://127.0.0.1:7001/v1/credentials/status/revocation",
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
}
```

e.g. Revoke the credential
```shell
ssikit vc revocation revoke vc.json
```

e.g. Revocation result

{% tabs %}
{% tab title="Success" %}
```text
Revoking credential stored at: vc.json
Revocation result:
{
    "message" : "",
    "succeed" : true
}
```
{% endtab %}
{% tab title="Failure" %}
```text
Revoking credential stored at: vc-missing-status.json
Revocation result:
{
    "message" : "Verifiable credential has no credential-status property",
    "succeed" : false
}
```
{% endtab %}
{% endtabs %}