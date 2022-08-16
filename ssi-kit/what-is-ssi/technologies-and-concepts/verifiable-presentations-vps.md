# Verifiable Presentations (VPs)

A Verifiable Presentation (VP) is a collection from one or more Verifiable Credentials, whereas the authorship of the whole collection can be cryptographically verified. VPs are standardized as part of the [W3C Verifiable Credentials Data Model](https://www.w3.org/TR/vc-data-model/#presentations).

## Why do we need Verifiable Presentations?

Verifiable Credentials introduced credentials which are tamper-evident, easy to verify and privacy preserving by design. Verifiable Presentations make sure to take the idea of privacy even a step further, by giving us a way to only reveal the required data to make a transaction work with a service/product provider (verifier). Therefore, Alice can share in a Verifiable Presentation only her name and address with an e-commerce shop, so they can send her the package, but she doesn't have to share her birthday and other information present in her digital ID (Verifiable Credential).

Another great benefit of Verifiable Presentations is, that they can compress multiple Verifiable Credentials into one verifiable document. Thereby, eliminating the need for different flows and multiple transactions. For example, a service provider could require a proof of employment, the address and a bank statement from Bob to give him access to the service. To provide this information, Bob might need to share multiple Verifiable Credentials, as none of them holds all the data. With the Verifiable Presentation, the data could be gathered from multiple Verifiable Credentials in your wallet and be composed into one shareable and verifiable document.



## How Verifiable Presentations are composed?

**Verifiable Presentations** represent a composition of claims, which can come from one or multiple Verifiable Credentials, of which the authorship is verified. This **gives the holder of credentials the chance of composing context specify presentations**, which only contain the data which is relevant in that context. When presenting the composition to a verifier, it can easily be validated.

Taking a closer look at how they are built up. We will see four different layers:

1. **Presentation Layer  -**  Being the Verifiable Presentation itself with the required metadata
2. **Credential Layer -** Referenced by Layer 1 and pointing to one or more credentials
3. **Credential Proof Layer -** Holding the proofs of the credentials and the signatures from Layer
4. **Presentation Proof Layer -** Holding the proof of the Verifiable Presentation and its signatures

![](<../../../.gitbook/assets/Verifiable Presentation Overview (1).jpg>)

### Example of a Verifiable Presentation in code

If you want to get a better understanding of the different attributes present, please visit our section about [VCs](https://docs.walt.id/v/idpkit/concepts/identity-provision-via-nfts#nft\_token-scope).

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
Our open source products enable you to act as a Holder (share VPs) and as a Verifier (request verify VPs).
{% endhint %}
