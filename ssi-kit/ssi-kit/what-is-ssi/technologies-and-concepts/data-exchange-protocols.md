---
description: >-
  Data Exchange (Protocols) enable the exchange of data (VCs) between different
  parties.
noIndex: true
---

# Data Exchange (Protocols)

Different authentication and data exchange protocols are used to **securely transfer identity data** (e.g. VCs, VPs) **between parties** (e.g. from an Issuer to a Holder). They typically establish a mutually authenticated and encrypted data channel between the communicating parties.

The most common data exchange protocols used for SSI are:

* OIDC4SSI / SIOP (Self-Issued OpenID Connect Provider): An extension of a mature authentication and authorization protocol called "OpenID Connect" (OIDC).
* DIDComm: A novel protocol specifically designed for SSI and maintained by the Decentralized Identity Foundation (DIF).
* Credential Handler API: A proposed browser-extension that may be used to connect the user's identity wallet to a web-application.

{% hint style="info" %}
Our solutions enable you to use different data exchange protocols like OIDC/SIOP as required by different ecosystems.
{% endhint %}
