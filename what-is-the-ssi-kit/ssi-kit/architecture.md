# Architecture

## Technology Stack

[Severin Stampler](https://app.gitbook.com/u/QbVrGMSggtaXNsjpphAURnvy9dB2 "mention")

Add:

* Frameworks
* Libraries
* Languages

## Overview

The SSI Kit’s architecture is split in three abstraction layers:

1. **Low-Level Services**: Abstracts cryptographic and core SSI operations.
2. **Ecosystems**: Abstracts ecosystem-specific operations and business logic.
3. **High-Level Interfaces / APIs**: Provides high-level interfaces that hide complexity and facilitate usage.

Also, our architecture allows for the integration of third-party solutions throughout the stack, e.g.:

* Key storage (e.g. HSM, WebKMS)
* Data storage (e.g. identity hubs, confidential storage)
* Registries (e.g. blockchains, DNS)

This architectural openness prevents vendor lock-in and allows developers to build SSI-based solutions that meet their unique requirements.

_Illustration:_

![The blue boxes symbolise our products and their interfaces. The green boxes symbolise third party solutions that can be integrated via open APIs to avoid rip-and-replace and extend functionality to meet diverse customer requirements.](../../what-is-ssikit/ssi-kit/Architecture-SSIKit-by-waltid.png)

### Low-Level Service Abstraction

[phil](https://app.gitbook.com/u/Xy5PETDzUVT9yjUrLtjs53z9wvW2 "mention") **Please explain core services! \[TO BE DONE]**

#### Key Interfaces

Handles keys and cryptographic operations like the generation of signatures (e.g. linked data, JWT) with signature types such as ES256K or EdDSA.

Keys can be stored in a file and database keystore, which is extendable to HSMs and WebKMS.

#### DID Interfaces

Abstracts common functionality related to Decentralised Identifiers (DIDs, DID Documents) for methods like “did:web”, “did:key”, “did:ebsi”.

#### Credential Interfaces

Abstracts common functionality related to Verifiable Credentials (VCs) and Verifiable Presentations (VPs) in different formats like JSON and JSON-LD.

### Ecosystem Abstraction

We believe in a multi-ecosystem future. This is why we built a layer that abstracts ecosystem-specific operations and business logic so that developers can use our solutions to participate in different ecosystems without having to switch between different technical implementations. The idea is to support any ecosystem with a single solution that does not put any additional burden on developers.

We currently support:

* EBSI/ESSIF (EU's new decentralized identity ecosystem)
* Gaia-X (EU's new cloud infrastructure)
* Velocity Network
* ...

Other selected ecosystems will be added over time.

### High-Level Interfaces / APIs

The SSI Kit exposes high-level APIs that hide complex low-level crypto and SSI operations as well as different flavours of SSI introduced by different ecosystems.

Developers and implementers can simply call the same generic and robust interfaces they know even if new low-level services are added or new ecosystems supported.

[phil](https://app.gitbook.com/u/Xy5PETDzUVT9yjUrLtjs53z9wvW2 "mention") **Please explain high level core services! \[TO BE DONE]**

