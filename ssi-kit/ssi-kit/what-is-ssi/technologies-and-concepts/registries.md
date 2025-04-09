---
description: A shared and trusted record of information.
noIndex: true
---

# Registries

Registries serve as a **single source of truth** which all participants of an SSI ecosystem can trust. Depending on the ecosystem, registries make information accessible to anyone or just a limited group. Registries are important because they enable:

* **(Distributed) Public Key Infrastructures (DPKIs)** which establishes an open distribution system for public keys which can be used for encryption and authentication among others.
* **Trust Registries** hold reliable information about people, organizations, things and even credentials (e.g. data models, status and validity information) to ensure that different parties can trust each other and the identity-related data they exchange.

Different technologies can be used to implement Registries. For example:

* **Blockchains** or **L1**: Typically blockchains are used because it is unfeasible (or even impossible) to tamper with them. The fact that no single organization can change the contents of a blockchain or manipulate the terms by which it is governed are very aligned with the requirements for identity ecosystems. Today, we see a growing number of developers and organizations focusing on so-called permissioned blockchains (i.e. only a selected group can “write”) like Ethereum Quorum/Enterprise. Permissionless blockchains, like Ethereum, are still used, but less than the permissioned alternatives for a variety of reasons like scalability, costs, lack of customisable governance frameworks.
* **L2**: Layer two networks sit on top of blockchains and aggregate data before anchoring it. The main idea behind them is to circumvent common challenges of public, permissionless blockchains like scalability and cost issues. The most popular implementations in the context of identity are “ION” (for Bitcoin) and “Element” (for Ethereum).
* **Other Distributed Ledger Technologies (DLTs)**: Sometimes other DLTs are utilised like the Interplanetary File System (IPFS) though its use for digital identity remains limited.
* **Domain Name Service (DNS)**: Considering certain drawbacks of DLTs and their relatively slow adoption by the mass market, DNS can also be used to serve as a registry. Though it is not fully decentralised (considering its underlying governance framework), DNS has many advantages like its maturity and global adoption.

Importantly, SSI can be implemented without registries, particularly without blockchains, because identity data (or at least personal data of individuals) is never anchored due to privacy and compliance reasons. However, by combining SSI with blockchains (or other technologies), robust and trustworthy identity ecosystems that utilise transparent DPKIs and reliable Trust Registries can emerge.
