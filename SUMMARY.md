# Table of contents

## General <a href="#ssi-kit" id="ssi-kit"></a>

* [Introduction](README.md)
* [Self-Sovereign Identity (SSI)](what-is-the-ssi-kit/what-is-ssi/README.md)
  * [SSI | Basics](what-is-the-ssi-kit/what-is-ssi/ssi-or-basics.md)
  * [Technologies & Concepts](ssi-kit/what-is-ssi/technologies-and-concepts/README.md)
    * [Registries](ssi-kit/what-is-ssi/technologies-and-concepts/registries.md)
    * [Decentralised Identifiers (DIDs)](ssi-kit/what-is-ssi/technologies-and-concepts/decentralised-identifiers-dids.md)
    * [Verifiable Credentials (VCs)](ssi-kit/what-is-ssi/technologies-and-concepts/verifiable-credentials-vcs-and-verifiable-presentations-vps.md)
    * [Verifiable Presentations (VPs)](ssi-kit/what-is-ssi/technologies-and-concepts/verifiable-presentations-vps.md)
    * [Data Exchange (Protocols)](ssi-kit/what-is-ssi/technologies-and-concepts/data-exchange-protocols.md)
* [SSI Kit](what-is-the-ssi-kit/ssi-kit/README.md)
  * [SSI Kit | Basics](what-is-the-ssi-kit/ssi-kit/ssi-kit-or-basics/README.md)
    * [Overview](what-is-the-ssi-kit/ssi-kit/ssi-kit-or-basics/overview.md)
    * [Functionality](what-is-the-ssi-kit/ssi-kit/ssi-kit-or-basics/functionality.md)
    * [Components](what-is-the-ssi-kit/ssi-kit/ssi-kit-or-basics/components.md)
  * [SSI Flavors & Ecosystems](what-is-the-ssi-kit/ssi-kit/tech-stack/README.md)
    * [Trust Registries](what-is-the-ssi-kit/ssi-kit/tech-stack/trust-registries.md)
    * [Keys](what-is-the-ssi-kit/ssi-kit/tech-stack/keys.md)
    * [Decentralized Identifiers (DIDs)](what-is-the-ssi-kit/ssi-kit/tech-stack/decentralized-identifiers-dids.md)
    * [Verifiable Credentials (VCs)](ssi-kit/ssi-kit/tech-stack/verifiable-credentials-vcs.md)
    * [Data Exchange Protocols](what-is-the-ssi-kit/ssi-kit/tech-stack/data-exchange-protocols.md)
  * [Architecture](what-is-the-ssi-kit/ssi-kit/architecture/README.md)
    * [Low-Level Service Abstraction](what-is-the-ssi-kit/ssi-kit/architecture/low-level-service-abstraction.md)
    * [Ecosystem Abstraction](what-is-the-ssi-kit/ssi-kit/architecture/ecosystem-abstraction.md)
    * [High-Level Interfaces / APIs](what-is-the-ssi-kit/ssi-kit/architecture/high-level-interfaces-apis.md)
  * [Use Cases](what-is-the-ssi-kit/ssi-kit/use-cases.md)

## Getting started

* [Quick Start](getting-started/quick-start.md)
* [REST API](getting-started/rest-apis.md)
  * [Signatory API - For Issuers](getting-started/rest-apis/signatory-api.md)
  * [Custodian API - For Holders](getting-started/rest-apis/custodian-api.md)
  * [Auditor API - For Verifiers](getting-started/rest-apis/auditor-api.md)
  * [Core API](getting-started/rest-apis/core-api.md)
  * [API Serving Configs](getting-started/rest-apis/api-service.md)
* [Dependency (JVM)](getting-started/dependency-jvm/README.md)
  * [Java Examples](https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/java/id/walt/ssikitexamples)
  * [Kotlin Examples](https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/kotlin/id/walt/ssikitexamples)
* [CLI | Command Line Interface](getting-started/cli-command-line-interface.md)
  * [Key Management](getting-started/cli-command-line-interface/key-management.md)
  * [Decentralized Identifiers](getting-started/cli-command-line-interface/decentralized-identifiers.md)
  * [Verifiable Credentials](getting-started/cli-command-line-interface/verifiable-credentials.md)
  * [OpenID Connect (OIDC)](getting-started/cli-command-line-interface/open-id-connect.md)
