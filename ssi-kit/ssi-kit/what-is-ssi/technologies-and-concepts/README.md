---
description: Learn about the technologies and concepts on which SSI is based.
---

# Technologies & Concepts

Understanding SSI requires the understanding of a few core concepts:

* [**Registries**](registries.md), which hold a shared and trusted record of information. In other words, they represent a “layer of trust” and can be referred to as the “single source of truth”.
* **Cryptographic keys**, which convey control over digital identities and enable core functionality such as encryption and authentication.
* [**Decentralized Identifiers (DIDs)**](decentralised-identifiers-dids.md), which give us the power of verifying information, for example credentials, anywhere, anytime, through the establishment of a public key infrastructure. They link keys to unique identifiers that allow different parties to find and interact with each other.
* [**Verifiable Credentials** **(VCs)**](verifiable-credentials-vcs-and-verifiable-presentations-vps.md) which are digital identity documents that can easily and securely be shared with and verified (incl. validity, integrity, authenticity, provenance) by anyone in a privacy preserving way. Importantly, they are never (!) stored on a blockchain due to privacy and compliance reasons.
* [**Verifiable Presentations (VPs)**](verifiable-presentations-vps.md), contain identity data for verification from one or multiple VCs and are mainly created by the holder of the VCs.
* [**Protocols**](data-exchange-protocols.md) enable the exchange of data (VCs) between different parties.&#x20;
* **Wallets**, which store our keys (control) and VCs (identity data) and enable the management and sharing of our digital identities and data via easy-to-use applications.

#### The SSI tech stack:

![](<../../../../.gitbook/assets/Screenshot 2022-03-16 at 13.16.32.png>)



#### How the SSI works:

The following graphic shows how SSI works and highlights the core concepts (in blue)



![](https://images.squarespace-cdn.com/content/v1/609c0ddf94bcc0278a7cbdb4/6276f3d0-2d29-4664-be03-65d555fb824c/Screenshot+2022-03-09+at+08.26.35.png?format=2500w)

#### Building Blocks:

Think of these core concepts as different building blocks that are available in different variations and can be put together in different ways:

![Different technologies can be used to establish Trust Registries like blockchains (EBSI, Ethereum) or the domain name service (DNS). SSI even works (for certain use cases) without any Trust Registries but purely on a peer-to-peer basis. Similarly different types of DIDs, keys, proofs, credential formats,  authentication and data exchange protocols can be used.](https://images.squarespace-cdn.com/content/v1/609c0ddf94bcc0278a7cbdb4/1646980697410-HI3ESFOZM2HT5DZ12HG8/Screenshot+2022-03-10+at+09.34.37.png?format=1500w)

**As a result, there are** **different “flavours” of SSI** depending on which variations of which building blocks have been used and how they have been put together.

Importantly, the differences in terms of technologies that are being used illustrate why interoperability has always been one of the most important topics within the industry and why the development and use of open standards (e.g. by the W3C, Decentralized Identity Foundation, OpenID Foundation and others) are vital for technology and vendor selection.

