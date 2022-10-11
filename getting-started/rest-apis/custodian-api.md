---
description: >-
  Custodian REST API functions.
---

# Custodian API
[Swagger](https://custodian.ssikit.walt.id/v1/swagger) | [Redoc](https://custodian.ssikit.walt.id/v1/redoc)

The _Custodian API_ provides management functions for maintaining secrets and sensitive data (e.g. keys, Verifiable Credentials) in a secure way:
* [Key](custodian-api.md#key-management)
* [DID](custodian-api.md#did-management)
* [Credentials](custodian-api.md#credentials-management)

## Key management
Key management functions include:
* [List](custodian-api.md#list-keys) - lists the available keys
* [Load](custodian-api.md#load-key) - loads a key specified by its alias
* [Generate](custodian-api.md#generate-key) - generate a key using the specified algorithm
* [Import](custodian-api.md#import-key) - imports a key
* [Delete](custodian-api.md#delete-key) - deletes a specific key
* [Export](custodian-api.md#export-key) - exports public and private key parts (if supported by the underlying keystore)

### List keys
The `/keys` endpoint lists the key available to the Custodian

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/keys' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "list":
    [
        {
            "algorithm": "string",
            "cryptoProvider": "string",
            "keyId":
            {
                "id": "string"
            },
            "keyPair": {},
            "keysetHandle": null
        }
    ]
}
```
{% endtab %}
{% endtabs %}

E.g. List the available keys

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/keys' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "list":
    [
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "e548f032cadf4145ab6886a57c2e87e6"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "e70e8fd8932043caa7c857c3b944d0e0"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "b50db0c1f73242b8bb0f2f6324e15ec3"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "8cc0b1707ea345ed83e479469d42aac2"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "did:key:z6Mkv58vGsBMwbiyQ3P93MRnYfRgGvn4STEEsj5hFHYe51wu#z6Mkv58vGsBMwbiyQ3P93MRnYfRgGvn4STEEsj5hFHYe51wu"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "186a1e0a6d42459ba902724fe7643ed4"
            },
            "keyPair": {},
            "keysetHandle": null
        },
        {
            "algorithm": "EdDSA_Ed25519",
            "cryptoProvider": "SUN",
            "keyId":
            {
                "id": "c5b11445be0e4d37863170df3328630b"
            },
            "keyPair": {},
            "keysetHandle": null
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Load key
The `/keys/{alias}` endpoint loads a key specified by its alias.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/keys/{alias}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "algorithm": "string",
    "cryptoProvider": "string",
    "keyId":
    {
        "id": "string"
    },
    "keyPair": {},
    "keysetHandle": null
}
```
{% endtab %}
{% endtabs %}

E.g. Load a key with `id` _e548f032cadf4145ab6886a57c2e87e6_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/keys/e548f032cadf4145ab6886a57c2e87e6' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "algorithm": "EdDSA_Ed25519",
    "cryptoProvider": "SUN",
    "keyId":
    {
        "id": "e548f032cadf4145ab6886a57c2e87e6"
    },
    "keyPair": {},
    "keysetHandle": null
}
```
{% endtab %}
{% endtabs %}

### Generate key
The `/keys/generate` endpoint generates a key using the specified algorithm.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/generate' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "keyAlgorithm": "EdDSA_Ed25519"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "algorithm": "string",
    "cryptoProvider": "string",
    "keyId":
    {
        "id": "string"
    },
    "keyPair": {},
    "keysetHandle": null
}
```
{% endtab %}
{% endtabs %}

E.g. Generate a key using the _EdDSA_Ed25519_ algorithm.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/generate' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{ "keyAlgorithm": "EdDSA_Ed25519" }'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "keyAlgorithm": "EdDSA_Ed25519"
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "algorithm": "EdDSA_Ed25519",
    "cryptoProvider": "SUN",
    "keyId":
    {
        "id": "8394ea7883bc4328a3f18b146b7e16bd"
    },
    "keyPair": {},
    "keysetHandle": null
}
```
{% endtab %}
{% endtabs %}

### Import key
The `/keys/import` endpoint imports a key (_JWK_ or _PEM_ format) to the underlying keystore.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
The key string in JWK or PEM format
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "id": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Import a public key specified in JWK format.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{"kty":"OKP","use":"sig","crv":"Ed25519","kid":"bc6fa6b0593648238c4616800bed7746","x":"YyswAyRO2Aur8Jmzc8aOvI3AWFka3ZynJwB84a0FJVU","alg":"EdDSA"}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "kty": "OKP",
    "use": "sig",
    "crv": "Ed25519",
    "kid": "bc6fa6b0593648238c4616800bed7746",
    "x": "YyswAyRO2Aur8Jmzc8aOvI3AWFka3ZynJwB84a0FJVU",
    "alg": "EdDSA"
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "id": "bc6fa6b0593648238c4616800bed7746"
}
```
{% endtab %}
{% endtabs %}

### Delete key
The `/keys/{id}` deletes the specified as parameter:
* id path parameter (required) - the key alias

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/keys/{id}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Delete the key with `id` _bc6fa6b0593648238c4616800bed7746_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/keys/bc6fa6b0593648238c4616800bed7746' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

### Export key
The `/keys/export` endpoint exports a key.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/export' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "keyAlias": "string",
    "format": "JWK",
    "exportPrivate": true
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
The key in the specified format, JWK or PEM
```
{% endtab %}
{% endtabs %}

E.g. Export the public key with id = _e548f032cadf4145ab6886a57c2e87e6_ as _JWK_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/keys/export' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyAlias": "e548f032cadf4145ab6886a57c2e87e6",
  "format": "JWK",
  "exportPrivate": false
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "keyAlias": "e548f032cadf4145ab6886a57c2e87e6",
    "format": "JWK",
    "exportPrivate": false
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "kty": "OKP",
    "use": "sig",
    "crv": "Ed25519",
    "kid": "e548f032cadf4145ab6886a57c2e87e6",
    "x": "jT8YleOQnaABpZTnvId3WoID4Pia9Lex9OndqQ22Xxs",
    "alg": "EdDSA"
}
```
{% endtab %}
{% endtabs %}

## DID management
DID management functions enable the following:
* [List](custodian-api.md#list-did) - lists the available DIDs
* [Load](custodian-api.md#load-did) - loads a DID by the specified id
* [Delete](custodian-api.md#delete-did) - deletes a DID by the specified url
* [Create](custodian-api.md#create-did) - creates a new DID
* [Resolve](custodian-api.md#resolve-did) - resolves a DID to a document
* [Import](custodian-api.md#import-did) - import a DID

### List DID
The `/did` endpoint lists the available DIDs.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/did' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
The list of DID strings
```
{% endtab %}
{% endtabs %}

E.g. List the available DIDs

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/did' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
[
    "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "did:web:my.domain",
    "did:web:walt.id",
    "did:key:z6Mkv58vGsBMwbiyQ3P93MRnYfRgGvn4STEEsj5hFHYe51wu"
]
```
{% endtab %}
{% endtabs %}

### Load DID
The `/did/{id}` endpoint loads a DID specified by:
* id path parameter (required) - the DID url string

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/{id}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "assertionMethod":
    [
        "string"
    ],
    "authentication":
    [
        "string"
    ],
    "@context":
    [
        "string"
    ],
    "id": "string",
    "verificationMethod":
    [
        {
            "controller": "string",
            "id": "string",
            "publicKeyJwk":
            {
                "alg": "string",
                "crv": "string",
                "kid": "string",
                "kty": "string",
                "use": "string",
                "x": "string"
            },
            "type": "string"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

E.g Load the DID having the id = _did:web:walt.id_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/did/did%3Aweb%3Awalt.id' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "assertionMethod":
    [
        "did:web:walt.id#186a1e0a6d42459ba902724fe7643ed4"
    ],
    "authentication":
    [
        "did:web:walt.id#186a1e0a6d42459ba902724fe7643ed4"
    ],
    "@context":
    [
        "https://www.w3.org/ns/did/v1"
    ],
    "id": "did:web:walt.id",
    "verificationMethod":
    [
        {
            "controller": "did:web:walt.id",
            "id": "did:web:walt.id#186a1e0a6d42459ba902724fe7643ed4",
            "publicKeyJwk":
            {
                "alg": "EdDSA",
                "crv": "Ed25519",
                "kid": "186a1e0a6d42459ba902724fe7643ed4",
                "kty": "OKP",
                "use": "sig",
                "x": "7-ofBq4vt0ePzC5IjiWkqTedfSv7WJJr6-HsQNXsr2M"
            },
            "type": "Ed25519VerificationKey2019"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Delete DID
The `/did/{id}` deletes the DID specified by:
* url - path parameter (required) - the DID url string

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/did/{id}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Delete the DID having id = _did:web:walt.id_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/did/did%3Aweb%3Awalt.id' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

### Create DID
The `/did/create` endpoints creates a DID.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "method": "key",
    "keyAlias": "string",
    "didWebDomain": "string",
    "didWebPath": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
The DID url string
```
{% endtab %}
{% endtabs %}

E.g. Create a DID using the `web` method having the domain set to `walt.id`.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "web",
  "didWebDomain": "walt.id"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "method": "web",
    "didWebDomain": "walt.id"
}
```
{% endtab %}
{% tab title="Response body" %}
```
did:web:walt.id
```
{% endtab %}
{% endtabs %}

### Resolve DID
The `/did/resolve` endpoints resolves a DID.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/resolve' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "did": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "assertionMethod":
    [
        "string"
    ],
    "authentication":
    [
        "string"
    ],
    "@context":
    [
        "string"
    ],
    "id": "string",
    "verificationMethod":
    [
        {
            "controller": "string",
            "id": "string",
            "publicKeyJwk":
            {
                "alg": "string",
                "crv": "string",
                "kid": "string",
                "kty": "string",
                "use": "string",
                "x": "string"
            },
            "type": "string"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

E.g. Reslove the DID having id = _did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/resolve' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "did": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "did": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "assertionMethod":
    [
        "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
    ],
    "authentication":
    [
        "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
    ],
    "capabilityDelegation":
    [
        "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
    ],
    "capabilityInvocation":
    [
        "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX"
    ],
    "@context":
    [
        "https://www.w3.org/ns/did/v1"
    ],
    "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "keyAgreement":
    [
        "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6LShXhgLqK3vQX3eg18gwZUYNtt6M6FjPqpV1eQD86m8Hwh"
    ],
    "verificationMethod":
    [
        {
            "controller": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
            "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
            "publicKeyBase58": "6tW7uQ6c3YgZDoCFbHMB6QFjPENyHRouTUwGnLv36wS9",
            "type": "Ed25519VerificationKey2019"
        },
        {
            "controller": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
            "id": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6LShXhgLqK3vQX3eg18gwZUYNtt6M6FjPqpV1eQD86m8Hwh",
            "publicKeyBase58": "6rXWpXWBpwoJZHdNAJ3XDngQFCZ92nffc2viifTEQvAw",
            "type": "X25519KeyAgreementKey2019"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Import DID
The `/did/import` endpoint resolves and imports the DID to the underlying data store.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
The DID url string.
{% endtab %}
{% tab title="Response body schema" %}
```
Code 201
```
{% endtab %}
{% endtabs %}

E.g. Import DID having id = _did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z'
```
{% endtab %}
{% tab title="Request body" %}
```
did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z
```
{% endtab %}
{% endtabs %}

## Credentials management
The following functions are available for credentials management:
* [List](custodian-api.md#list-credentials) - lists the available credentials
* [List compact](custodian-api.md#list-credentials-compact) - lists credential ids
* [Load](custodian-api.md#load-credential) - loads a credential by id
* [Store](custodian-api.md#store-credential) - store a credential
* [Delete](custodian-api.md#delete-credential) - delete a credential by id
* [Present](custodian-api.md#present-credential) - create a verifiable presentation from specific credentials
* [Present stored](custodian-api.md#present-stored-credential) - create a verifiable presentation from specific stored credential ids

### List credentials
The `/credentials` endpoint lists the available credentials:
* id - query parameter (optional) - the list of credentials ids

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
The list of credentials
```
{% endtab %}
{% endtabs %}

E.g. List the the credentials having ids _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_ and _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84271_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials?id=urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270&id=urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84271' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "list":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://www.w3.org/2018/credentials/examples/v1"
            ],
            "credentialSubject":
            {
                "degree":
                {
                    "name": "Bachelor of Science and Arts",
                    "type": "BachelorDegree"
                },
                "id": "did:web:my.domain"
            },
            "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
            "issued": "2022-10-07T09:53:41.369913097Z",
            "issuer":
            {
                "id": "did:web:walt.id"
            },
            "proof":
            {
                "created": "2022-10-07T09:53:41Z",
                "creator": "did:web:walt.id",
                "domain": "https://api.preprod.ebsi.eu",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
                "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
                "type": "Ed25519Signature2018"
            },
            "validFrom": "2022-10-07T09:53:41.369917079Z",
            "issuanceDate": "2022-10-07T09:53:41.369917079Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### List credentials compact
The `/credentials/list/credentialIds` lists the available credentials ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/list/credentialIds' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
The list of credentials ids
```
{% endtab %}
{% endtabs %}

E.g. List the available credentials ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/list/credentialIds' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "list":
    [
        "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
    ]
}
```
{% endtab %}
{% endtabs %}

### Load credential
The `/credentials/{id}` loads a credential specified by:
* id - path parameter (required) - the credential id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/{id}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
The credential string
```
{% endtab %}
{% endtabs %}

E.g. Load the credential having id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
    ],
    "credentialSubject":
    {
        "degree":
        {
            "name": "Bachelor of Science and Arts",
            "type": "BachelorDegree"
        },
        "id": "did:web:my.domain"
    },
    "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
    "issued": "2022-10-07T09:53:41.369913097Z",
    "issuer":
    {
        "id": "did:web:walt.id"
    },
    "proof":
    {
        "created": "2022-10-07T09:53:41Z",
        "creator": "did:web:walt.id",
        "domain": "https://api.preprod.ebsi.eu",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "type": "Ed25519Signature2018"
    },
    "validFrom": "2022-10-07T09:53:41.369917079Z",
    "issuanceDate": "2022-10-07T09:53:41.369917079Z",
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ]
}
```
{% endtab %}
{% endtabs %}

### Store credential
The `/credentials/{alias}` endpoint stores a verifiable credential by:
* alias - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'PUT' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
The body should contain, the VC to be store. If no adjustments are required to VC, then the body can be the VC itself (e.g. the one received from the create VC endpoint).
```
{
    "json": "string",
    "issuanceDate": "string",
    "dateFormat":
    {
        "locale":
        {
            "language": "string",
            "script": "string",
            "variant": "string",
            "displayName": "string",
            "country": "string",
            "unicodeLocaleAttributes":
            [
                "string"
            ],
            "unicodeLocaleKeys":
            [
                "string"
            ],
            "displayLanguage": "string",
            "displayScript": "string",
            "displayCountry": "string",
            "displayVariant": "string",
            "extensionKeys":
            [
                "string"
            ],
            "iso3Language": "string",
            "iso3Country": "string"
        },
        "decimalStyle":
        {
            "zeroDigit": "string",
            "positiveSign": "string",
            "negativeSign": "string",
            "decimalSeparator": "string"
        },
        "resolverStyle": "STRICT",
        "resolverFields":
        [
            {
                "baseUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "rangeUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "dateBased": true,
                "timeBased": true
            }
        ],
        "zone":
        {
            "id": "string",
            "rules":
            {
                "fixedOffset": true,
                "transitions":
                [
                    {
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "duration":
                        {
                            "seconds": 0,
                            "nano": 0,
                            "negative": true,
                            "zero": true,
                            "units":
                            [
                                {
                                    "dateBased": true,
                                    "timeBased": true,
                                    "durationEstimated": true
                                }
                            ]
                        },
                        "gap": true,
                        "dateTimeBefore": "2022-10-09T09:09:41.896Z",
                        "dateTimeAfter": "2022-10-09T09:09:41.896Z",
                        "overlap": true,
                        "instant": "2022-10-09T09:09:41.896Z"
                    }
                ],
                "transitionRules":
                [
                    {
                        "month": "JANUARY",
                        "timeDefinition": "UTC",
                        "standardOffset":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "dayOfWeek": "MONDAY",
                        "dayOfMonthIndicator": 0,
                        "localTime":
                        {
                            "hour": 0,
                            "minute": 0,
                            "second": 0,
                            "nano": 0
                        },
                        "midnightEndOfDay": true
                    }
                ]
            }
        },
        "chronology":
        {
            "id": "string",
            "calendarType": "string"
        }
    },
    "jwt": "string",
    "id": "string",
    "type":
    [
        "string"
    ],
    "subject": "string",
    "expirationDate": "string",
    "credentialSchema":
    {
        "id": "string",
        "type": "string"
    },
    "proof":
    {
        "type": "string",
        "creator": "string",
        "created": "string",
        "domain": "string",
        "proofPurpose": "string",
        "verificationMethod": "string",
        "jws": "string",
        "nonce": "string"
    },
    "challenge": "string",
    "validFrom": "string",
    "issued": "string",
    "issuer": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 201
```
{% endtab %}
{% endtabs %}

E.g. Store the `UniversityDegree` verifiable credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'PUT' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "@context" : [ "https://www.w3.org/2018/credentials/v1", "https://www.w3.org/2018/credentials/examples/v1" ],
  "credentialSubject" : {
    "degree" : {
      "name" : "Bachelor of Science and Arts",
      "type" : "BachelorDegree"
    },
    "id" : "did:web:my.domain"
  },
  "id" : "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
  "issued" : "2022-10-07T09:53:41.369913097Z",
  "issuer" : {
    "id" : "did:web:walt.id"
  },
  "validFrom" : "2022-10-07T09:53:41.369917079Z",
  "issuanceDate" : "2022-10-07T09:53:41.369917079Z",
  "type" : [ "VerifiableCredential", "UniversityDegreeCredential" ],
  "proof" : {
    "type" : "Ed25519Signature2018",
    "creator" : "did:web:walt.id",
    "created" : "2022-10-07T09:53:41Z",
    "domain" : "https://api.preprod.ebsi.eu",
    "nonce" : "dc2be572-cca4-43dc-9903-0fec1dcf786f",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ"
  }
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
    ],
    "credentialSubject":
    {
        "degree":
        {
            "name": "Bachelor of Science and Arts",
            "type": "BachelorDegree"
        },
        "id": "did:web:my.domain"
    },
    "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
    "issued": "2022-10-07T09:53:41.369913097Z",
    "issuer":
    {
        "id": "did:web:walt.id"
    },
    "validFrom": "2022-10-07T09:53:41.369917079Z",
    "issuanceDate": "2022-10-07T09:53:41.369917079Z",
    "type":
    [
        "VerifiableCredential",
        "UniversityDegreeCredential"
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:walt.id",
        "created": "2022-10-07T09:53:41Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ"
    }
}
```
{% endtab %}
{% endtabs %}

### Delete credential
The `/credentials/{alias}` deletes a credential by:
* alias - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/credentials/{alias}' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Request body schema" %}
```
No parameters
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Delete the credential with id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://custodian.ssikit.walt.id/credentials/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

### Present credential
The `/credentials/present` endpoint creates a verifiable presentation from the specified credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "vcs":
    [
        "string"
    ],
    "holderDid": "string",
    "verifierDid": "string",
    "domain": "string",
    "challenge": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "context":
    [
        "string"
    ],
    "id": "string",
    "holder": "string",
    "verifiableCredential":
    [
        {
            "json": "string",
            "issuanceDate": "string",
            "dateFormat":
            {
                "locale":
                {
                    "language": "string",
                    "script": "string",
                    "variant": "string",
                    "displayName": "string",
                    "country": "string",
                    "unicodeLocaleAttributes":
                    [
                        "string"
                    ],
                    "unicodeLocaleKeys":
                    [
                        "string"
                    ],
                    "displayLanguage": "string",
                    "displayScript": "string",
                    "displayCountry": "string",
                    "displayVariant": "string",
                    "extensionKeys":
                    [
                        "string"
                    ],
                    "iso3Language": "string",
                    "iso3Country": "string"
                },
                "decimalStyle":
                {
                    "zeroDigit": "string",
                    "positiveSign": "string",
                    "negativeSign": "string",
                    "decimalSeparator": "string"
                },
                "resolverStyle": "STRICT",
                "resolverFields":
                [
                    {
                        "baseUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "rangeUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "dateBased": true,
                        "timeBased": true
                    }
                ],
                "zone":
                {
                    "id": "string",
                    "rules":
                    {
                        "fixedOffset": true,
                        "transitions":
                        [
                            {
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "duration":
                                {
                                    "seconds": 0,
                                    "nano": 0,
                                    "negative": true,
                                    "zero": true,
                                    "units":
                                    [
                                        {
                                            "dateBased": true,
                                            "timeBased": true,
                                            "durationEstimated": true
                                        }
                                    ]
                                },
                                "gap": true,
                                "dateTimeBefore": "2022-10-09T11:30:48.206Z",
                                "dateTimeAfter": "2022-10-09T11:30:48.206Z",
                                "overlap": true,
                                "instant": "2022-10-09T11:30:48.206Z"
                            }
                        ],
                        "transitionRules":
                        [
                            {
                                "month": "JANUARY",
                                "timeDefinition": "UTC",
                                "standardOffset":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "dayOfWeek": "MONDAY",
                                "dayOfMonthIndicator": 0,
                                "localTime":
                                {
                                    "hour": 0,
                                    "minute": 0,
                                    "second": 0,
                                    "nano": 0
                                },
                                "midnightEndOfDay": true
                            }
                        ]
                    }
                },
                "chronology":
                {
                    "id": "string",
                    "calendarType": "string"
                }
            },
            "jwt": "string",
            "id": "string",
            "type":
            [
                "string"
            ],
            "subject": "string",
            "expirationDate": "string",
            "credentialSchema":
            {
                "id": "string",
                "type": "string"
            },
            "proof":
            {
                "type": "string",
                "creator": "string",
                "created": "string",
                "domain": "string",
                "proofPurpose": "string",
                "verificationMethod": "string",
                "jws": "string",
                "nonce": "string"
            },
            "challenge": "string",
            "validFrom": "string",
            "issued": "string",
            "issuer": "string"
        }
    ],
    "proof":
    {
        "type": "string",
        "creator": "string",
        "created": "string",
        "domain": "string",
        "proofPurpose": "string",
        "verificationMethod": "string",
        "jws": "string",
        "nonce": "string"
    },
    "issued": "string",
    "validFrom": "string",
    "expirationDate": "string",
    "json": "string",
    "issuanceDate": "string",
    "dateFormat":
    {
        "locale":
        {
            "language": "string",
            "script": "string",
            "variant": "string",
            "displayName": "string",
            "country": "string",
            "unicodeLocaleAttributes":
            [
                "string"
            ],
            "unicodeLocaleKeys":
            [
                "string"
            ],
            "displayLanguage": "string",
            "displayScript": "string",
            "displayCountry": "string",
            "displayVariant": "string",
            "extensionKeys":
            [
                "string"
            ],
            "iso3Language": "string",
            "iso3Country": "string"
        },
        "decimalStyle":
        {
            "zeroDigit": "string",
            "positiveSign": "string",
            "negativeSign": "string",
            "decimalSeparator": "string"
        },
        "resolverStyle": "STRICT",
        "resolverFields":
        [
            {
                "baseUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "rangeUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "dateBased": true,
                "timeBased": true
            }
        ],
        "zone":
        {
            "id": "string",
            "rules":
            {
                "fixedOffset": true,
                "transitions":
                [
                    {
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "duration":
                        {
                            "seconds": 0,
                            "nano": 0,
                            "negative": true,
                            "zero": true,
                            "units":
                            [
                                {
                                    "dateBased": true,
                                    "timeBased": true,
                                    "durationEstimated": true
                                }
                            ]
                        },
                        "gap": true,
                        "dateTimeBefore": "2022-10-09T11:30:48.207Z",
                        "dateTimeAfter": "2022-10-09T11:30:48.207Z",
                        "overlap": true,
                        "instant": "2022-10-09T11:30:48.207Z"
                    }
                ],
                "transitionRules":
                [
                    {
                        "month": "JANUARY",
                        "timeDefinition": "UTC",
                        "standardOffset":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "dayOfWeek": "MONDAY",
                        "dayOfMonthIndicator": 0,
                        "localTime":
                        {
                            "hour": 0,
                            "minute": 0,
                            "second": 0,
                            "nano": 0
                        },
                        "midnightEndOfDay": true
                    }
                ]
            }
        },
        "chronology":
        {
            "id": "string",
            "calendarType": "string"
        }
    },
    "jwt": "string",
    "type":
    [
        "string"
    ],
    "subject": "string",
    "credentialSchema":
    {
        "id": "string",
        "type": "string"
    },
    "issuer": "string",
    "challenge": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Create a verifiable presentation from the provided _VeriafiableID_ and _OpenBadgeCredential_ credentials for a holder with did = _did:web:my.domain_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcs": [
"{\r\n    \"@context\":\r\n    [\r\n        \"https:\/\/www.w3.org\/2018\/credentials\/v1\"\r\n    ],\r\n    \"credentialSchema\":\r\n    {\r\n        \"id\": \"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\r\n        \"type\": \"FullJsonSchemaValidator2021\"\r\n    },\r\n    \"credentialSubject\":\r\n    {\r\n        \"currentAddress\":\r\n        [\r\n            \"1 Boulevard de la Libert\u00E9, 59800 Lille\"\r\n        ],\r\n        \"dateOfBirth\": \"1993-04-08\",\r\n        \"familyName\": \"DOE\",\r\n        \"firstName\": \"Jane\",\r\n        \"gender\": \"FEMALE\",\r\n        \"id\": \"did:web:my.domain\",\r\n        \"nameAndFamilyNameAtBirth\": \"Jane DOE\",\r\n        \"personalIdentifier\": \"0904008084H\",\r\n        \"placeOfBirth\": \"LILLE, FRANCE\"\r\n    },\r\n    \"evidence\":\r\n    [\r\n        {\r\n            \"documentPresence\":\r\n            [\r\n                \"Physical\"\r\n            ],\r\n            \"evidenceDocument\":\r\n            [\r\n                \"Passport\"\r\n            ],\r\n            \"subjectPresence\": \"Physical\",\r\n            \"type\":\r\n            [\r\n                \"DocumentVerification\"\r\n            ],\r\n            \"verifier\": \"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"\r\n        }\r\n    ],\r\n    \"id\": \"urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a\",\r\n    \"issued\": \"2022-10-09T10:11:51Z\",\r\n    \"issuer\": \"did:web:walt.id\",\r\n    \"validFrom\": \"2022-10-09T10:11:51Z\",\r\n    \"issuanceDate\": \"2022-10-09T10:11:51Z\",\r\n    \"type\":\r\n    [\r\n        \"VerifiableCredential\",\r\n        \"VerifiableAttestation\",\r\n        \"VerifiableId\"\r\n    ],\r\n    \"proof\":\r\n    {\r\n        \"type\": \"JsonWebSignature2020\",\r\n        \"creator\": \"did:web:walt.id\",\r\n        \"created\": \"2022-10-09T10:11:52Z\",\r\n        \"proofPurpose\": \"assertionMethod\",\r\n        \"verificationMethod\": \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n        \"jws\": \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA\"\r\n    }\r\n}",
"{\r\n  \"@context\" : [ \"https:\/\/www.w3.org\/2018\/credentials\/v1\", \"https:\/\/w3c-ccg.github.io\/vc-ed\/plugfest-1-2022\/jff-vc-edu-plugfest-1-context.json\" ],\r\n  \"credentialSubject\" : {\r\n    \"achievement\" : {\r\n      \"criteria\" : {\r\n        \"narrative\" : \"The first cohort of the JFF Plugfest 1 in May\/June of 2021 collaborated to push interoperability of VCs in education forward.\",\r\n        \"type\" : \"Criteria\"\r\n      },\r\n      \"description\" : \"This wallet can display this Open Badge 3.0\",\r\n      \"image\" : \"https:\/\/w3c-ccg.github.io\/vc-ed\/plugfest-1-2022\/images\/plugfest-1-badge-image.png\",\r\n      \"name\" : \"Our Wallet Passed JFF Plugfest #1 2022\",\r\n      \"type\" : \"Achievement\"\r\n    },\r\n    \"id\" : \"did:web:my.domain\",\r\n    \"type\" : \"AchievementSubject\"\r\n  },\r\n  \"id\" : \"urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25\",\r\n  \"issuanceDate\" : \"2020-03-10T04:24:12.164Z\",\r\n  \"issued\" : \"2022-10-09T10:12:50Z\",\r\n  \"issuer\" : {\r\n    \"id\" : \"did:web:walt.id\",\r\n    \"image\" : \"https:\/\/kayaelle.github.io\/vc-ed\/plugfest-1-2022\/images\/JFF_LogoLockup.png\",\r\n    \"name\" : \"Jobs for the Future (JFF)\",\r\n    \"type\" : \"Profile\",\r\n    \"url\" : \"https:\/\/kayaelle.github.io\/vc-ed\/plugfest-1-2022\/images\/JFF_LogoLockup.png\"\r\n  },\r\n  \"validFrom\" : \"2022-10-09T10:12:50Z\",\r\n  \"type\" : [ \"VerifiableCredential\", \"OpenBadgeCredential\" ],\r\n  \"proof\" : {\r\n    \"type\" : \"JsonWebSignature2020\",\r\n    \"creator\" : \"did:web:walt.id\",\r\n    \"created\" : \"2022-10-09T10:12:50Z\",\r\n    \"proofPurpose\" : \"assertionMethod\",\r\n    \"verificationMethod\" : \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n    \"jws\" : \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg\"\r\n  }\r\n}"
  ],
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "vcs":
    [
        "{\r\n    \"@context\":\r\n    [\r\n        \"https://www.w3.org/2018/credentials/v1\"\r\n    ],\r\n    \"credentialSchema\":\r\n    {\r\n        \"id\": \"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\r\n        \"type\": \"FullJsonSchemaValidator2021\"\r\n    },\r\n    \"credentialSubject\":\r\n    {\r\n        \"currentAddress\":\r\n        [\r\n            \"1 Boulevard de la Liberté, 59800 Lille\"\r\n        ],\r\n        \"dateOfBirth\": \"1993-04-08\",\r\n        \"familyName\": \"DOE\",\r\n        \"firstName\": \"Jane\",\r\n        \"gender\": \"FEMALE\",\r\n        \"id\": \"did:web:my.domain\",\r\n        \"nameAndFamilyNameAtBirth\": \"Jane DOE\",\r\n        \"personalIdentifier\": \"0904008084H\",\r\n        \"placeOfBirth\": \"LILLE, FRANCE\"\r\n    },\r\n    \"evidence\":\r\n    [\r\n        {\r\n            \"documentPresence\":\r\n            [\r\n                \"Physical\"\r\n            ],\r\n            \"evidenceDocument\":\r\n            [\r\n                \"Passport\"\r\n            ],\r\n            \"subjectPresence\": \"Physical\",\r\n            \"type\":\r\n            [\r\n                \"DocumentVerification\"\r\n            ],\r\n            \"verifier\": \"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"\r\n        }\r\n    ],\r\n    \"id\": \"urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a\",\r\n    \"issued\": \"2022-10-09T10:11:51Z\",\r\n    \"issuer\": \"did:web:walt.id\",\r\n    \"validFrom\": \"2022-10-09T10:11:51Z\",\r\n    \"issuanceDate\": \"2022-10-09T10:11:51Z\",\r\n    \"type\":\r\n    [\r\n        \"VerifiableCredential\",\r\n        \"VerifiableAttestation\",\r\n        \"VerifiableId\"\r\n    ],\r\n    \"proof\":\r\n    {\r\n        \"type\": \"JsonWebSignature2020\",\r\n        \"creator\": \"did:web:walt.id\",\r\n        \"created\": \"2022-10-09T10:11:52Z\",\r\n        \"proofPurpose\": \"assertionMethod\",\r\n        \"verificationMethod\": \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n        \"jws\": \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA\"\r\n    }\r\n}",
        "{\r\n  \"@context\" : [ \"https://www.w3.org/2018/credentials/v1\", \"https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/jff-vc-edu-plugfest-1-context.json\" ],\r\n  \"credentialSubject\" : {\r\n    \"achievement\" : {\r\n      \"criteria\" : {\r\n        \"narrative\" : \"The first cohort of the JFF Plugfest 1 in May/June of 2021 collaborated to push interoperability of VCs in education forward.\",\r\n        \"type\" : \"Criteria\"\r\n      },\r\n      \"description\" : \"This wallet can display this Open Badge 3.0\",\r\n      \"image\" : \"https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/images/plugfest-1-badge-image.png\",\r\n      \"name\" : \"Our Wallet Passed JFF Plugfest #1 2022\",\r\n      \"type\" : \"Achievement\"\r\n    },\r\n    \"id\" : \"did:web:my.domain\",\r\n    \"type\" : \"AchievementSubject\"\r\n  },\r\n  \"id\" : \"urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25\",\r\n  \"issuanceDate\" : \"2020-03-10T04:24:12.164Z\",\r\n  \"issued\" : \"2022-10-09T10:12:50Z\",\r\n  \"issuer\" : {\r\n    \"id\" : \"did:web:walt.id\",\r\n    \"image\" : \"https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png\",\r\n    \"name\" : \"Jobs for the Future (JFF)\",\r\n    \"type\" : \"Profile\",\r\n    \"url\" : \"https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png\"\r\n  },\r\n  \"validFrom\" : \"2022-10-09T10:12:50Z\",\r\n  \"type\" : [ \"VerifiableCredential\", \"OpenBadgeCredential\" ],\r\n  \"proof\" : {\r\n    \"type\" : \"JsonWebSignature2020\",\r\n    \"creator\" : \"did:web:walt.id\",\r\n    \"created\" : \"2022-10-09T10:12:50Z\",\r\n    \"proofPurpose\" : \"assertionMethod\",\r\n    \"verificationMethod\" : \"did:web:walt.id#c1672b42f846471eb2c22fd601169566\",\r\n    \"jws\" : \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg\"\r\n  }\r\n}"
    ],
    "holderDid": "did:web:my.domain"
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1"
    ],
    "holder": "did:web:my.domain",
    "id": "urn:uuid:0f9a8692-badf-4f0c-aa07-a4c3279e3470",
    "type":
    [
        "VerifiablePresentation"
    ],
    "verifiableCredential":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1"
            ],
            "credentialSchema":
            {
                "id": "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
                "type": "FullJsonSchemaValidator2021"
            },
            "credentialSubject":
            {
                "currentAddress":
                [
                    "1 Boulevard de la Liberté, 59800 Lille"
                ],
                "dateOfBirth": "1993-04-08",
                "familyName": "DOE",
                "firstName": "Jane",
                "gender": "FEMALE",
                "id": "did:web:my.domain",
                "nameAndFamilyNameAtBirth": "Jane DOE",
                "personalIdentifier": "0904008084H",
                "placeOfBirth": "LILLE, FRANCE"
            },
            "evidence":
            [
                {
                    "documentPresence":
                    [
                        "Physical"
                    ],
                    "evidenceDocument":
                    [
                        "Passport"
                    ],
                    "subjectPresence": "Physical",
                    "type":
                    [
                        "DocumentVerification"
                    ],
                    "verifier": "did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
                }
            ],
            "id": "urn:uuid:4d88d22e-214b-4aa3-a4e9-906da9daf36a",
            "issued": "2022-10-09T10:11:51Z",
            "issuer": "did:web:walt.id",
            "proof":
            {
                "created": "2022-10-09T10:11:52Z",
                "creator": "did:web:walt.id",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..H4mLlx3Ot3rWV_EzthoiAjZs6J4UkJywuGENmSsqNHEnMGlwFHRKSNGWHwWnz2a7R38ktyo8r0_3sc2IkxGvCA",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:web:walt.id#c1672b42f846471eb2c22fd601169566"
            },
            "validFrom": "2022-10-09T10:11:51Z",
            "issuanceDate": "2022-10-09T10:11:51Z",
            "type":
            [
                "VerifiableCredential",
                "VerifiableAttestation",
                "VerifiableId"
            ]
        },
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/jff-vc-edu-plugfest-1-context.json"
            ],
            "credentialSubject":
            {
                "achievement":
                {
                    "criteria":
                    {
                        "narrative": "The first cohort of the JFF Plugfest 1 in May/June of 2021 collaborated to push interoperability of VCs in education forward.",
                        "type": "Criteria"
                    },
                    "description": "This wallet can display this Open Badge 3.0",
                    "image": "https://w3c-ccg.github.io/vc-ed/plugfest-1-2022/images/plugfest-1-badge-image.png",
                    "name": "Our Wallet Passed JFF Plugfest #1 2022",
                    "type": "Achievement"
                },
                "id": "did:web:my.domain",
                "type": "AchievementSubject"
            },
            "id": "urn:uuid:1745f6ff-3e12-4678-b714-e779e989ae25",
            "issuanceDate": "2020-03-10T04:24:12.164Z",
            "issued": "2022-10-09T10:12:50Z",
            "issuer":
            {
                "id": "did:web:walt.id",
                "image": "https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png",
                "name": "Jobs for the Future (JFF)",
                "type": "Profile",
                "url": "https://kayaelle.github.io/vc-ed/plugfest-1-2022/images/JFF_LogoLockup.png"
            },
            "proof":
            {
                "created": "2022-10-09T10:12:50Z",
                "creator": "did:web:walt.id",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..8EIBOS-UKOUXboKElqWxRuux851NTbbll_sd16-67vv8Gh8vicJDNu7DjU-QgpsnJO_4mG8swxrOJeIFuU58Bg",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:web:walt.id#c1672b42f846471eb2c22fd601169566"
            },
            "validFrom": "2022-10-09T10:12:50Z",
            "type":
            [
                "VerifiableCredential",
                "OpenBadgeCredential"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-09T10:21:11Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..2S3aHQISbL81Dbe1yOakXBFGvUJjxEZ7zGZZZ3XOJibtAON5v9lr5Q9NGt1c8h0zSrTLQDl2-fQ7A6HA9KL9Cw"
    }
}
```
{% endtab %}
{% endtabs %}

### Present stored credential
The `/credentials/presentIds` endpoint creates a verifiable presentation from the specified credential ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/presentIds' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "vcIds":
    [
        "string"
    ],
    "holderDid": "string",
    "verifierDid": "string",
    "domain": "string",
    "challenge": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
{
    "context":
    [
        "string"
    ],
    "id": "string",
    "holder": "string",
    "verifiableCredential":
    [
        {
            "json": "string",
            "issuanceDate": "string",
            "dateFormat":
            {
                "locale":
                {
                    "language": "string",
                    "script": "string",
                    "variant": "string",
                    "displayName": "string",
                    "country": "string",
                    "unicodeLocaleAttributes":
                    [
                        "string"
                    ],
                    "unicodeLocaleKeys":
                    [
                        "string"
                    ],
                    "displayLanguage": "string",
                    "displayScript": "string",
                    "displayCountry": "string",
                    "displayVariant": "string",
                    "extensionKeys":
                    [
                        "string"
                    ],
                    "iso3Language": "string",
                    "iso3Country": "string"
                },
                "decimalStyle":
                {
                    "zeroDigit": "string",
                    "positiveSign": "string",
                    "negativeSign": "string",
                    "decimalSeparator": "string"
                },
                "resolverStyle": "STRICT",
                "resolverFields":
                [
                    {
                        "baseUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "rangeUnit":
                        {
                            "dateBased": true,
                            "timeBased": true,
                            "duration":
                            {
                                "seconds": 0,
                                "nano": 0,
                                "negative": true,
                                "zero": true,
                                "units":
                                [
                                    {
                                        "dateBased": true,
                                        "timeBased": true,
                                        "durationEstimated": true
                                    }
                                ]
                            },
                            "durationEstimated": true
                        },
                        "dateBased": true,
                        "timeBased": true
                    }
                ],
                "zone":
                {
                    "id": "string",
                    "rules":
                    {
                        "fixedOffset": true,
                        "transitions":
                        [
                            {
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "duration":
                                {
                                    "seconds": 0,
                                    "nano": 0,
                                    "negative": true,
                                    "zero": true,
                                    "units":
                                    [
                                        {
                                            "dateBased": true,
                                            "timeBased": true,
                                            "durationEstimated": true
                                        }
                                    ]
                                },
                                "gap": true,
                                "dateTimeBefore": "2022-10-09T09:52:44.738Z",
                                "dateTimeAfter": "2022-10-09T09:52:44.738Z",
                                "overlap": true,
                                "instant": "2022-10-09T09:52:44.738Z"
                            }
                        ],
                        "transitionRules":
                        [
                            {
                                "month": "JANUARY",
                                "timeDefinition": "UTC",
                                "standardOffset":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetBefore":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "offsetAfter":
                                {
                                    "totalSeconds": 0,
                                    "id": "string"
                                },
                                "dayOfWeek": "MONDAY",
                                "dayOfMonthIndicator": 0,
                                "localTime":
                                {
                                    "hour": 0,
                                    "minute": 0,
                                    "second": 0,
                                    "nano": 0
                                },
                                "midnightEndOfDay": true
                            }
                        ]
                    }
                },
                "chronology":
                {
                    "id": "string",
                    "calendarType": "string"
                }
            },
            "jwt": "string",
            "id": "string",
            "type":
            [
                "string"
            ],
            "subject": "string",
            "expirationDate": "string",
            "credentialSchema":
            {
                "id": "string",
                "type": "string"
            },
            "proof":
            {
                "type": "string",
                "creator": "string",
                "created": "string",
                "domain": "string",
                "proofPurpose": "string",
                "verificationMethod": "string",
                "jws": "string",
                "nonce": "string"
            },
            "challenge": "string",
            "validFrom": "string",
            "issued": "string",
            "issuer": "string"
        }
    ],
    "proof":
    {
        "type": "string",
        "creator": "string",
        "created": "string",
        "domain": "string",
        "proofPurpose": "string",
        "verificationMethod": "string",
        "jws": "string",
        "nonce": "string"
    },
    "issued": "string",
    "validFrom": "string",
    "expirationDate": "string",
    "json": "string",
    "issuanceDate": "string",
    "dateFormat":
    {
        "locale":
        {
            "language": "string",
            "script": "string",
            "variant": "string",
            "displayName": "string",
            "country": "string",
            "unicodeLocaleAttributes":
            [
                "string"
            ],
            "unicodeLocaleKeys":
            [
                "string"
            ],
            "displayLanguage": "string",
            "displayScript": "string",
            "displayCountry": "string",
            "displayVariant": "string",
            "extensionKeys":
            [
                "string"
            ],
            "iso3Language": "string",
            "iso3Country": "string"
        },
        "decimalStyle":
        {
            "zeroDigit": "string",
            "positiveSign": "string",
            "negativeSign": "string",
            "decimalSeparator": "string"
        },
        "resolverStyle": "STRICT",
        "resolverFields":
        [
            {
                "baseUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "rangeUnit":
                {
                    "dateBased": true,
                    "timeBased": true,
                    "duration":
                    {
                        "seconds": 0,
                        "nano": 0,
                        "negative": true,
                        "zero": true,
                        "units":
                        [
                            {
                                "dateBased": true,
                                "timeBased": true,
                                "durationEstimated": true
                            }
                        ]
                    },
                    "durationEstimated": true
                },
                "dateBased": true,
                "timeBased": true
            }
        ],
        "zone":
        {
            "id": "string",
            "rules":
            {
                "fixedOffset": true,
                "transitions":
                [
                    {
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "duration":
                        {
                            "seconds": 0,
                            "nano": 0,
                            "negative": true,
                            "zero": true,
                            "units":
                            [
                                {
                                    "dateBased": true,
                                    "timeBased": true,
                                    "durationEstimated": true
                                }
                            ]
                        },
                        "gap": true,
                        "dateTimeBefore": "2022-10-09T09:52:44.739Z",
                        "dateTimeAfter": "2022-10-09T09:52:44.739Z",
                        "overlap": true,
                        "instant": "2022-10-09T09:52:44.739Z"
                    }
                ],
                "transitionRules":
                [
                    {
                        "month": "JANUARY",
                        "timeDefinition": "UTC",
                        "standardOffset":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetBefore":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "offsetAfter":
                        {
                            "totalSeconds": 0,
                            "id": "string"
                        },
                        "dayOfWeek": "MONDAY",
                        "dayOfMonthIndicator": 0,
                        "localTime":
                        {
                            "hour": 0,
                            "minute": 0,
                            "second": 0,
                            "nano": 0
                        },
                        "midnightEndOfDay": true
                    }
                ]
            }
        },
        "chronology":
        {
            "id": "string",
            "calendarType": "string"
        }
    },
    "jwt": "string",
    "type":
    [
        "string"
    ],
    "subject": "string",
    "credentialSchema":
    {
        "id": "string",
        "type": "string"
    },
    "issuer": "string",
    "challenge": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Create a verifiable presentation from the stored credential having id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_ for the holder with did = _did:web:my.domain_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/credentials/presentIds' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcIds": [
    "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
  ],
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "vcIds":
    [
        "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270"
    ],
    "holderDid": "did:web:my.domain"
}
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "@context":
    [
        "https://www.w3.org/2018/credentials/v1"
    ],
    "holder": "did:web:my.domain",
    "id": "urn:uuid:35e627b2-297c-4d33-85cd-a4dfc40bab32",
    "type":
    [
        "VerifiablePresentation"
    ],
    "verifiableCredential":
    [
        {
            "@context":
            [
                "https://www.w3.org/2018/credentials/v1",
                "https://www.w3.org/2018/credentials/examples/v1"
            ],
            "credentialSubject":
            {
                "degree":
                {
                    "name": "Bachelor of Science and Arts",
                    "type": "BachelorDegree"
                },
                "id": "did:web:my.domain"
            },
            "id": "urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270",
            "issued": "2022-10-07T09:53:41.369913097Z",
            "issuer":
            {
                "id": "did:web:walt.id"
            },
            "proof":
            {
                "created": "2022-10-07T09:53:41Z",
                "creator": "did:web:walt.id",
                "domain": "https://api.preprod.ebsi.eu",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ",
                "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
                "type": "Ed25519Signature2018"
            },
            "validFrom": "2022-10-07T09:53:41.369917079Z",
            "issuanceDate": "2022-10-07T09:53:41.369917079Z",
            "type":
            [
                "VerifiableCredential",
                "UniversityDegreeCredential"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-09T09:52:44Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..KCfytKgejnjdW_D632lugaj08E9yO8DcDmNcAoGHywld7twcUf1QqKoidfGNW3j2un4ywqRnjSIiYzK8ZxoXDg"
    }
}
```
{% endtab %}
{% endtabs %}