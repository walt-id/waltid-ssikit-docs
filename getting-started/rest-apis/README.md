# REST APIs

## Overview

This sections outlines the APIs of the SSI Kit:

* _Core API_&#x20;
* _Signatory API_
* _Custodian API_
* _Auditor API_
* _ESSIF Connector API_

In order to review the Swagger doc of each API, run the **serve** command of the CLI tool and navigate to the corresponding web pages:

```
    ./ssikit.sh serve
```

or with Docker:

```
    docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0
```

* Core API: http://127.0.0.1:7000
* Signatory API: http://127.0.0.1:7001
* Custodian API: http://127.0.0.1:7002
* Auditor API: http://127.0.0.1:7003
* ESSIF API: http://127.0.0.1:7004

## Core API

The _Core API_ exposes wallet core functionality in the scope of storing and managing:

* cryptographic keys,
* Decentralised Identifiers (DIDs),
* Verifiable Credentials (VCs).

## Signatory API

The _Signatory API_ exposes the "issuance" endpoint, which provides flexible integration possibilities for anyone intending to act as an "Issuer" (i.e. create, sign and issue Verifiable Credentials).

## Custodian API

The _Custodian API_ provides management functions for maintaining secrets and sensitive data (e.g. keys, Verifiable Credentials) in a secure way.

## Auditor API

The _Auditor API_ enables anybody to act as a "Verifier" (i.e. verify Verifiable Credentials or Verifiable Presentations). The validation steps can be easily configured by existing or custom _policies_.

## ESSIF API

The _ESSIF API_ exposes the necessary endpoints for running the ESSIF specific flows between Issuers (incl. ESSIF Onboarding Services), Holders and Verifiers.

Aligned with the ESSIF terminology, the API is grouped by the User Wallet (wallet API for consumers / natural persons) and Enterprise Wallet (wallet API for organisations / legal entities).

Note that the EBSI/ESSIF specifications are expected to evolve which will be reflected in continuous updates of the proposed APIs.
