---
noIndex: true
---

# Basics

## **EU Blockchain Service Infrastructure (EBSI)**

EBSI is a blockchain run by member states and public authorities. The idea is to create a trusted, public ledger that serves as a single source of truth for vital information. As such, EBSI instantiates different Trust Registries, such as

* Trusted Issuers Registry (TIR), which contains information about organisations (e.g. public keys, accreditations, legal name, ...)
* Trusted Accreditation Organisation Registry (TAOR), which is similar to the TIR, but contains information about organisations that can authorise Issuers to issue credentials in regulated fields.
* Trusted Schemas Registry (TSR), which contains information about semantic contexts and vocabularies, policies and templates of VCs and their data models to ensure semantic interoperability.

## European Self-Sovereign Identity Framework (ESSIF)

ESSIF's goal is to bring SSI to Europe. To do so, it fullfills different functions:

* Governance and Trust Framework: ESSIF drives the creation of a EU Governance and Trust Framework supported by Member States.
* Standards and specifications: ESSIF creates business, functional and technical specifications, which make up the European “flavor of SSI”.
* Facilitate Adoption: ESSIF coordinates the adoption of SSI across Europe starting with pilot projects of “Early Adopters” which are public authorities from different member states.

Note that ESSIF specifies its own DID Method and different types of Verifiable Credentials (VCs):

* Verifiable IDs, which are mainly used to identify entities at a high-level of assurance. As such, they can be compared to passports or national IDs.
* Verifiable Attestions, which encode basically any other type of identity information, such as education or work records, financial data or health data.
* Verifiable Manadates, which enable delegation as outlined in this paper.

There are also other variations of VC that evolved over time such as Verifiable Accreditations (as issued by TAOS; see above) or Verifiable Authorizations (used to authorize parties to interact with EBSI).
