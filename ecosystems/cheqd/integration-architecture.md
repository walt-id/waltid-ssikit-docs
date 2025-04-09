---
noIndex: true
---

# Integration architecture

In order to be able to onboard the `did:cheqd` on testnet and mainnet, SSIKit relies on a [cheqd universal registrar](https://github.com/cheqd/did-registrar) deployed on walt.id infrastructure. The DID will be created using a key imported into or also created with SSIKit.

<figure><img src="../../.gitbook/assets/CHEQD Network walt.id stack CHEQD Connector Signatory API Auditor API CHEQD Connector Discord Server CHEQD Credential Platform (Issuing_Verification logic) Signatory API Auditor API CHEQD Wallet + Keplr Auth CHEQD Discord + CHE.png" alt=""><figcaption><p>cheqd architecture infrastructure</p></figcaption></figure>
