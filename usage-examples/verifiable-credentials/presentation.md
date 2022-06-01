# Presentation

The following CLI commands shows the creation of a W3C Verifiable Presentation.

```
./ssikit.sh vc present --holder-did did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3 vc.json

Creating a verifiable presentation for DID "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3"...
Using 1 VC:
- 1. vc.json (VerifiableId)

Results:

Verifiable presentation generated for holder DID: "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3"
Verifiable presentation document (below, JSON):

{
  "@context" : [ "https://www.w3.org/2018/credentials/v1" ],
  "holder" : "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3",
  "id" : "urn:uuid:b120968f-5cba-4276-aa88-fff1256f837d",
  "type" : [ "VerifiablePresentation" ],
  "verifiableCredential" : [ {
    "@context" : [ "https://www.w3.org/2018/credentials/v1" ],
    "credentialSchema" : {
      "id" : "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
      "type" : "FullJsonSchemaValidator2021"
    },
    "credentialSubject" : {
      "currentAddress" : [ "1 Boulevard de la Liberté, 59800 Lille" ],
      "dateOfBirth" : "1993-04-08",
      "familyName" : "DOE",
      "firstName" : "Jane",
      "gender" : "FEMALE",
      "id" : "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3",
      "nameAndFamilyNameAtBirth" : "Jane DOE",
      "personalIdentifier" : "0904008084H",
      "placeOfBirth" : "LILLE, FRANCE"
    },
    "evidence" : [ {
      "documentPresence" : [ "Physical" ],
      "evidenceDocument" : [ "Passport" ],
      "subjectPresence" : "Physical",
      "type" : [ "DocumentVerification" ],
      "verifier" : "did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
    } ],
    "id" : "urn:uuid:6ef38d73-d23d-434c-93c4-264763873726",
    "issued" : "2022-06-01T07:03:00.131603314Z",
    "issuer" : "did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w",
    "proof" : {
      "created" : "2022-06-01T07:03:00Z",
      "creator" : "did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w",
      "domain" : "https://api.preprod.ebsi.eu",
      "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFUzI1NksifQ..RirH_lcUtMrcqOU59j372xDoTRib8rZdkTUVT2Ma0WkqRsecmXxBK5SUqNbZoGPIpfRoV4y6nf_gp5JBiSC7KQ",
      "nonce" : "bc1f5b6a-1fe2-40cb-9005-86a53d8f2f5c",
      "proofPurpose" : "assertion",
      "type" : "EcdsaSecp256k1Signature2019"
    },
    "validFrom" : "2022-06-01T07:03:00.131604945Z",
    "issuanceDate" : "2022-06-01T07:03:00.131604945Z",
    "type" : [ "VerifiableCredential", "VerifiableAttestation", "VerifiableId" ]
  } ],
  "proof" : {
    "type" : "Ed25519Signature2018",
    "creator" : "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3",
    "created" : "2022-06-01T07:08:32Z",
    "domain" : "https://api.preprod.ebsi.eu",
    "nonce" : "a7b2abe3-08b1-44f8-aa4c-191d74e243df",
    "proofPurpose" : "authentication",
    "verificationMethod" : "did:key:z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3#z6MkpDKnofSJ2DCc3gJpsHnviQ6i41Uyyegk6AmAdZHkbxU3",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..ViE0kEDYQEfX-4W_0g--rs8CyaNFxj_PXpRFH5sutCQRepylaU_RdNQHguOz9Ut41eTMEzi__s46FzpGAq_pAQ"
  }
}

```

An example will be added shortly. If you have any questions, please feel free to [reach out](../../contact-and-developer-relations/contact.md).
