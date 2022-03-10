# EBSI/ESSIF - European SSI and blockchain infrastructures

This section shows how you can use the SSI Kit to interact with Europe’s emerging identity ecosystem based on the

* **EU Blockchain Service Infrastructure (EBSI)**
* **EU Self-Sovereign Identity Framework (ESSIF)**

## ESSIF Use Cases & Flow Diagrams

### State of the EBSI/ESSIF specifications

::: warning
Note, that some of the flows are not in their final version. Slight modifications are to be expected.
:::

[comment]: <> (ESSIF specifies the flows to standardise the following use cases:)

[comment]: <> (1.   ESSIF DID Registration - creation and anchoring of a new DID on the EBSI ledger &#40;incl. use of "Verifiable Authorizations" and EBSI access tokens&#41;.)

[comment]: <> (1.   ESSIF Onboarding - onboarding of a legal entity to the EBSI/ESSIF ecosystem &#40;incl. combined VC request and DID registration&#41;.)

[comment]: <> (1.   EBSI Auth API - gaining access to protected EBSI/ESSIF services &#40;incl. presentation of "Verifiable Authorization"&#41;.)

[comment]: <> (1.   VC Issuance - issuance of VCs from a legal entity to a natural person &#40;incl. OIDC-based data exchange, open interface for third party issuers component&#41;.)

[comment]: <> (1.   VC Exchange - presentation of a Verifiable Presentation to a Verifier / Relying Party &#40;incl. OIDC-based data exchange, open interface for third party verifier component&#41;.)

### ESSIF DID Registration 

Creation and anchoring of a new DID on the EBSI ledger (incl. use of "Verifiable Authorizations" and EBSI access tokens).

![ESSIF VC issuance flow](./essif/02_essif-register-did.png)

For SSIKit usage examples, refer to: [**EBSI DID registration**](../ecosystems-interoperability/ebsi-essif/usage-examples.md#ebsi-did-registration)

### ESSIF Onboarding

Onboarding of a legal entity to the EBSI/ESSIF ecosystem &#40;incl. combined VC request and DID registration&#41;.

![ESSIF Onboarding](./essif/essif-onboarding.png)

### EBSI Auth API

Gaining access to protected EBSI/ESSIF services &#40;incl. presentation of "Verifiable Authorization"&#41;.

![EBSI Auth API ](./essif/04_essif-auth-api.png)

### Issuance of Verifiable Credentials

The ESSIF protocol for issuance of verifiable credentials aims to being compliant with the OIDC for credential issuance specification. Refer to the respective section for details:

[**OIDC for credential issuance**](../ecosystems-interoperability/oidc.md#oidc-for-credential-issuance)

### Exchange of Verifiable Presentations

The ESSIF protocol for presentation of verifiable credentials to a Verifier or Relying Party, aims to being compliant with the OIDC/SIOPv2 specification.
Refer to this section for details:

[**OIDC/SIOPv2 for verifiable presentations**](../ecosystems-interoperability/oidc.md#oidcsiopv2-for-verifiable-presentations)

[comment]: <> (TODO: insert further flows)

### Code examples 

::: tip
Several code-examples how to use the ESSIF functionality of the SSI Kit are shown on [GitHub](https://github.com/walt-id/waltid-ssikit-examples)
:::


