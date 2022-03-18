# Components

## Signatory | For Issuers

Signatory allows you to digitize paper credentials and automate data provision to your stakeholders.

It provides all functionality required by “Issuers”. For example:

* Process and authenticate data requests by people or organisations,
* Import data (from local storage or third parties),
* Create re-usable VC templates,
* Create VCs in different formats (e.g. JSON/JWT, JSON-LD),
* Sign VCs using different key types (e.g. ed25519, secp256K1, RSA),
* Manage the lifecycle of VCs (e.g. revocation).
* Issue VCs (e.g. via OIDC/SIOP)

![](../../../what-is-ssikit/Signatory-Issuer.png)

## Custodian | For Holders

Custodian is a secure data hub for people and organizations. It provides all functionality required by “Holders”. For example:

* Interact with Registries (read, write)
* Create, store, manage keys, data (DIDs, VCs) and other secrets,
* Request and import data (VCs) from third parties,
* Selectively disclose data (VCs/VPs) for authentication and identification,
* Manage consent and data access in a user-centric fashion.

![](../../../what-is-ssikit/Custodian-Holder.png)



## Auditor | For Verifiers <a href="#auditor-or-for-verifiers" id="auditor-or-for-verifiers"></a>

Auditor allows you to verify your stakeholders’ identity data and offer frictionless access to services or products. It provides all functionality required by “Verifiers”. For example:

* request data (VCs/VPs) from stakeholders,
* verify data (VCs/VPs; incl. integrity, validity, provenance, authenticity),
* trigger pre-defined actions following the verification.



![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F1k3zreXT6Nz41D1g1C6K%2Fuploads%2Fgit-blob-cfa46bc9aee08a2e799f66822eec66ca94c15ab6%2FAuditor-Verifier.png?alt=media)

