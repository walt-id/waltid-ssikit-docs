---
description: Learn about the technology stack.
---

# SSI Flavours & Ecosystems

The SSI Kit abstracts complexity for developers by following a "multi-stack approach" that enables you to use different implementations or "flavours" of SSI. As a result, you can participate in different identity ecosystems (e.g. EBSI/ESSIF, Gaia-X, Velocity Network) and avoid technology-related lock-in effects.&#x20;

Based on our [Introduction to Self-Sovereign Identity (SSI)](../what-is-ssi/), we distinguish the following concepts or building blocks: &#x20;

![Each building block is available in different variations and can be put together in different ways. The result: different "SSI flavours".](<../../.gitbook/assets/Screenshot 2022-03-16 at 13.16.32 (1).png>)

## **Registries**&#x20;

Our products are agnostic towards the underlying technologies used to implement Registries, which means that the SSI Kit is potentially compatible with any type of Registry.

The SSI Kit supports:

* Permissionless Blockchains (e.g. Ethereum),
* Permissioned Blockchains (e.g. Ethereum Enterprise/Hyperledger Besu),
* Domain Name Service (DNS),
* Pure peer-to-peer approaches that do not require Registries.

_Note that we are continuously adding support for new Registries and underlying technologies._

&#x20;**** You can learn more about Registries [here](../what-is-ssi/technologies-and-concepts.md).

## **Cryptographic keys**

Keys convey control over digital identities and enable core functionality such as encryption and authentication.

The SSI Kit supports:

* ed25519
* secp256k1
* RSA

_Note that we are continuously adding support for new key types._

You can learn more about keys [here](../what-is-ssi/technologies-and-concepts.md).

## **Decentralized Identifiers (DIDs)**

Decentralized Identifiers (DIDs) establish a public key infrastructure by linking keys to unique identifiers that allow different parties to find and interact with each other.

The SSI Kit supports:

* did:ebsi
* did:web
* did:key

_Note that we are continuously adding support for new DID methods._

You can find more about DIDs [here](../what-is-ssi/technologies-and-concepts.md).

## **Verifiable Credentials** **(VCs)**

Verifiable Credentials (VCs) are digital identity documents that can easily and securely be shared with and verified (incl. validity, integrity, authenticity, provenance) by anyone in a privacy preserving way. Importantly, they are never (!) stored on a blockchain due to privacy and compliance reasons.

The SSI Kit supports W3C Verifiable Credentials in different formats:

* JSON / JWT
* JSON-LD

_Note that we are continuously adding support for new VC types and formats._

You can learn more about VCs [here](../what-is-ssi/technologies-and-concepts.md).

## **Data Exchange Protocols**

Authentication and data exchange protocols (e.g. OIDC/SIOP) enable the exchange of data (VCs) between different parties.

The SSI Kit supports latest OpenID Connect extension for SSI:

* OpenID Connect for Credential Issuance (OIDC4CI)
* OpenID Connect for Verifiable Presentations (OIDC4VP)

You can learn more about protocols [here](../what-is-ssi/technologies-and-concepts.md).
