# Revoke a verifiable credential

Revoking a verifiable credential can be done using the command-line interface with the
following command:

```shell
ssikit.sh vc revocation revoke <vc-filepath>
```

where _<vc-filepath>_ is the path to the verifiable credential to be checked.

e.g. Verifiable Credential - vc.json

```json
{
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
  "credentialStatus":
  {
    "id": "http://127.0.0.1:7001/v1/credentials/status/revocation#6",
    "statusListCredential": "http://127.0.0.1:7001/v1/credentials/status/revocation",
    "statusListIndex": "6",
    "statusPurpose": "revocation",
    "type": "StatusList2021Entry"
  },
  "proof":
  {
    "type": "JsonWebSignature2020",
    "creator": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
    "created": "2023-04-28T09:50:02Z",
    "verificationMethod": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK#z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
    "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9.._ed-3UyXh-Km9xanh0H2J_HJr9WRIH0dyJg-uKXAz3cvQVk1WSeMv-QdApNvXuaMUKEvtBakVc5NzhcoBA9hBw"
  }
}
```

e.g. Revoke the credential
```shell
ssikit.sh vc revocation revoke vc.json
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