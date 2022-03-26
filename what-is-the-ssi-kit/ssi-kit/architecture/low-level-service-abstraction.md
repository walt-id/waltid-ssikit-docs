# Low-Level Service Abstraction

This software-layer holds a set of generic core services for common SSI and cryptographic functions. The services are in the scope of cryptography, key management, digital signatures, data storage, decentralized identifierers and verifiable credentials. The common interfaces are designed that these functions can be conveniently used by components sitting in higher layers of the software stack.

The low-level services are can be unitized directly via the Kotlin/Java classes or via the REST API ( [Swagger doc of the core API](https://core.ssikit.walt.id/v1/swagger))

The following is a short summary of the interfaces available. The detailed functions are described in the further sections of the documentation.

### Key Interfaces

Handles keys and cryptographic operations like the generation of signatures (e.g. linked data, JWT) with signature types such as ES256K or EdDSA.

Keys can be stored in a file and database keystore, which is extendable to HSMs and WebKMS.

### DID Interfaces

Abstracts common functionality related to Decentralised Identifiers (DIDs, DID Documents) for methods like “did:web”, “did:key”, “did:ebsi”.

### Credential Interfaces

Abstracts common functionality related to Verifiable Credentials (VCs) and Verifiable Presentations (VPs) in different formats like JSON and JSON-LD.

##
