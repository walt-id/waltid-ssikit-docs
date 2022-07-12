# Verifiable Credentials (VCs)

Verifiable Credentials (VCs) are **digital credentials** that **contain actual identity data** of people or organizations and are standardized by the [W3C](https://www.w3.org/TR/vc-data-model/). They are **digital equivalents of paper-based identity documents** like passports or diplomas.



**VCs are** **created and signed by “Issuers”**, the data sources within an SSI ecosystem. Issuers are typically organizations (e.g. governments, universities, banks) who provide people (or other organizations) with VCs that prove identity-related attributes.

For example, a university acts as an Issuer, if it issues diplomas (VCs) to its graduates.

VCs typically contain at least:

* the Issuer’s DID
* the recipient’s DID (also called “Holder”)
* information about the VC’s validity (e.g. expiration date, references to revocation mechanisms)
* the recipient’s identity attributes (e.g. name, age, address, …)
* the signature of Issuer (also called “proof”) other information (e.g. semantic contexts, issuance date, evidence related to the issuance process, references to external VC data models/templates)

Here is an illustrative **example of a Verifiable Credential (VCs)**:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://essif.europa.eu/schemas/v-a/2020/v1",
    "https://essif.europa.eu/schemas/eidas/2020/v1"
  ],
  "id": "education#higherEducation#3fea53a4-0432-4910-ac9c-69ah8da3c37f",
  "type": [
    "VerifiableCredential",
    "VerifiableAttestation"
  ],
  "issuer": "did:ebsi:2757945549477fc571663bee12042873fe555b674bd294a3",
  "issuanceDate": "2019-06-22T14:11:44Z",
  "validFrom": "2019-06-22T14:11:44Z",
  "credentialSubject": {
    "id": "id111"
  },
  "credentialStatus": {
    "id": "https://essif.europa.eu/status/identity#verifiableID#1dee355d-0432-4910-ac9c-70d89e8d674e",
    "type": "CredentialStatusList2020"
  },
  "credentialSchema": {
    "id": "https://essif.europa.eu/tsr-vid/verifiableid1.json",
    "type": "JsonSchemaValidator2018"
  },
  "evidence": [
    {
      "id": "https://essif.europa.eu/tsr-va/evidence/f2aeec97-fc0d-42bf-8ca7-0548192d5678",
      "type": [
        "DocumentVerification"
      ],
      "verifier": "did:ebsi:2962fb784df61baa267c8132497539f8c674b37c1244a7a",
      "evidenceDocument": "Passport",
      "subjectPresence": "Physical",
      "documentPresence": "Physical"
    }
  ],
  "proof": {
    "type": "EidasSeal2021",
    "created": "2019-06-22T14:11:44Z",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "did:ebsi:2757945549477fc571663bee12042873fe555b674bd294a3#2368332668",
    "jws": "HG21J4fdlnBvBA+y6D...amP7O="
  }
}
```

{% hint style="info" %}
Our open source products enable you to act as an "Issuer" (create and issue VCs), as a Holder (manage and share VCs/VPs) and as a Verifier (request and verify VCs/VPs).
{% endhint %}
