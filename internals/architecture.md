# Architecture

The SSI Kit’s architecture is split in three layers:
- Low-Level Service Abstraction Layer: Abstracts low-level cryptographic and SSI-related functionality.
- Ecosystem Abstraction Layer: Abstracts ecosystem-specific operations and business logic.
- Interface / API Layer: Provides high-level interfaces that hide complexity and facilitates the use for developers and implementers.

Furthermore, our architecture allows for the integration of third-party solutions such as:

- Key Stores (HSM, WebKMS)
- Identity Hubs
- Trust Registries

This architectural openness prevents vendor lock-in and allows developers and organisations to build SSI-based solutions that meet their unique requirements.

_Illustration:_

![](./Architecture-SSIKit-by-waltid.png)

_The blue boxes symbolise our products and their interfaces. The green boxes symbolise third party solutions that can be integrated via open APIs to avoid rip-and-replace and extend functionality to meet diverse customer requirements._


## Low-Level Service Abstraction
### Key API

Handles keys and cryptographic operations like the generation of signatures (e.g. linked data, JWT) with signature types such as ES256K or EdDSA.

Keys can be stored in a file and database keystore, which is extendable to HSMs  and WebKMS.

### DID API

Abstracts common functionality related to Decentralised Identifiers (DIDs, DID Documents) for methods like  “did:web”, “did:key”, “did:ebsi”.

### Credential API

Abstracts common functionality related to Verifiable Credentials (VCs) and Verifiable Presentations (VPs) in different formats like JSON and JSON-LD.

## Ecosystem Abstraction

We believe that multiple identity ecosystems will exist in the future. This is why we built a layer that abstracts ecosystem-specific operations and business logic so that developers and organisations can use our solutions to participate in multiple ecosystems without having to switch between different technical implementations. The idea is to support various ecosystems with a single solution that does not put any additional burden on developers.  
We currently support:
- European Digital Identity Ecosystem based on the EU Blockchain Service Infrastructure (EBSI) and the EU Self-Sovereign Identity Framework (ESSIF).
- Hyperledger Aries based ecosystems

Other selected ecosystems will be added over time.

Read more about identity ecosystems [here](https://docs.walt.id/ecosystems/)

## Interfaces & APIs
The SSI Kit exposes high-level APIs that hide complex low-level crypto and SSI operations as well as different flavors of SSI introduced by different ecosystems. Developers and implementers can simply call the same generic and robust interfaces they know even if new low-level services are added or new ecosystems supported.
