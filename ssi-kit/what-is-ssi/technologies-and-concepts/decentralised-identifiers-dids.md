---
description: >-
  DIDs give us the power of verifying information, for example credentials,
  anywhere, anytime, through the establishment of a public key infrastructure.
---

# Decentralised Identifiers (DIDs)

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
