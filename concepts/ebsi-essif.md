# EU Blockchain Service Infrastructure (EBSI, ESSIF)&#x20;

This section shows how you can use the SSI Kit to interact with Europe’s emerging identity ecosystem based on the

* **EU Blockchain Service Infrastructure (EBSI)**
* **EU Self-Sovereign Identity Framework (ESSIF)**

Refer to [**EBSI/ESSIF usage examples**](../usage-examples/ebsi-essif/usage-examples.md) for examples of using **SSI Kit command line interface** with the EBSI/ESSIF infrastructures.

## ESSIF Use Cases & Flow Diagrams

### State of the EBSI/ESSIF specifications

{% hint style="danger" %}
Note, that some of the flows are not in their final version. Slight modifications are to be expected.
{% endhint %}

### ESSIF DID Registration

Creation and anchoring of a new DID on the EBSI ledger (incl. use of "Verifiable Authorizations" and EBSI access tokens).

![ESSIF DID registration](./essif/02\_essif-register-did.png)

For SSIKit usage examples, refer to: [**EBSI DID registration**](../ecosystems-interoperability/usage-examples.md#ebsi-did-registration)

### ESSIF Onboarding

Onboarding of a legal entity to the EBSI/ESSIF ecosystem (incl. combined VC request and DID registration).

![ESSIF Onboarding](./essif/essif-onboarding.png)

### EBSI Auth API

Gaining access to protected EBSI/ESSIF services (incl. presentation of "Verifiable Authorization").

![EBSI Auth API](./essif/04\_essif-auth-api.png)

### Issuance of Verifiable Credentials

The ESSIF protocol for issuance of verifiable credentials aims to being compliant with the OIDC for credential issuance specification. Refer to the respective section for details:

[**OIDC for credential issuance**](../getting-started/cli-command-line-interface/oidc.md#oidc-for-credential-issuance)

### Exchange of Verifiable Presentations

The ESSIF protocol for presentation of verifiable credentials to a Verifier or Relying Party, aims to being compliant with the OIDC/SIOPv2 specification. Refer to this section for details:

[**OIDC/SIOPv2 for verifiable presentations**](../getting-started/cli-command-line-interface/oidc.md#oidcsiopv2-for-verifiable-presentations)

### Code examples

{% hint style="success" %}
Several code-examples how to use the ESSIF functionality of the SSI Kit are shown on [GitHub](https://github.com/walt-id/waltid-ssikit-examples)
{% endhint %}
