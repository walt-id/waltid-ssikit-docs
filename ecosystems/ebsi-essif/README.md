# EBSI

This section shows how you can use the SSI Kit to interact with Europe’s emerging identity ecosystem based on the

* **EU Blockchain Service Infrastructure (EBSI)**
* **EU Self-Sovereign Identity Framework (ESSIF)**

[Here](usage-examples/usage-examples.md) \*\*\*\* you can find examples on how to use the SSI Kit command line interface to interact with the EBSI/ESSIF ecosystem.

### State of the EBSI/ESSIF specifications

{% hint style="danger" %}
Note, that some of the flows are not in their final version. Slight modifications are to be expected.
{% endhint %}

### ESSIF DID Registration

Creation and anchoring of a new DID on the EBSI ledger (incl. use of "Verifiable Authorizations" and EBSI access tokens).

![ESSIF DID registration](use-cases/02\_essif-register-did.png)

For SSIKit usage examples, refer to: [**EBSI DID registration**](usage-examples/onboarding-and-dids.md)

### ESSIF Onboarding

Onboarding of a legal entity to the EBSI/ESSIF ecosystem (incl. combined VC request and DID registration).

![ESSIF Onboarding](use-cases/essif-onboarding.png)

### EBSI Auth API

Gaining access to protected EBSI/ESSIF services (incl. presentation of "Verifiable Authorization").

![EBSI Auth API](use-cases/04\_essif-auth-api.png)

### Issuance of Verifiable Credentials

The ESSIF protocol for issuance of verifiable credentials aims to being compliant with the OIDC for credential issuance specification. Refer to the respective section for details:

[**OIDC for credential issuance**](../../concepts/oidc/credential-issuance/)

### Exchange of Verifiable Presentations

The ESSIF protocol for presentation of verifiable credentials to a Verifier or Relying Party, aims to being compliant with the OIDC/SIOPv2 specification. Refer to this section for details:

[**OIDC/SIOPv2 for verifiable presentations**](../../concepts/oidc/presentation-exchange/)

### Code examples

{% hint style="success" %}
Several code-examples how to use the ESSIF functionality of the SSI Kit are shown on [GitHub](https://github.com/walt-id/waltid-ssikit-examples)
{% endhint %}
