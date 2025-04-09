---
noIndex: true
---

# Onboarding

In order to operate on Velocity network, any entity (regardless of scope - issuer, relying party or credential agent operator) has to register with the network.

The onboarding is currently done _manually_ and will custody a DID on the DID:ION network:

* get an account with the registrar
  * by sending an email to [_support@velocitynetwork.foundation_](support@velocitynetwork.foundation)
* set up the organization(s)
  * set the required services according to the use case:
    * issuer - _VlcCareerIssuer\_v1_
    * verifier - _VlcInspector\_v1_
    * agent operator - _VlcCredentialAgentOperator\_v1_
* configure the tenants
  * add the required keys according to the use case:
    * issuer - _ISSUING\_METADATA_
    * verifier - _EXCHANGES_
    * agent operator - _DLT\_TRANSACTIONS_

The configuration steps from above can be completed either using:

* [registration UI](https://docs.velocitynetwork.foundation/docs/developers/developers-guide-getting-started#using-the-registration-ui)
* or [Rest API](https://docs.velocitynetwork.foundation/docs/developers/developers-guide-getting-started#using-json-rest-api-endpoints)

More information on Velocity onboarding can be found at https://docs.velocitynetwork.foundation/docs/developers/developers-guide-getting-started.
