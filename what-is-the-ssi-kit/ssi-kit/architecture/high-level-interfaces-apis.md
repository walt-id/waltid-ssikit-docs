---
noIndex: true
---

# High-Level Interfaces / APIs

The SSI Kit exposes high-level interfaces / APIs to hide the complex introduced by

* low-level services (e.g. key management, signing, data storage)
* different ecosystems (i.e. different SSI flavors, business logic and governance frameworks).

The functionality of the high-level interfaces correlate with the [SSI Kit Components](../../../ssi-kit/ssi-kit-or-basics/components.md). The functions are grouped around:

* **issuing** Verifiable Credentials by the Signatory,
* **holding** (storing, presenting) Verifiable Credentials by the Custodian
* and **verifying** Verifiable Credentials by the Auditor.

The interfaces can be used in JVM-based applications directly, or via the REST API.

The Swagger documentation can be found under section [REST API](../../../getting-started/rest-apis.md).