* [Building the Project](getting-started/build.md)
  * [Docker Build](getting-started/quick-start/docker.md)
  * [Local Build](getting-started/quick-start/build/local-build.md)
* [Project Configurations](getting-started/configuration.md)
* [Demo](getting-started/demo.md)

## Ecosystems

* [EBSI](ecosystems/ebsi-essif/README.md)
  * [Basics](ecosystems/ebsi-essif/ebsi-essif-or-basics.md)
  * [Use Cases & Flow Diagrams](ecosystems/ebsi-essif/use-cases/use-cases-and-flow-diagrams.md)
  * [Command line interface](ecosystems/ebsi-essif/cli/README.md)
    * [DID Registration](ecosystems/ebsi-essif/cli/did-registration.md)
  * [REST API](getting-started/rest-apis/essif-api.md)
  * [Usage / examples](ecosystems/ebsi-essif/usage-examples/usage-examples.md)
    * [Onboarding & DIDs](ecosystems/ebsi-essif/usage-examples/onboarding-and-dids.md)
    * [Build end-to-end use cases](ecosystems/ebsi-essif/usage-examples/build-end-to-end-use-cases.md)
* [IOTA](ecosystems/iota/README.md)
  * [OIDC4VP profile for Login-with-IOTA](ecosystems/iota/oidc4vp-profile.md)
  * [Login With IOTA Demo](https://youtu.be/samp2o65nX8)
* [Velocity](ecosystems/velocity/README.md)
  * [Basics](ecosystems/velocity/basics/README.md)
    * [Onboarding](ecosystems/velocity/basics/onboarding.md)
    * [Issuing](ecosystems/velocity/basics/issuing.md)
    * [Inspection](ecosystems/velocity/basics/inspection.md)
  * [Integration with SSIKit](ecosystems/velocity/integration/README.md)
  * [Command line interface](ecosystems/velocity/cli/README.md)
    * [Onboarding](ecosystems/velocity/cli/onboarding.md)
    * [Issuing](ecosystems/velocity/cli/issuance.md)
    * [Inspection](ecosystems/velocity/cli/verification.md)
* [cheqd](ecosystems/cheqd/README.md)
  * [Integration architecture](ecosystems/cheqd/integration-architecture.md)
  * [Create DID](ecosystems/cheqd/create-did.md)
  * [Issue VC](ecosystems/cheqd/issue-vc.md)
  * [Verify VC](ecosystems/cheqd/verify-vc.md)

## Tutorials

* [My First VC](tutorials/my-first-vc.md)

## Concepts

* [Open Policy Agent](usage-examples/open-policy-agent.md)
* [OpenID Connect (OIDC)](helpful-concepts/oidc/README.md)
  * [Credential Issuance](helpful-concepts/oidc/credential-issuance.md)
    * [OIDC4CI | Example](usage-examples/data-exchange-protocols/oidc/usage-examples.md)
  * [Presentation Exchange](helpful-concepts/oidc/presentation-exchange.md)
    * [OIDC4VP | Example](usage-examples/data-exchange-protocols/oidc/usage-examples-1.md)
* [Verification Policies](usage-examples/verifiable-credentials/verification-policies.md)
  * [Static Policies](concepts/verification-policies/static-policies.md)
  * [Parameterized Policies](concepts/verification-policies/parameterized-policies.md)
  * [Dynamic Policies](concepts/verification-policies/dynamic-policies.md)
* [Delegation and Mandates](usage-examples/verifiable-credentials/delegation-and-mandates.md)

## Community

* [Discord](https://walt.id/discord)
* [Twitter](https://twitter.com/walt\_id)
* [Newsletter](https://walt.id/community)
* [GitHub Discussions](https://github.com/walt-id/.github/discussions)

## DEVELOPER RELATIONS

* [Contribute](https://github.com/walt-id/.github/discussions/6)
* [Roadmap](https://walt-id.notion.site/fcde1687baab42378b3047d4a22eeaca?v=1140dd17c17b4726a70cc1465d20866d)
* [Share Feedback](https://walt.id/feedback)
* [Contact](https://github.com/walt-id/.github/discussions)

## Product Editions

* [Open Source | Always Free](product-editions/open-source.md)
* [Enterprise | Self-Managed](product-editions/enterprise-or-self-managed.md)
* [Cloud Platform | Managed](product-editions/cloud-platform-or-managed.md)
