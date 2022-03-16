---
description: Learn what the SSI Kit is.
---

# SSI Kit 101

## What is the SSI Kit?

The SSI Kit offers an **everything developers and organizations need to use Self-Sovereign Identity (SSI) with ease.**&#x20;

Here are the most important things to know about the SSI Kit:

* It is written in **Kotlin/Java**. **** It can be directly integrated (Maven/Gradle dependency) or run as RESTful web-service. A CLI tool allows running all included functions manually.
* It is fully **open source (Apache 2).** You can use the code for free and without strings attached. &#x20;
* It is a holistic solution that allows you to **build** **use cases “end-to-end”.** There is no need to research, combine or tweak different libraries to build pilots or production systems.
* It **abstracts complexity** via different interfaces (CLI, APIs). Apart from the abstracted core infrastructure which enables low-level functionality (e.g. key handling, data storage, signing), additional services **facilitate development and integration** (e.g. Issuer and Verifier Portals).
* It is **modular, composable and built on open standards** allowing you to individualize and extend functionality with your own or third party implementations. This openness **** prevents lock-in and enables you to build solutions that meet your requirements without compromise.&#x20;
* It is **flexible** in a sense that you can deploy and run it on-premise, in your (multi) cloud environment or as a library in your application.&#x20;
* It enables you to **use different identity ecosystems** like Europe’s emerging identity ecosystem ([EBSI, ESSIF](https://ec.europa.eu/digital-building-blocks/wikis/display/ebsi)) in anticipation of a multi-ecosystem future.

## Functionality

The SSI Kit establishes an identity infrastructure layer for any use case in any industry. Its core services are in the scope of:

* **Registry Interactions** (e.g. read, write; agnostic towards the underlying tech e.g. DLT, DNS)
* **Key Management** (e.g. generate, sign, import, export, manage lifecycle)
* **Decentralized Identifier (DID)** operations (e.g. register, resolve, manage lifecycle)
* **Verifiable Credential/Presentations (VC, VP)** operations (e.g. create, issue, present, verify)
* **Ecosystem specific use cases** (e.g. onboarding, data exchange and monetization)

_Illustration:_

![](../../what-is-ssikit/SSI-Kit.png)

## Components

The SSI Kit unifies three components:

* Signatory | For Issues
* Custodian | For Holders
* Auditor | For Verifiers

### Signatory | For Issuers

Signatory allows you to digitise paper credentials and automate data provision to stakeholders.

![](../../what-is-ssikit/Signatory-Issuer.png)



In short, this product provides all functionality required by “Holders”.One-LinerWallet framework for organisations (B2B) and individuals (B2C).Value- Secure storage of keys, sensitive data and secrets without lock-in (full data portability). - Authentication and identification (with 1-click). - Digital signature service (incl. eIDAS compatibility). - Data and consent management (GDPR).Main FunctionsCreate, store, manage, import, export cryptographic keys (e.g. ed25519, secp256k1, eIDAS), personal data or other secrets. Create, store, manage, import, export DIDs and DID Documents. Anchor (write), resolve (look up) and manage the lifecycle of DIDs and DID Documents. Request, store and manage VCs and VPs. Interact with DLTs to anchor or resolve information (e.g. information about legal entities, DIDs, keys, proofs, ...). Authenticate via DIDs, keys or VCs/VPs. Identify/prove attributes via VCs/VPs. Enable other products (Signatory, Auditor).Deployment OptionsOn-Premise. Multi-Cloud (self-managed). Multi-Cloud (managed service by walt.id)Wallet OptionsCloud wallet (multi-cloud, on-prem). Custodial wallet (organisations can offer a wallet "as a service" to their citizens/customers). Mobile app (starting with Android).

### Auditor | For Verifiers <a href="#auditor-or-for-verifiers" id="auditor-or-for-verifiers"></a>

Auditor allows you to verify your customers’ or citisens’ identity data and offer frictionless access to services or products.![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F1k3zreXT6Nz41D1g1C6K%2Fuploads%2Fgit-blob-cfa46bc9aee08a2e799f66822eec66ca94c15ab6%2FAuditor-Verifier.png?alt=media)This product enables your organisation to

* request data (VCs/VPs) from customers, citisens or other stakeholders.
* verify such data (VCs/VPs) incl. integrity, validity, provenance, authenticity.
* trigger pre-defined actions following the verification.
* In short, this product provides all functionality required by “Verifiers”.

One-LinerVerifier backend service for organisations (B2B).ValueImprove citisen/customer experiences by offering them seamless access to services (SSI-based authentication and identification). Get reliable data signed by data sources (41% of customers provide false data due to security and privacy concerns; RSA). Verify citizen/customer data in a privacy-friendly fashion.Reduce help desk requests (e.g. related to passwords). Prevent data breaches (e.g. eliminate passwords).​Deployment OptionsOn-Premise. Multi-Cloud (self-managed). Multi-Cloud (managed service by walt.id)
