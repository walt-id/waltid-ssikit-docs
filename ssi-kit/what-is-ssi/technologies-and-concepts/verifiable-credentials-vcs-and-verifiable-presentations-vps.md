# Verifiable Credentials (VCs)

Verifiable Credentials (VCs) are **digital credentials** that **contain actual identity data** of people or organizations and are standardized by the [W3C](https://www.w3.org/TR/vc-data-model/). They are **digital equivalents of paper-based identity documents** like passports or diplomas.

Before we dive deeper into Verifiable Credentials and learn about their structure and how they work, we will have a look at the problems of today's credentials.

## Credentials today

Today's credentials are easy to fake, hard to verify, and not privacy preserving by design. Making it hard for business and people offline but especially online to trust each other, when exchanging information and data. This brings about many problems, thereunder:

* To verify that a document or claim presented is actually valid, can take up many resources and time. Just think about, what you had to do last time you opened up a bank account. The presenting of your ID card via a video call, taking selfies etc.
* Often the credentials provided by you to get access to a service, are then stored on centralized servers. This makes them not only vulnerable to data breaches, but you also need to trust the organization that they only use the data in ways you would agree with.
* You might be forced to disclose more information than needed. The police officer checking your driver license, in most cases, only needs to know that you are allowed to drive, but not where you live or your name.
* Organizations employing people who claim to have a skill by presenting a fake certificate, can get jobs, which, when performed poorly, could have catastrophic consequences.

This is why we need a better way to make claims,  and that is where Verifiable Credentials come in.



## **Verifiable Credentials to the Rescue**

With VCs and the standard introduced by [W3C](https://www.w3.org/TR/vc-data-model/), we now have a way of creating a digital piece of information that identifies a particular entity or verifies a specific attribute, qualification or claim about them, in a way, that is almost impossible to forger, easy to verify, and privacy preserving by design.  Leaving us with the following benefits:

* **Easy to verify:** There is a clearly defined and reliable way of verifying a Verifiable Credential.&#x20;
* **Temper-proof:** No one expect the issuer (entity creating the VC) can change the claims stated in the VC.
* **Independent:** No need to contact the issuer of the presented certificate to be certain about its validity. The check can happen in an independent, asynchronous way.
* **Data is owned:** The holder of a certificate now owns the data and decides what to share and when, only providing proof but never actually giving it (a copy) to the service provider.
* **Portable:** The user is free to choose where to take their VC and in which wallet it is saved.



### The lifecycle of a Verifiable Credential

For us to understand the typical lifecycle of a Verifiable Credential, we need to make sure, we understand the idea behind an [Issuer, Holder and Verifier](https://docs.walt.id/v/ssikit/ssi-kit/what-is-ssi/ssi-or-basics#how-does-ssi-work) and what [DID and DID Documents](decentralised-identifiers-dids.md) are. With that out of the way, let's start with cycle.&#x20;

### Setup

* **Registration of the Issuer:** Depending on the governance framework, the issuer will be accredited by a trusted entity, before their DID as well as DID Document will be put into the [Registry](registries.md). The Registry is the Single Source of truth and trust entity which verifiers will use as a reference point to make sure a  presented VC is valid. &#x20;
* **Holder setup:** The holder generates the DID via the wallet and saves the private and public key as part of the DID Document, to be able to request, receive and present Verifiable Credentials from thereon. The DID and the DID Document will never be put into any registry, it will only exist locally in the wallet.
* **Verifier setup:** The verifier only needs to have the technology to communicate with the registries when presented with a VC, to validate its authenticity using the DID and the DID Document from the issuer.



After the registration of the issuer and the setup of the wallet for the holder, the holder can now receive a VC from the issuer.&#x20;

### Issuance & Content

When the holder receives their Verifiable Credential it will be saved on their wallet, and it will contain the following:

* **Metadata:**&#x20;
  * The DID of the issuer
  * The status of the credential (expiration and issuing date, revoke state)
* **Claims:**
  * The DID of the holder of the credential
  * The claims about the subject (what the issuer asserts about the subject). This could be, if they can drive a car and what type of car (driver license) or the subject of their study and knowledge areas skilled in (university certificate).
* **Proof:**
  * This will contain the signatures of the issuer, which can be used to see if the content of the VC has been tempered with and for an authenticity check.&#x20;

### Using the Certificate

The holder can now use the VC in their wallet to access services, and get access to products by presenting it to the service/product provider (The Verifier) and thereby making it a [Verifiable Presentation](verifiable-presentations-vps.md). The verifier will go through the following steps to make sure the certificate is valid:

1. Before the validation of the content of the certificate can take place, the VC needs to be parsed from the support JSON-LD or the JWT format. Depending on the ecosystem used, there will also happen a [validation of the schema](../../../usage-examples/verifiable-credentials/verification-policies.md) of the credential.
2. Validate that the DID of the holder, stated in the certificate, is the person presenting the VC.
3. Checking if all the state values are valid (expiration date and if the certificate is revoked or not).
4. Checking the claims about the subject and if they match the requirements to give the person access to the service they are requesting to get access to.
5. Checking the signatures of the issuer and the holder, by getting the DID of the issuer from the registry and the DID from the holder in their wallet and validating it using the public keys presented in the related DID documents.

When all the checks pass, the verifier can now grant the holder access to the service requested.



## Example of a Verifiable Credential

```json
{
 // Sets the context of the credential. Establishes the idea and meaning behind the 
 // special terms used in the credential, so that the parties interacting with the
 // credential are on the same side.
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://essif.europa.eu/schemas/v-a/2020/v1",
    "https://essif.europa.eu/schemas/eidas/2020/v1"
  ],
  // The identifier of the Verifiable Credential
  "id": "education#higherEducation#3fea53a4-0432-4910-ac9c-69ah8da3c37f",
  // Types of the credential, giving you an overview of the data to expect
  "type": [
    "VerifiableCredential",
    "VerifiableAttestation"
  ],
  // Issuer of the credential
  "issuer": "did:ebsi:2757945549477fc571663bee12042873fe555b674bd294a3",
  // When the credential was issued
  "issuanceDate": "2019-06-22T14:11:44Z",
  // When the credential will be valid
  "validFrom": "2019-06-22T14:11:44Z",
  // Claims about the subject
  "credentialSubject": {
  // Identifier of the only subject of the credential
    "id": "id111"
  },
  // Current status of the credential, such as if it is suspended or revoked
  "credentialStatus": {
    "id": "https://essif.europa.eu/status/identity#verifiableID#1dee355d-0432-4910-ac9c-70d89e8d674e",
    "type": "CredentialStatusList2020"
  },
  // Used data schema by the credential. It gives the verifiers an idea, 
  // if the presented data in the credential conforms.
  "credentialSchema": {
    "id": "https://essif.europa.eu/tsr-vid/verifiableid1.json",
    "type": "JsonSchemaValidator2018"
  },
  // It can give the verifier an extra level of security, that the issued credential
  // can be trused, as it lays out requirements the issuer needs to check the 
  // subject against, before issuance of the credential can take place.
  "evidence": [
    {
      "id": "https://essif.europa.eu/tsr-va/evidence/f2aeec97-fc0d-42bf-8ca7-0548192d5678",
      "type": [
        "DocumentVerification"
      ],
      "verifier": "did:ebsi:2962fb784df61baa267c8132497539f8c674b37c1244a7a",
      "evidenceDocument": "Passport",
      "subjectPresence": "Physical",
      "documentPresence": "Physical"
    }
  ],
  // Digital proof that makes the credential temper-evident
  "proof": {
    // The cryptographic signature suite that was used to generate the signature
    "type": "EidasSeal2021",
    // The date when the signature was created
    "created": "2019-06-22T14:11:44Z",
    // Purpose of this prove
    "proofPurpose": "assertionMethod",
    // The identifier of the public key that can be used to verify the signature
    "verificationMethod": "did:ebsi:2757945549477fc571663bee12042873fe555b674bd294a3#2368332668",
    // The digital signature value
    "jws": "HG21J4fdlnBvBA+y6D...amP7O="
  }
}
```

{% hint style="info" %}
Our open source products enable you to act as an "Issuer" (create and issue VCs), as a Holder (manage and share VCs/VPs) and as a Verifier (request and verify VCs/VPs).
{% endhint %}
