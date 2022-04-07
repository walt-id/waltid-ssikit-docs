---
description: Learn about the technologies and concepts on which SSI is based.
---

# Technologies & Concepts

Understanding SSI requires the understanding of a few core concepts:

* **Registries**, which serve as a shared and trusted record of certain information. In other words, they serve as a “layer of trust” and a “single source of truth”.
* **Cryptographic keys**, which convey control over digital identities and enable core functionality such as encryption and authentication.
* **Decentralized Identifiers (DIDs)**, which establish a public key infrastructure by linking keys to unique identifiers that allow different parties to find and interact with each other.
* **Verifiable Credentials** **(VCs)** which are digital identity documents that can easily and securely be shared with and verified (incl. validity, integrity, authenticity, provenance) by anyone in a privacy preserving way. Importantly, they are never (!) stored on a blockchain due to privacy and compliance reasons.
* **Protocols** enable the exchange of data (VCs) between different parties.&#x20;
* **Wallets**, which store our keys (control) and VCs (identity data) and enable the management and sharing of our digital identities and data via easy-to-use applications.

The following graphic shows the SSI tech stack:

![](<../../.gitbook/assets/Screenshot 2022-03-16 at 13.16.32 (1).png>)

The following graphic shows how SSI works and highlights the core concepts (in blue):



