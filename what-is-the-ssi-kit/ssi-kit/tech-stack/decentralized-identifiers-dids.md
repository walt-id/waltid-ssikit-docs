# Decentralized Identifiers (DIDs)

## Overview

DIDs are unique identifiers (URIs) which are globally standardised by the [W3C](https://www.w3.org/TR/did-core). They are usually linked to so-called "DID Documents" which contain not only DIDs, but also metadata like keys or service endpoints.

DIDs are important because they establish a (Distributed) Public Key Infrastructure (D/PKI) by linking keys to unique identifiers that allow different parties to find and interact with each other (discovery), authenticate, encrypt and verifiably sign data.

Today, a variety of so-called “DID methods'', i.e. different implementations of the DID specification, exist. Considering that each DID method differs in terms of how it is created, registered and resolved, different methods come with different advantages and disadvantages. For example, while DIDs are traditionally anchored on registries, like blockchains (e.g. did:ebsi) or DNS (e.g. did:web), new methods emerged that do not require such registries because their distribution mechanism is based on peer-to-peer interactions (e.g. did:key).

As example the identifier did:ebsi:2A9RkiYZJsBHT1nSB3HZAwYMNfgM7Psveyodxrr8KgFvGD5y of the method **did:ebsi** would resolve to the following DID document:

```
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

## Our Implementations

Our open source solutions enable you to use different DID methods for different identity ecosystems. Every relevant functionality is supported from the generation of DIDs and DID Documents to anchoring or resolving them on/from Registries.

We are currently supporting the following DID methods:

* did:ebsi
* did:web
* did:key

_Note that we are continuously adding support for new DID methods._
