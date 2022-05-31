---
description: Credential validation powered by the Open Policy Agent
---

# Open Policy Agent

The Open Policy Agent ([https://www.openpolicyagent.org](https://www.openpolicyagent.org)) is an open source, general-purpose policy engine that unifies policy enforcement. OPA provides a high-level declarative language called [Rego](https://www.openpolicyagent.org/docs/latest/#rego) that lets you specify policy as code and simple APIs to offload policy decision-making from your software.&#x20;

The SSI Kit offers an integration with OPA and therfore allows the flexible validation of W3C Verifiable Credentials by the execution of Rego policies.

## Integration of the Open Policy Agent with the SSI Kit

The following graphic illustrates the technical architecture how a custom application can verify credentials by utilizing the Open Policy Agent.

![SSI Kit and the Open Policy Agent](<../../.gitbook/assets/opa (1).png>)

In order to verify W3C Verifiable Credentials and Presentations, the SSI Kit offers the [Auditor API](https://auditor.ssikit.walt.id/). This API is typically the integration point of a Verifier portal (a custom application), but also can be used for testing by the built-in CLI tool. In either way a Verifiable Credential (VC) is forwarded to the SSI Kit iorder to have it verified.
