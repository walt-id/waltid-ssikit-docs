# Low-Level Service Abstraction

[phil](https://app.gitbook.com/u/Xy5PETDzUVT9yjUrLtjs53z9wvW2 "mention") **Please explain core services! \[TO BE DONE]**

### Key Interfaces

Handles keys and cryptographic operations like the generation of signatures (e.g. linked data, JWT) with signature types such as ES256K or EdDSA.

Keys can be stored in a file and database keystore, which is extendable to HSMs and WebKMS.

### DID Interfaces

Abstracts common functionality related to Decentralised Identifiers (DIDs, DID Documents) for methods like “did:web”, “did:key”, “did:ebsi”.

### Credential Interfaces

Abstracts common functionality related to Verifiable Credentials (VCs) and Verifiable Presentations (VPs) in different formats like JSON and JSON-LD.

##
