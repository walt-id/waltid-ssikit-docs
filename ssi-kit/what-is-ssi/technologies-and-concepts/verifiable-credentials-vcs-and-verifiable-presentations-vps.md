# Verifiable Credentials (VCs) & Verifiable Presentations (VPs)

Verifiable Credentials (VCs) and Verifiable Presentations (VPs) are digital credentials that **contain actual identity data** of people or organizations and are standardized by the W3C. They are digital equivalents of paper-based identity documents like passports or diplomas.

#### Verifiable Credentials

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

#### **Verifiable Presentations (VPs)**

**VPs** are composed and signed by “Holders”. They can **contain identity information from one or multiple VCs** and are created for the purpose of presenting them to a “Verifier”. In other words, VPs are the format with which the contents of VCs are shared by the person or organization that is described by the VCs.

For example, a graduate presents a VP to an employer that contains information from her digital passport and diplomas.&#x20;

VPs typically contain at least:

* VCs or parts of VCs (individual attributes)
* the recipient’s signature (to ensure so-called “Holder binding”)

Here is an illustrative **example of a Verifiable Presentation**:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1"
  ],
  "type": [
    "VerifiableCredential",
    "VerifiablePresentation"
  ],
  "verifiableCredential": [
    {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://essif.europa.eu/schemas/vc/2020/v1"
      ],
      "credentialSubject": {
        "id": "did:ebsi:00000004321",
        "naturalPerson": {
          "did": "did:example:00001111"
        }
      },
      "id": "did:ebsi-eth:00000001/credentials/1872",
      "issuanceDate": "2020-08-24T14:13:44Z",
      "issuer": "did:ebsi:000001234",
      "proof": {
        "created": "2020-08-24T14:13:44Z",
        "jws": "eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19.",
        "proofPurpose": "assertionMethod",
        "type": "EcdsaSecp256k1Signature2019",
        "verificationMethod": "did:ebsi-eth:000001234#key-1"
      },
      "type": [
        "VerifiableCredential",
        "VerifiableAuthorization"
      ]
    },
    {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/citizenship/v1"
      ],
      "credentialSubject": {
        "birthDate": "1958-08-17",
        "givenName": "JOHN",
        "id": "did:example:123",
        "type": [
          "PermanentResident",
          "Person"
        ]
      },
      "issuer": "did:example:456",
      "proof": {
        "created": "2020-04-22T10:37:22Z",
        "jws": "eyJjcml0IjpbImI2NCJdLCJiNjQiOmZhbHNlLCJhbGciOiJFZERTQSJ9..BhWew0x-txcroGjgdtK-yBCqoetg9DD9SgV4245TmXJi-PmqFzux6Cwaph0r-mbqzlE17yLebjfqbRT275U1AA",
        "proofPurpose": "assertionMethod",
        "type": "Ed25519Signature2018",
        "verificationMethod": "did:example:456#key-1"
      },
      "type": [
        "VerifiableCredential",
        "PermanentResidentCard"
      ]
    }
  ]
}
```

{% hint style="info" %}
Our open source products enable you to act as an "Issuer" (create and issue VCs), as a Holder (manage and share VCs/VPs) and as a Verifier (request and verify VCs/VPs).
{% endhint %}
