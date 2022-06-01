# Issuance

The following CLI commands shows the creation of a W3C Verifiable Credential.

```
./ssikit.sh vc issue --template VerifiableId --issuer-did did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w --subject-did did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd

Issuing a verifiable credential (using template VerifiableId)...

Results:

Issuer "did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w"
⇓ issued a "VerifiableId" to ⇓
Holder "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd"

Credential document (below, JSON):

{
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
    "id" : "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd",
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
  "id" : "urn:uuid:6bb34c92-b08b-4067-822e-4fcd4372a928",
  "issued" : "2022-06-01T07:00:28.954610431Z",
  "issuer" : "did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w",
  "validFrom" : "2022-06-01T07:00:28.954612224Z",
  "issuanceDate" : "2022-06-01T07:00:28.954612224Z",
  "type" : [ "VerifiableCredential", "VerifiableAttestation", "VerifiableId" ],
  "proof" : {
    "type" : "EcdsaSecp256k1Signature2019",
    "creator" : "did:ebsi:zvXXbgxmw6xzeQqQdvD3N2w",
    "created" : "2022-06-01T07:00:29Z",
    "domain" : "https://api.preprod.ebsi.eu",
    "nonce" : "80dc7eb1-8413-4bd7-8c3f-3f0d3e5bec7f",
    "proofPurpose" : "assertion",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFUzI1NksifQ..zivyo9W5bNmRZNEByR959RYnQbdvZhZOzdwenWmdiS7sDx_7Sa_qlGkchsn8JWUjE7CjNePSVzjTxLUHnn_Lcw"
  }
}

```

More examples will be added shortly. If you have any questions, please feel free to [reach out](../../contact-and-developer-relations/contact.md).
