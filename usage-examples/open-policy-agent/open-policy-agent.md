---
description: Credential validation powered by the Open Policy Agent
---

# Open Policy Agent

The Open Policy Agent ([https://www.openpolicyagent.org](https://www.openpolicyagent.org)) is an open source, general-purpose policy engine that unifies policy enforcement. OPA provides a high-level declarative language called [Rego](https://www.openpolicyagent.org/docs/latest/#rego) that lets you specify policy as code in order to offload policy decision-making from your business logic.

The SSI Kit offers an integration with OPA and therefore allows the flexible validation of W3C Verifiable Credentials by the execution of Rego policies.

## Integration of the Open Policy Agent with the SSI Kit

The following graphic illustrates the technical architecture how a custom application can verify credentials by utilizing the Open Policy Agent.

![SSI Kit and the Open Policy Agent](<../.gitbook/assets/opa (1).png>)

In order to verify W3C Verifiable Credentials and Presentations, the SSI Kit offers the [Auditor API](https://auditor.ssikit.walt.id/). This API serves as integration point for a Verifier application, but also can be used for testing by the built-in CLI tool. In either way a Verifiable Credential (VC) is forwarded to the SSI Kit in order to have it verified.

The SSI Kit loads a Rego Policy either from a file-system, database or a trusted registry that most likely is implemented using Distributed Ledger Technology.

Further on the SSI Kit generates the verification request which is processed by the OPA engine. This request consists of the policy, the input-data to be verified and the action. The input-data is just the relevant data-points of the credential - typically the nested JSON-object "credentialSubject" or part of it. The "action" is the request that should be granted by the policy.

The Open Policy Agent processes the verification request and returns the result to the SSI Kit. The SSI Kit evaluates the result and composes an aggregated credential validation response (as also other validation checks are performed) for the calling party.

## Example VC validation with the Open Policy Agent

* See the [**Dynamic Verification Policies**](../concepts/verification-policies/dynamic-policies.md) section for a full example of verifying credentials with a Rego/OPA policy.
* See how the verification of W3C Verifiable Credentials using OPA (Open Policy Agent) works in a [hands-on video](https://www.youtube.com/watch?v=mue4UjzOZ3Q)

