---
noIndex: true
---

# Issuing

Issuing involves an exchange between a Holder and an Issuer, by which the Holder receives a set of offers from the Issuer. Once the Holder accepts the offers, the Issuer converts them into verifiable credentials and supplies them to the Holder.

Depending on data source location and process initiating party, the following issuing types are supported:

* custom - credential agent loads offers from itself as well as calling out webhooks
  * demand triggered - Holder initiates the credential claiming process
    * Issuer responds with the available credential offers according to Holder’s criteria
  * supply triggered - Issuer initiates the credential claiming process
    * offers are made available to the Holder using a notification mechanism by sending a deep-link or qr-code to claim the credentials
* batch - credential agent loads offers only from itself
  * a specialized version of supply triggered custom issuing

More information on issuing can be found at https://docs.velocitynetwork.foundation/docs/developers/developers-guide-issuing.
