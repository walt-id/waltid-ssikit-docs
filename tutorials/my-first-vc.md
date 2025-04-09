---
noIndex: true
---

# My First VC

In this tutorial, our fictional SSI Use-Case involves Emma, a recent university graduate, who wants to apply for a job. The employer requires proof of her academic credentials. To achieve this, she will use her Verifiable Degree Credential issued by her university.

**Where we start:**

Utilizing the walt.id SSI-Kit's REST-API, we will provide Emma with the Verifiable Degree Credential by creating a DID for both the university (Issuer) and Emma (Holder). After that, the employer (Verifier) will authenticate the Degree Credential using the associated DIDs.

**What we do:**

1. [Run the SSI-Kit and expose API](my-first-vc.md#running-the-ssi-kit)
2. [Create DIDs](my-first-vc.md#creating-the-dids) - for Emma + University
3. [Issue Credential](my-first-vc.md#issuing-a-verifiable-university-degree-credential) to Emma
4. [Verify Credential](my-first-vc.md#verify-the-university-degree-credential) from Emma

### Running the SSI-Kit

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
{% tab title="Docker" %}
Pull the docker container directly from docker hub and run the project

```
docker run -p 7000-7004:7000-7004 -itv $(pwd)/data:/app/data waltid/ssikit serve -b 0.0.0.0
```

This will create a folder called data in your current directory as storage for the VC, DIDs, Keys and other things which need to be stored in order to provide all the functionality.
{% endtab %}

{% tab title="Local" %}
1. Clone the project

```
git clone https://github.com/walt-id/waltid-ssikit.git
```

2\. Change the folder

```
cd waltid-ssikit/
```

3\. Run the project

The first time you run the command you will be asked to built the project. You can confirm the prompt.

```
./ssikit.sh serve
```
{% endtab %}
{% endtabs %}

Now with the project up and running, visit the [walt.id Custodian API](http://localhost:7002/v1/swagger) URL displayed in your terminal. We will use it, to create our first DID (Decentralised Identifier). If you want to learn more about DIDs, visit the [general section.](../ssi-kit/ssi-kit/what-is-ssi/technologies-and-concepts/decentralised-identifiers-dids.md)

#### **Creating the DIDs**

{% tabs %}
{% tab title="REST API" %}
```bash
curl -X 'POST' \
  'http://localhost:7002/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "{method}"
}'
```

**Body Parameters**\
`method`: _**\[string]**_ method of the did. Value can be one of `key`, `web`, `ebsi`, `iota`, `cheqd`, `jwk`\
\
**Example**

```bash
curl -X 'POST' \
  'http://localhost:7002/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "key"
}'
```
{% endtab %}
{% endtabs %}

Create DIDs for the University (Issuer) and Emma (Holder) using the example above twice. Make sure to save the DIDs somewhere, as we will be needing them later for the issuance of the credential.

####

#### Issuing a Verifiable University Degree Credential

Using the DIDs from the previous step, we will now issue a University Degree Credential. To issue the credential, we will be using the [Signatory API endpoint](http://localhost:7001/). Below you find the final credential structure.\
\
**Verifiable Diploma**

```perl
{
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.gov/credentials/3732",
  "issuer": {
    "id": "did:example:456"
  },
  "issuanceDate" : "2023-03-21T15:35:08Z",
  "issued" : "2023-03-21T15:35:08Z",
  "validFrom" : "2023-03-21T15:35:08Z",
  "credentialSubject": {
    "id": "did:example:123",
    "degree": {
      "name": "Bachelor of Science and Arts",
      "type": "BachelorDegree"
    }
  },
  "proof" : {
    "type" : "JsonWebSignature2020",
    "creator" : "did:example:456",
    "created" : "2023-03-21T15:35:08Z",
    "verificationMethod" : "did:example:456",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..zDI3Wc6jWN7288tlat3LohWsoZiIkBODvlmLPtCy49vUZxpv1NYtZNCMd5Z4RxVQSSbkjPSDzDfAmlOBLhUZBg"
  }
}
```

This Verifiable Diploma includes the following key elements:

* `"type"`: Defines the credential as both a general "VerifiableCredential" and a more specific "UniversityDegreeCredential".
* `"@context"`: Provides references to the necessary standards and examples for interpreting the credential.
* `"id"`: A unique identifier for the credential.
* `"issuer"`: The DID of the university issuing the diploma (e.g., "did:example:456").
* `"issuanceDate"`: The timestamp indicating when the credential was issued.
* `"issued"`: The timestamp indicating when the credential was issued.
* `"validFrom"`: The timestamp indicating from when the credential is valid.
* `"credentialSubject"`: Contains the DID of the credential holder (Emma - e.g., "did:example:123") and the details of the degree earned, such as the name of the degree and its type.
* `proof`: The proof object contains the digital signature and related information that is used to verify the authenticity and integrity of the Verifiable Credential.
  * `type`: "JsonWebSignature2020" indicates the cryptographic suite used for generating the digital signature. In this case, it's the JSON Web Signature (JWS) standard based on the Ed25519 signature algorithm.
  * `creator`: "did:example:456" is the DID of the entity that created the digital signature, in this case, the issuer of the Verifiable Credential.
  * `created`: "2023-03-21T15:35:08Z" is the timestamp when the digital signature was created. It is in the ISO 8601 format.
  * `verificationMethod`: "did:example:456" is the identifier for the public key or cryptographic method used to verify the digital signature.
  * `jws`: is the actual digital signature (JWS) generated using the Ed25519 algorithm. This signature is used to verify the authenticity and integrity of the Verifiable Credential.

Now that we know how the credential looks like, let's issue it.

\
**Issue**

{% tabs %}
{% tab title="REST API" %}
```bash
curl -X 'POST' \
  'http://localhost:7001/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "templateId": "{template type}",
  "config": {
    "issuerDid": "{issuerDid}",
    "subjectDid": "{subjectDid}",
    "proofType": "{proofType}"
  },
  "credentialData": {
    "id": "{subjectDid}",
    "degree": {
      "name": "{Degree name}",
      "type": "{Degree type}"
    }
  }
}'
```

**Body Parameters**

* `templateId`: _**\[string]**_ The identifier of the template used for issuing a Verifiable Credential. This template defines the structure and format of the credential being issued.
* `config`: _**\[object]**_ Contains configuration parameters for the issuance process.
  * `issuerDid`: _**\[string]**_ The DID of the entity issuing the credential (University).
  * `subjectDid`: _**\[string]**_ The DID of the entity receiving the credential (Emma).
  * `proofType`: _**\[string]**_ Specifies the format and cryptographic algorithm used for the digital signature of the Verifiable Credential. E.g. LD\_PROOF
* `credentialData`: _**\[object]**_ Contains the actual data of the credential being issued.
  * `credentialSubject`: _**\[object]**_ Holds the information about the credential holder and the earned degree.
    * `id`: _**\[string]**_ The DID of the credential holder, identical to the `subjectDid` in the `config` object.
    * `degree`: _**\[object]**_ Contains details of the degree earned by the credential holder.
      * `name`: _**\[string]**_ The name of the earned degree (e.g., "Bachelor of Science and Arts").
      * `type`: _**\[string]**_ The type of the earned degree (e.g., "BachelorDegree").

**Example:**

```bash
curl -X 'POST' \
  'http://localhost:7001/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "templateId": "UniversityDegree",
  "config": {
    "issuerDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "subjectDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "proofType": "LD_PROOF"
  },
  "credentialData": {
    "id": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "degree": {
      "name": "Bachelor of Science and Arts",
      "type": "BachelorDegree"
    }
  }
}'
```
{% endtab %}
{% endtabs %}

Awesome, you just issued your first VC 🎉. Now Emma can use it to prove her academic credentials to her employer.

#### **Verify The University Degree Credential**

Emma needs to verify her academic credentials to her employer, which involves the following steps performed by the verifier (employer):

1. **Verify the credential's digital signature**: The Verifier checks if the digital signature on the credential is valid and has been signed by the Issuer's private key. This ensures that the credential was indeed issued by the claimed Issuer.
2. **Check the Issuer's DID**: The Verifier validates the Issuer's Decentralized Identifier (DID) by resolving it to a DID Document. This step helps confirm the Issuer's identity and retrieve their public key for signature verification.
3. **Verify the Holder's DID**: The Verifier checks the credential's subject (i.e., the Holder) by validating their DID. This ensures that the credential was issued to the correct entity and prevents unauthorized use of the credential.
4. **Check the credential's status**: (Not for our use-case) The Verifier may also query the credential's status on a registry, ledger, or another trusted source. This step helps confirm whether the credential is still valid or has been revoked by the Issuer.
5. **Check the credential's integrity**: The Verifier confirms that the credential data has not been tampered with since issuance. This is typically done by comparing the signed data with the credential's content to detect any discrepancies.
6. **Verify the credential's issuance and expiration dates**: The Verifier checks the issuance and expiration dates (if applicable) of the credential to ensure it was issued within the specified time frame and is still valid.

\
To verify the credential, we will be using the [Auditor API](http://localhost:7003/v1/swagger#/Verification%20Policies/verifyVP) endpoint.

{% tabs %}
{% tab title="REST API" %}
```bash
curl -X 'POST' \
  'http://localhost:7003/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "policies": [
    {
      "policy": "SignaturePolicy"
    }
  ],
  "credentials": [{Emma's Credential}]
}'
```

\
\
**Example**

```bash
curl -X 'POST' \
  'http://localhost:7003/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "policies": [
    {
      "policy": "SignaturePolicy"
    }
  ],
  "credentials": [
    {
      "type": [
        "VerifiableCredential",
        "UniversityDegreeCredential"
      ],
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
      ],
      "id": "urn:uuid:a78bcd04-183b-4e57-91fe-954cb8dc6a04",
      "issuer": {
        "id": "did:key:z6MkgjQxcoh1JWXMgG7xPNeBaqUXWu42LAW8G5KmE7J6d1CG"
      },
      "issuanceDate": "2023-03-21T15:54:16Z",
      "issued": "2023-03-21T15:54:16Z",
      "validFrom": "2023-03-21T15:54:16Z",
      "credentialSubject": {
        "id": "did:key:z6MkgjQxcoh1JWXMgG7xPNeBaqUXWu42LAW8G5KmE7J6d1CG",
        "degree": {
          "name": "Bachelor of Science and Arts",
          "type": "BachelorDegree"
        }
      },
      "degree": {
        "name": "Bachelor of Science and Arts",
        "type": "BachelorDegree"
      },
      "proof": {
        "type": "JsonWebSignature2020",
        "creator": "did:key:z6MkgjQxcoh1JWXMgG7xPNeBaqUXWu42LAW8G5KmE7J6d1CG",
        "created": "2023-03-21T15:54:16Z",
        "verificationMethod": "did:key:z6MkgjQxcoh1JWXMgG7xPNeBaqUXWu42LAW8G5KmE7J6d1CG#z6MkgjQxcoh1JWXMgG7xPNeBaqUXWu42LAW8G5KmE7J6d1CG",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..9LiRH2WXqAWIgA54PJ3Qt6ECOSykuU2b_n7UTA-2otZqX-sNP79VgZ5cBlLZeUTis90pAtsRS5uoAblxWjwcDg"
      }
    }
  ]
}'
```
{% endtab %}
{% endtabs %}

You have successfully issued and verified a Verifiable Credential. Great job!! Emma can start her new job 🎉\
\
**Where to go next?**

1. Exploring ssi-kit Capabilities - Familiarize yourself with the various features of ssi-kit by reviewing the [REST API](../getting-started/rest-apis.md) or [Command Line](../getting-started/cli-command-line-interface.md) section.
2. [Understanding Verification Policies](../usage-examples/verifiable-credentials/verification-policies.md) - Discover the potential applications of Verification Policies and how they can be useful for your particular use-case.
3. [Exploring Supported Ecosystems](../what-is-the-ssi-kit/ssi-kit/architecture/ecosystem-abstraction.md) - Visit our ecosystem overview page to explore the different ecosystems (did:methods) that we support.
