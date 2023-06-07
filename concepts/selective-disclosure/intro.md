---
description: Selective Disclosure allows holders to reveal only necessary information.
---

# Intro

### What is Selective Disclosure?

**Selective disclosure enables a holder to choose which pieces of information contained in a Verifiable Credential will be revealed to a verifier**, rather than being forced to reveal all the data present in a Verifiable Credential.

For example, Alice could now only share her age to verify being old enough to purchase products offered in an ecommerce shop, without revealing other personal information present in her Verifiable ID document used for verification. This allows for **greater privacy and control over personal data**.

### The importance of Selective Disclosure

Selective disclosure is a critical aspect of SSI because it enables individuals to share only the minimum amount of personal information necessary to complete a transaction or interaction, while keeping the rest of their personal data private. This reduces the risk of identity theft and other types of fraud.

### SD-JWTs: A Mechanism for Selective Disclosure

Our implementation of selective disclosure currently does not follow any specific standard, as standards in the field are still under development. As reference, we used the [Selective Disclosure for JWTs (SD-JWT)](https://www.ietf.org/archive/id/draft-ietf-oauth-selective-disclosure-jwt-04.html) reference by IETF. Please note that our implementation is subject to change.

#### What is an SD-JWT

A Selective Disclosure JSON Web Token (SD-JWT) is a type of [JSON Web Token](#user-content-fn-1)[^1] in which the claims in the body are hashed, making them unreadable without disclosure. By providing the necessary disclosures, the original values of the claims can be revealed.

#### How it works

When presenting a classical credential via JWT, claims are visible to the verifier in plain text. With an SD-JWT credential, claims are encrypted in a hashed format, making them unreadable. This allows the holder to choose which claims to reveal to the verifier by providing the plain text key-value pairs (known as disclosures) next to the SD-JWT. The verifier can then hash these disclosures and compare them to the values in the SD-JWT, verifying that the claim was part of the SD-JWT. Additionally, SD-JWTs also allow for decoy hashes to be included in the credential, which are dummy values to conceal the actual number of claims in the credential.



<figure><img src="../../.gitbook/assets/Screenshot on 2023-05-15 at 164216.png" alt=""><figcaption><p>Comparison of normal and SD-JWT credential</p></figcaption></figure>



In the following section, we will see how to issue and verify SD-JWT credentials.

[^1]: JWTs (JSON Web Tokens) are a compact, URL-safe means of representing claims to be transferred between two parties. They consist of three parts: a header, a payload, and a signature. The header describes the cryptographic algorithm used to sign the token, the payload contains the claims being made, and the signature is used to verify the integrity of the token