![](https://images.squarespace-cdn.com/content/v1/609c0ddf94bcc0278a7cbdb4/6276f3d0-2d29-4664-be03-65d555fb824c/Screenshot+2022-03-09+at+08.26.35.png?format=2500w)

Think of these core concepts as different building blocks that are available in different variations and can be put together in different ways:

![Different technologies can be used to establish Trust Registries like blockchains (EBSI, Ethereum) or the domain name service (DNS). SSI even works (for certain use cases) without any Trust Registries but purely on a peer-to-peer basis. Similarly different types of DIDs, keys, proofs, credential formats,  authentication and data exchange protocols can be used.](https://images.squarespace-cdn.com/content/v1/609c0ddf94bcc0278a7cbdb4/1646980697410-HI3ESFOZM2HT5DZ12HG8/Screenshot+2022-03-10+at+09.34.37.png?format=1500w)

**As a result, there are** **different “flavours” of SSI** depending on which variations of which building blocks have been used and how they have been put together.

Importantly, the differences in terms of technologies that are being used illustrate why interoperability has always been one of the most important topics within the industry and why the development and use of open standards (e.g. by the W3C, Decentralized Identity Foundation, OpenID Foundation and others) are vital for technology and vendor selection.

## Deep Dive

The following section explains all concepts in more detail.

### Registries

Registries serve as a **single source of truth** in which all participants of an SSI ecosystem can trust. Depending on the ecosystem, registries make information accessible to anyone or just a limited group. Registries are important because they enable:

* **(Distributed) Public Key Infrastructures (DPKIs)** which establishes an open distribution system for public keys which can be used for encryption and authentication among others.
* **Trust Registries** which contain reliable information about people, organizations, things and even credentials (e.g. data models, status and validity information) to ensure that different parties can trust each other and the identity-related data they exchange.

Different technologies can be used to implement Registries. For example:

* **Blockchains** or **L1**: Typically blockchains are used because it is unfeasible (or even impossible) to tamper with them. The fact that no single organization can change the contents of a blockchain or manipulate the terms by which it is governed are very aligned with the requirements for identity ecosystems. Today, we see a growing number of developers and organizations focusing on so-called permissioned blockchains (i.e. only a selected group can “write”) like Ethereum Quorum/Enterprise. Permissionless blockchains, like Ethereum, are still used, but less than the permissioned alternatives for a variety of reasons like scalability, costs, lack of customisable governance frameworks.
* **L2**: Layer two networks sit on top of blockchains and aggregate data before anchoring it. The main idea behind them is to circumvent common challenges of public, permissionless blockchains like scalability and cost issues. The most popular implementations in the context of identity are “ION” (for Bitcoin) and “Element” (for Ethereum).
* **Other Distributed Ledger Technologies (DLTs)**: Sometimes other DLTs are utilised like the Interplanetary File System (IPFS) though its use for digital identity remains limited.
* **Domain Name Service (DNS)**: Considering certain drawbacks of DLTs and their relatively slow adoption by the mass market, DNS can also be used to serve as a registry. Though it is not fully decentralised (considering its underlying governance framework), DNS has many advantages like its maturity and global adoption.

Importantly, SSI can be implemented without registries, particularly without blockchains, because identity data (or at least personal data of individuals) is never anchored due to privacy and compliance reasons. However, by combining SSI with blockchains (or other technologies), robust and trustworthy identity ecosystems that utilise transparent DPKIs and reliable Trust Registries can emerge.

### Decentralised Identifiers (DIDs)

DIDs are **unique identifiers** (URIs) which are standardised by the [W3C](https://www.w3.org/TR/did-core). DIDs are typically linked to "DID Documents" which contain metadata like keys, service endpoints or proofs.

DIDs are important because they **establish a (distributed) public key infrastructure** (DPKI) and allow parties to find each other, authenticate and encrypt and verifiably sign data.

A variety of “**DID methods**'', which are different implementations of the DID specification, exist. Considering that DID methods differ in terms of how they are created, registered and resolved, different methods come with different advantages and disadvantages.&#x20;

For example, while DIDs are often anchored on Registries, such as EBSI (did:ebsi) or the Domain Name Service (did:web), new methods emerged that do not require Registries because their distribution is based on peer-to-peer interactions (e.g. did:key).

As example, the identifier _did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y_ of the method **did:ebsi** would resolve to the following DID document:

```json
{
    "@context": [
        "https://w3id.org/did/v1"
    ],
    "authentication": [
        "did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y#1a7514b2d58141c3982021a6323b99bf"
    ],
    "id": "did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y",
    "verificationMethod": [{
        "controller": "did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y",
        "id": "did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y#1a7514b2d58141c3982021a6323b99bf",
        "publicKeyJwk": {
            "alg": "EdDSA",
            "crv": "Ed25519",
            "kid": "1a7514b2d58141c3982021a6323b99bf",
            "kty": "OKP",
            "use": "sig",
            "x": "tqJADByHRU3YxswewQD4wQYXU9tB43j3PfjofsYEvqs"
        },
        "type": "Ed25519VerificationKey2018"
    }]
}
```

{% hint style="info" %}
Our open source products enable you to use different DID methods for different identity ecosystems. Every relevant functionality (e.g. generation, anchoring, resolution) is supported .
{% endhint %}

### Verifiable Credentials (VCs) & Verifiable Presentations (VPs)

Verifiable Credentials (VCs) and Verifiable Presentations (VPs) are digital credentials that **contain actual identity data** of people or organizations and are standardized by the W3C. They are digital equivalents of paper-based identity documents like passports or diplomas.

**VCs are** **created and signed by “Issuers”**, the data sources within an SSI ecosystem. Issuers are typically organizations (e.g. governments, universities, banks) who provide people (or other organizations) with VCs that prove identity-related attributes.

For example, a university acts as an Issuer, if it issues diplomas (VCs) to its graduates.

VCs typically contain at least:

* the Issuer’s DID
* the recipient’s DID (also called “Holder”)
* information about the VC’s validity (e.g. expiration date, references to revocation mechanisms)
* the recipient’s identity attributes (e.g. name, age, address, …)
* the signature of Issuer (also called “proof”) other information (e.g. semantic contexts, issuance date, evidence related to the issuance process, references to external VC data models/templates)

Here is an illustrative example of a VC:

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

**VPs** are composed and signed by “Holders”. They can **contain identity information from one or multiple VCs** and are created for the purpose of presenting them to a “Verifier”. In other words, VPs are the format with which the contents of VCs are shared by the person or organization that is described by the VCs.

For example, a graduate presents a VP to an employer that contains information from her digital passport and diplomas.&#x20;

VPs typically contain at least:

* VCs or parts of VCs (individual attributes)
* the recipient’s signature (to ensure so-called “Holder binding”)

Here is an illustrative example of a Verifiable Presentation:

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

### Data Exchange (Protocols)

Different authentication and data exchange protocols are used to **securely transfer identity data** (e.g. VCs, VPs) **between parties** (e.g. from an Issuer to a Holder). They typically establish a mutually authenticated and encrypted data channel between the communicating parties.

The most common data exchange protocols used for SSI are:

* OIDC4SSI / SIOP (Self-Issued OpenID Connect Provider): An extension of a mature authentication and authorization protocol called "OpenID Connect" (OIDC).
* DIDComm: A novel protocol specifically designed for SSI and maintained by the Decentralized Identity Foundation (DIF).
* Credential Handler API: A proposed browser-extension that may be used to connect the user's identity wallet to a web-application.

{% hint style="info" %}
Our solutions enable you to use different data exchange protocols like OIDC/SIOP as required by different ecosystems.
{% endhint %}

##

