# OpenID Connect (OIDC)

This section shows how the SSIKit can be used to interact with OpenID Connect identity providers for the exchange of verifiables credentials and presentation.

Below you find **sequence diagrams**, for the issuance and verification flows.

Examples of using the **SSIKit command line interface** to interact with OIDC issuers and verifiers, can be found in the [**OIDC usage examples**](../usage-examples/usage-examples.md).

## OIDC for credential issuance

The SSIKit implements the OIDC credential issuance flow, allowing SDK and/or CLI users to get credentials issued from OIDC compliant issuers.

{% hint style="info" %}
The respective **OIDC4CI** specification can be found at:

[**OIDC4CI - OIDC for credential issuance**](https://tlodderstedt.github.io/openid-connect-4-verifiable-credential-issuance-1\_0-01.html)
{% endhint %}

![OIDC for CI](puml/oidc-credential-issuance-ssikit.png)

{% hint style="info" %}
Refer also to our **web wallet documentation**, for an example of an actual end-to-end integration of the OIDC issuance flow:
{% endhint %}

{% content-ref url="https://app.gitbook.com/o/ZPIzdSlXqm9n9ywE2dcK/s/rhL2aTXU1w6MO3blK9B1/" %}
[Wallet](https://app.gitbook.com/o/ZPIzdSlXqm9n9ywE2dcK/s/rhL2aTXU1w6MO3blK9B1/)
{% endcontent-ref %}

## OIDC/SIOPv2 for verifiable presentations

The SSIKit also supports the OIDC/SIOPv2 credential presentation flow, allowing SDK and CLI users to present verifiable credentials to an OIDC compliant verifier.

{% hint style="info" %}
The respective **OIDC4VP/SIOPv2** specification can be found at:

[**OIDC4VP - OIDC for verifiable presentations**](https://openid.net/specs/openid-connect-4-verifiable-presentations-1\_0.html)
{% endhint %}

![OIDC for VP](puml/siop-vc-presentation-ssikit.png)

{% hint style="info" %}
Refer also to our **web wallet documentation**, for an example of an actual end-to-end integration of the OIDC verification flow:
{% endhint %}

{% content-ref url="https://app.gitbook.com/o/ZPIzdSlXqm9n9ywE2dcK/s/rhL2aTXU1w6MO3blK9B1/" %}
[Wallet](https://app.gitbook.com/o/ZPIzdSlXqm9n9ywE2dcK/s/rhL2aTXU1w6MO3blK9B1/)
{% endcontent-ref %}
