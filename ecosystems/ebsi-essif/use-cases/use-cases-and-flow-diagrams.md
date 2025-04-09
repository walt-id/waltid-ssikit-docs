---
noIndex: true
---

# Use Cases & Flow Diagrams

{% hint style="danger" %}
Note, that EBSI/ESSIF specifications are evolving, which means that some flows are not available in their final version. Modifications are to be expected.
{% endhint %}

## ESSIF DID Registration

Creation and anchoring of a new DID on the EBSI ledger (incl. use of "Verifiable Authorizations" and EBSI access tokens).

![ESSIF DID registration](02_essif-register-did.png)

For SSIKit usage examples, refer to: [**EBSI DID registration**](../usage-examples/onboarding-and-dids.md)

## ESSIF Onboarding

Onboarding of a legal entity to the EBSI/ESSIF ecosystem (incl. combined VC request and DID registration).

![ESSIF Onboarding](essif-onboarding.png)

## EBSI Auth API

Gaining access to protected EBSI/ESSIF services (incl. presentation of "Verifiable Authorization").

![EBSI Auth API](04_essif-auth-api.png)

## Issuance of Verifiable Credentials

The ESSIF protocol for issuance of verifiable credentials aims to being compliant with the OIDC for credential issuance specification. Refer to the respective section for details:

[**OIDC for credential issuance**](../../../helpful-concepts/oidc/credential-issuance.md)

## Exchange of Verifiable Presentations

The ESSIF protocol for presentation of verifiable credentials to a Verifier or Relying Party, aims to being compliant with the OIDC/SIOPv2 specification. Refer to this section for details:

[**OIDC/SIOPv2 for verifiable presentations**](../../../helpful-concepts/oidc/presentation-exchange.md)

## Code examples

{% hint style="success" %}
Several code-examples how to use the ESSIF functionality of the SSI Kit are shown on [GitHub](https://github.com/walt-id/waltid-ssikit-examples)
{% endhint %}
