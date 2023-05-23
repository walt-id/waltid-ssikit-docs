---
description: 'Learn about did:web: what it is and how to create one.'
---

# DID Web

## What is a DID Web

Following the foundational principles defined in the DID specification. DIDs are globally unique, self-sovereign identifiers for individuals, companies, and devices, and they come in various forms, called DID methods. Those methods define the protocol for creating, reading, updating and deactivating DIDs for the target network or system. This could be a blockchain, like in the case of did:ethr or a DNS and HTTP-based systems as it is for did:web.&#x20;

did:web therefore is one protocol defining the rules on how to work with Decentralised Identifiers in the DNS system, blending decentralised identity principles with the traditional web and HTTP. Allowing domain owners to create, manage and expose their DID document, the public accessible part of their DID, under a domain they own. The major advantage of did:web is that it relies on the already established and widely used web and its standards, making the adoption and implementation process much simpler for companies. Instead of having to learn a whole new system, they can build on the existing knowledge and infrastructure they already have.\
\
Though one limitation of DID web is, that the security is fundamentally dependent on the safety of the website hosting the DID Document.

### **How a DID web looks like**

In practice, a DID Web looks like a regular URL but following the form standards of a DID **`did:<method>:<method-specific-string>`** If we decided to host one at walt.id, it would be accessible via [https://walt.id/.well-known/did.json](https://walt.id/.well-known/did.json) and defined as **`did:web:walt.id`**.

What is also possible, to define sub paths at which the DID document should be hosted, e.g. for `did:web:walt.id:user:alice` the DID document would be hosted at [https://walt.id/.well-known/user/alice/did.json](https://walt.id/user/alice/did.json)



## **Creating a DID Web**

Use the latest version of the walt.id SSI-Kits CLI to create a did:web. Refer to the [Getting Started guide](../getting-started/cli-command-line-interface.md) for instructions on how to run the project. Let's now create a did:web

#### Create a DID web via the SSI-Kit CLI

{% tabs %}
{% tab title="CLI" %}
Make sure you have set the aslias as explaind in [the setup](../getting-started/cli-command-line-interface.md), otherwise the ssikit command will not be defined in your terminal.

```bash
ssikit did create -m {method} --domain {domain} --path {domainPath}
```

**Flags**

* `m`: _\[string]_ specifiying the did method. Options `web`, `key`, `cheqd`, `ebsi` and others. See full list [here](https://walt-id.notion.site/Features-by-Product-aab646e46a744a7d84a6b8fd6b7066ac#7797d15830af4d148acfa57bdd20c716).
* `domain (optional):` _\[string]_ the domain you want to host your did:web under.
* `path (optional):` _\[string]_ location of the hosted DID document

**Example**

```bash
ssikit did create -m web --domain example.com --path user/alice
```

\
**Response**

```json
DID created: did:web:example.com


DID document (below, JSON):

{
    "assertionMethod" : [
        "did:web:example.com:user:alice#48e92d043c93484c86a295f5115dc3c4"
    ],
    "authentication" : [
        "did:web:example.com:user:alice#48e92d043c93484c86a295f5115dc3c4"
    ],
    "@context" : "https://www.w3.org/ns/did/v1",
    "id" : "did:web:example.com:user:alice",
    "verificationMethod" : [
        {
            "controller" : "did:web:example.com:user:alice",
            "id" : "did:web:example.com:user:alice#48e92d043c93484c86a295f5115dc3c4",
            "publicKeyJwk" : {
                "alg" : "EdDSA",
                "crv" : "Ed25519",
                "kid" : "48e92d043c93484c86a295f5115dc3c4",
                "kty" : "OKP",
                "use" : "sig",
                "x" : "GGH7EC9dZPX-5aE-Pf3ggkppz_wecrs_n2TYNhX4rY0"
            },
            "type" : "Ed25519VerificationKey2019"
        }
    ]
}

Install this did:web at: https://example.com/.well-known/user/alice/did.json
```

You can now take the DID document, and upload it to your server on the specified domain path provided by the ouput (https://example.com/.well-known/user/alice/did.json) or if you did not use a sub-path the domain would be something like (https://yourdomain.com/.well-known/did.json)
{% endtab %}
{% endtabs %}



### **Hosting a DID Web via the Wallet-Kit**

If you want to get the hosting right out of the box, you can deploy another product of ours, the Wallet-Kit, which builds on top of the SSI-Kit. With it, you can generate a did without specifying any domain and this will create a did:web for the domain the Wallet-Kit is hosted under and expose the DID Document on the right path automatically. \
\
You can try it out, by either using the [REST interface](did-web.md#create-a-did-web-via-wallet-kit-rest) of your hosted Wallet-Kit or by visiting our web wallet and creating your first did:web [via the UI](did-web.md#create-a-did-web-via-walt.id-web-wallet).&#x20;



#### Create a DID web via Wallet-Kit REST

Use the latest version of the walt.id Wallet-Kits REST interface to create a did:web. Refer to the [Getting Started guide](https://docs.walt.id/v/web-wallet/getting-started/rest-apis) for instructions on how to serve the API. Let's now create a did:web

{% tabs %}
{% tab title="REST" %}
```bash
curl -X 'POST' \
  'http://0.0.0.0:8080/issuer-api/default/config/did/createAdvanced' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "web"
}'
```

**Body paramters**

* `method`: _\[string]_ specifiying the did method. Options `web`,  `ebsi` and others. See full list [here](https://walt-id.notion.site/Features-by-Product-aab646e46a744a7d84a6b8fd6b7066ac#7797d15830af4d148acfa57bdd20c716).
* `domain (optiona):` _\[string]_ the domain you want to host your did:web under.
* `path (optional):` _\[string]_ location of the hosted DID document

**Example**

```bash
curl -X 'POST' \
  'http://0.0.0.0:8080/issuer-api/default/config/did/createAdvanced' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "web"
}'
```

**Response**

```
did:web:localhost%3A3000:api:did-registry:a3aa55ad8b9946d2a453a4e1d4c592e6
```
{% endtab %}
{% endtabs %}

####

#### Create a DID web via walt.id web wallet

{% embed url="https://scribehow.com/shared/Walt_Workflow__A6Y-6Kg-QiawVBy06HhqSg" %}

**Resolving your did:web**&#x20;

Using the did you just created via the Wallet UI, you can now use the SSI-Kit to resolve it.\


{% tabs %}
{% tab title="SSI-Kit CLI" %}
Make sure you have set the aslias as explaind in [the setup](../getting-started/cli-command-line-interface.md), otherwise the ssikit command will not be defined in your terminal.

```bash
ssikit did resolve -d {yourDID}
```

**Flags**

* `d`: _\[string]_ did to resolve

**Example**

```bash
ssikit did resolve -d did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb
```

\
**Response**

```json
Resolving DID "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb"...

Results:

DID resolved: "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb"
DID document (below, JSON):

{
    "assertionMethod" : [
        {
            "controller" : "",
            "id" : "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb#3b0fc8a129074fb98d764ec07f6e7aeb",
            "type" : ""
        }
    ],
    "authentication" : [
        {
            "controller" : "",
            "id" : "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb#3b0fc8a129074fb98d764ec07f6e7aeb",
            "type" : ""
        }
    ],
    "@context" : "https://www.w3.org/ns/did/v1",
    "id" : "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb",
    "verificationMethod" : [
        {
            "controller" : "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb",
            "id" : "did:web:wallet.walt.id:api:did-registry:3b0fc8a129074fb98d764ec07f6e7aeb#3b0fc8a129074fb98d764ec07f6e7aeb",
            "publicKeyJwk" : {
                "alg" : "EdDSA",
                "crv" : "Ed25519",
                "kid" : "3b0fc8a129074fb98d764ec07f6e7aeb",
                "kty" : "OKP",
                "use" : "sig",
                "x" : "nqwNGCV1myawqNqBcT1mEEA5M80sCoGSqiwAFb2ED-4"
            },
            "type" : "Ed25519VerificationKey2019"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

