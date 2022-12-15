---
description: Core REST API functions.
---

# Core API

[Swagger](https://core.ssikit.walt.id/v1/swagger) | [Redoc](https://core.ssikit.walt.id/v1/redoc)

The _Core API_ exposes wallet core functionality in the scope of storing and managing:

* [Cryptographic keys](core-api.md#cryptographic-keys)
* [Decentralised Identifiers (DIDs)](core-api.md#decentralised-identifiers)
* [Verifiable Credentials (VCs)](core-api.md#verifiable-credentials)

{% hint style="info" %}
The Core API exposes most of the funtionalities provided by the SSI Kit, however newer features will only be released in the other API endpoints. Therefore, it is recommended to use the Signatory API, Custodian API and Auditor API for most use cases.
{% endhint %}

## Cryptographic keys

The following key management functions are available:

* [list](core-api.md#list-key-ids) - list of key ids
* [load](core-api.md#load-key) - load the public key in _JWK_ format
* [delete](core-api.md#delete-key) - delete key
* [generate](core-api.md#generate-key) - generate key
* [import](core-api.md#import-key) - import key
* [export](core-api.md#export-key) - export key

### List key ids

The `/v1/key` endpoint lists the available key ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/key' \
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
The list of key ids
```
{% endtab %}
{% endtabs %}

E.g. List the available key ids.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/key' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    "e548f032cadf4145ab6886a57c2e87e6",
    "e70e8fd8932043caa7c857c3b944d0e0",
    "b50db0c1f73242b8bb0f2f6324e15ec3",
    "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX#z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "8cc0b1707ea345ed83e479469d42aac2",
    "c5b11445be0e4d37863170df3328630b",
    "8394ea7883bc4328a3f18b146b7e16bd",
    "fd36a0159592413da1d89f192dd77dcd",
    "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
    "fa9296808e64440d89e6d245a1709141",
    "8dd54d6ae25a4818b1497530a8659dc1"
]
```
{% endtab %}
{% endtabs %}

### Load key

The `/v1/key/{id}` endpoint loads the public component of the provided key id in _JWK_ format:

* id - path parameter (required) - the key id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/key/{id}' \
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
The string for the public component of the key
```
{% endtab %}
{% endtabs %}

E.g. Load the key having id = _e548f032cadf4145ab6886a57c2e87e6_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/key/e548f032cadf4145ab6886a57c2e87e6' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
"{\"kty\":\"OKP\",\"use\":\"sig\",\"crv\":\"Ed25519\",\"kid\":\"e548f032cadf4145ab6886a57c2e87e6\",\"x\":\"jT8YleOQnaABpZTnvId3WoID4Pia9Lex9OndqQ22Xxs\",\"alg\":\"EdDSA\"}"
```
{% endtab %}
{% endtabs %}

### Delete key

The `/v1/key/{id}` endpoint deletes the specified key.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/key/' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
The key id string
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Delete the key having id = _e548f032cadf4145ab6886a57c2e87e6_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/key/' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'e548f032cadf4145ab6886a57c2e87e6'
```
{% endtab %}

{% tab title="Request body" %}
```
e548f032cadf4145ab6886a57c2e87e6
```
{% endtab %}
{% endtabs %}

### Generate key

The `/v1/key/gen` generates a new key using the specified algorithm.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/key/gen' \
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
    "id": "string"
}
```
{% endtab %}
{% endtabs %}

E.g. Generate a new key using the _EdDSA\_Ed25519_ algorithm.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/key/gen' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyAlgorithm": "EdDSA_Ed25519"
}'
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
    "id": "2251db0d15eb4e96b80c471edbaed185"
}
```
{% endtab %}
{% endtabs %}

### Import key

The `/v1/key/import` endpoint imports a key (_JWK_ or _PEM_ format) to the underlying keystore.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/key/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
The key string in JWK or PEM format
```
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
  'https://core.ssikit.walt.id/v1/key/import' \
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

### Export key

The `/v1/key/export` endpoint exports public and private key part (if supported by underlying keystore).

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/key/export' \
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

E.g. Export the public key with id = _bc6fa6b0593648238c4616800bed7746_ as _JWK_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/key/export' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "keyAlias": "bc6fa6b0593648238c4616800bed7746",
  "format": "JWK",
  "exportPrivate": false
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "keyAlias": "bc6fa6b0593648238c4616800bed7746",
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
    "kid": "bc6fa6b0593648238c4616800bed7746",
    "x": "YyswAyRO2Aur8Jmzc8aOvI3AWFka3ZynJwB84a0FJVU",
    "alg": "EdDSA"
}
```
{% endtab %}
{% endtabs %}

## Decentralised identifiers

The following DID management functions are available:

* [list](core-api.md#list-dids) - list DIDs
* [load](core-api.md#load-did) - load DID
* [delete by url](core-api.md#delete-did) - delete by DID url
* [create](core-api.md#delete-did) - create DID
* [resolve](core-api.md#resolve-did) - resolve DID
* [import](core-api.md#import-did) - import DID

### List DIDs

The `/v1/did` endpoint lists the available DIDs.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/did' \
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
[
    "string"
]
```
{% endtab %}
{% endtabs %}

E.g. List the available DIDs.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/did' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    "did:ebsi:zwdPobJGue3w86Gpqhq5Cni",
    "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
    "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "did:web:my.domain",
    "did:web:walt.id",
    "did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q"
]
```
{% endtab %}
{% endtabs %}

### Load DID

The `/v1/did/{id}` endpoint loads a DID specified by:

* id - path parameter (required) - the DID url string

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/did/{id}' \
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
The DID document
```
{% endtab %}
{% endtabs %}

E.g. Load the DID = _did_:key:_z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/did/did%3Akey%3Az6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "assertionMethod":
    [
        "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z"
    ],
    "authentication":
    [
        "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z"
    ],
    "capabilityDelegation":
    [
        "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z"
    ],
    "capabilityInvocation":
    [
        "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z"
    ],
    "@context":
    [
        "https://www.w3.org/ns/did/v1"
    ],
    "id": "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
    "keyAgreement":
    [
        "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6LSrs5FudTTsAUhHUoS1kzkhskwAWaYjyU13CVgZT7fwDWk"
    ],
    "verificationMethod":
    [
        {
            "controller": "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
            "id": "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
            "publicKeyBase58": "7g7ZKyYMckYQyVVZmBaRMR1j2Fj9m5biSwV7iz3HxeGc",
            "type": "Ed25519VerificationKey2019"
        },
        {
            "controller": "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z",
            "id": "did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z#z6LSrs5FudTTsAUhHUoS1kzkhskwAWaYjyU13CVgZT7fwDWk",
            "publicKeyBase58": "GBu6PKebmhkxC6RfV7UoPHYTKN3S3NHrADn14zU9Dqjz",
            "type": "X25519KeyAgreementKey2019"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Delete DID

The `/v1/did/{id}` endpoint deletes the DID by:

* id - path parameter (required) - the DID url string

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/did/{id}' \
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

E.g. Delete the DID = _did_:key:_z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/did/did%3Akey%3Az6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

### Create DID

The `/v1/did/create` creates a DID.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/create' \
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

E.g. Create a DID using the _key_ method and automatically generate a new key.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "key"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "method": "key"
}
```
{% endtab %}

{% tab title="Response body" %}
```
did:key:z6MkqJfAPYYDiDeNERPMufpS1gxgzqiG5fvQnqbYTwY5xJDE
```
{% endtab %}
{% endtabs %}

### Resolve DID

The `/v1/did/resolve` resolves a DID url string to a DID document.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/resolve' \
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
The DID document
```
{% endtab %}
{% endtabs %}

E.g. Resolve the DID = _did_:key:_z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/resolve' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "did": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "did": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "assertionMethod":
    [
        "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
    ],
    "authentication":
    [
        "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
    ],
    "capabilityDelegation":
    [
        "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
    ],
    "capabilityInvocation":
    [
        "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa"
    ],
    "@context":
    [
        "https://www.w3.org/ns/did/v1"
    ],
    "id": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
    "keyAgreement":
    [
        "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6LSkSwxKk6TFYcqcRHv7ALR87CTFK6bSkQsxwqczx1YgYik"
    ],
    "verificationMethod":
    [
        {
            "controller": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
            "id": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
            "publicKeyBase58": "CKK9rn4QHwPsXpjzSKGepGytPxcZZqpdGDmZAja4HchC",
            "type": "Ed25519VerificationKey2019"
        },
        {
            "controller": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
            "id": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa#z6LSkSwxKk6TFYcqcRHv7ALR87CTFK6bSkQsxwqczx1YgYik",
            "publicKeyBase58": "9mmnoSHbA5u6X2v9aWpToWyyQAZUk9Ej5y7wWVN1yAwz",
            "type": "X25519KeyAgreementKey2019"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Import DID

The `/v1/did/import` endpoint resolves and imports the specified DID url to the underlying data store.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
The DID url string
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 201
```
{% endtab %}
{% endtabs %}

E.g. Import the DID = _did_:key:_z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/did/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa'
```
{% endtab %}

{% tab title="Request body" %}
```
did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa
```
{% endtab %}
{% endtabs %}

## Verifiable credentials

The following credentials management functions are available:

* [list](core-api.md#list-credentials) - list verifiable credentials
* [load](core-api.md#load-credential) - load the verifiable credential
* [delete](core-api.md#delete-credential) - delete the verifiable credential
* [create](core-api.md#create-credential) - create a verifiable credential
* [present](core-api.md#present-credentials) - create a verifiable presentation from the supplied credentials
* [verify](core-api.md#verifiable-credentials) - verify credential / presentation
* [import](core-api.md#import-credential) - import the verifiable credential

### List credentials

The `/v1/vc` endpoint lists the available credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc' \
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
The list of credential names (file names)
```
{% endtab %}
{% endtabs %}

E.g. List the available credentials.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc' \
  -H 'accept: application/json'
```
{% endtab %}

{% tab title="Response body" %}
```
[
    ""
]
```
{% endtab %}
{% endtabs %}

### Load credential

The `/v1/vc/{id}` endpoint loads a credential specified by:

* id - path parameter (required) - the credential id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://core.ssikit.walt.id/v1/vc/{id}' \
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
  'https://core.ssikit.walt.id/v1/vc/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
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

### Delete credential

The `/v1/vc/{id}` deletes a credential by:

* id - path parameter (required) - the credential's id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/vc/{id}' \
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

E.g. Delete the credential with id = _urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/vc/urn%3Auuid%3Ad36986f1-3cc0-4156-b5a4-6d3deab84270' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

### Create credential

The `/v1/vc/create` endpoint creates a credential.

{% tabs %}
{% tab title="Request body schema" %}
```
{
    "issuerDid": "string",
    "subjectDid": "string",
    "credentialOffer": "string",
    "templateId": "string",
    "domain": "string",
    "nonce": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
The verifiable credential
```
{% endtab %}
{% endtabs %}

E.g. Create a credential from the _UniveristyDegree_ template, having issuer = _did_:key:_z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa_ and holder = _did_:key:_z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX_.

{% tabs %}
{% tab title="Request body" %}
```
{
    "issuerDid": "did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa",
    "subjectDid": "did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX",
    "templateId": "UniversityDegree"
}
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

### Present credentials

The `/v1/vc/present` endpoint creates a verifiable presentation from the supplied credential. Only _JSON-LD_ format is supported.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vc": "string",
    "holderDid": "string",
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

E.g. Create a verifiable presentation from the provided _VeriafiableID_ credential for a holder with did = _did:web:my.domain_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/present' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vc": "{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"credentialSchema\":{\"id\":\"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Libert\u00E9, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"],\"proof\":{\"type\":\"JsonWebSignature2020\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"created\":\"2022-10-11T10:19:32Z\",\"proofPurpose\":\"assertionMethod\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\"}}",
  "holderDid": "did:web:my.domain"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vc": "{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"credentialSchema\":{\"id\":\"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Liberté, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"],\"proof\":{\"type\":\"JsonWebSignature2020\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"created\":\"2022-10-11T10:19:32Z\",\"proofPurpose\":\"assertionMethod\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\"}}",
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
    "id": "urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d",
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
                "id": "did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR",
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
            "id": "urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90",
            "issued": "2022-10-11T10:19:31Z",
            "issuer": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL",
            "proof":
            {
                "created": "2022-10-11T10:19:32Z",
                "creator": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL",
                "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw",
                "proofPurpose": "assertionMethod",
                "type": "JsonWebSignature2020",
                "verificationMethod": "did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL"
            },
            "validFrom": "2022-10-11T10:19:31Z",
            "issuanceDate": "2022-10-11T10:19:31Z",
            "type":
            [
                "VerifiableCredential",
                "VerifiableAttestation",
                "VerifiableId"
            ]
        }
    ],
    "proof":
    {
        "type": "Ed25519Signature2018",
        "creator": "did:web:my.domain",
        "created": "2022-10-11T10:23:26Z",
        "domain": "https://api.preprod.ebsi.eu",
        "nonce": "dc2be572-cca4-43dc-9903-0fec1dcf786f",
        "proofPurpose": "authentication",
        "verificationMethod": "did:web:my.domain#c5b11445be0e4d37863170df3328630b",
        "jws": "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ"
    }
}
```
{% endtab %}
{% endtabs %}

### Verify credentials

The `/v1/vc/verify` endpoint verifies the supplied credential or presentation against the signature policy.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
{
    "vcOrVp": "string"
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
{
    "verificationType": "string",
    "verified": boolean
}
```
{% endtab %}
{% endtabs %}

E.g. Verify a presentation.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "vcOrVp": "{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"holder\":\"did:web:my.domain\",\"id\":\"urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d\",\"type\":[\"VerifiablePresentation\"],\"verifiableCredential\":[{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\"],\"credentialSchema\":{\"id\":\"https:\/\/api.preprod.ebsi.eu\/trusted-schemas-registry\/v1\/schemas\/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Libert\u00E9, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"proof\":{\"created\":\"2022-10-11T10:19:32Z\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\",\"proofPurpose\":\"assertionMethod\",\"type\":\"JsonWebSignature2020\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\"},\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"]}],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:my.domain\",\"created\":\"2022-10-11T10:23:26Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"proofPurpose\":\"authentication\",\"verificationMethod\":\"did:web:my.domain#c5b11445be0e4d37863170df3328630b\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ\"}}"
}'
```
{% endtab %}

{% tab title="Request body" %}
```
{
    "vcOrVp": "{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"holder\":\"did:web:my.domain\",\"id\":\"urn:uuid:a6a93543-4fee-4127-8ec0-4c70eac60f2d\",\"type\":[\"VerifiablePresentation\"],\"verifiableCredential\":[{\"@context\":[\"https://www.w3.org/2018/credentials/v1\"],\"credentialSchema\":{\"id\":\"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba\",\"type\":\"FullJsonSchemaValidator2021\"},\"credentialSubject\":{\"currentAddress\":[\"1 Boulevard de la Liberté, 59800 Lille\"],\"dateOfBirth\":\"1993-04-08\",\"familyName\":\"DOE\",\"firstName\":\"Jane\",\"gender\":\"FEMALE\",\"id\":\"did:key:z6MkmRtH7cWeRnQfpeqDfBxa73jhSwUSKfBGUeB6Sk2DgbwR\",\"nameAndFamilyNameAtBirth\":\"Jane DOE\",\"personalIdentifier\":\"0904008084H\",\"placeOfBirth\":\"LILLE, FRANCE\"},\"evidence\":[{\"documentPresence\":[\"Physical\"],\"evidenceDocument\":[\"Passport\"],\"subjectPresence\":\"Physical\",\"type\":[\"DocumentVerification\"],\"verifier\":\"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"}],\"id\":\"urn:uuid:5368e8a9-b1f2-49a6-8ef2-6ba6088baa90\",\"issued\":\"2022-10-11T10:19:31Z\",\"issuer\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"proof\":{\"created\":\"2022-10-11T10:19:32Z\",\"creator\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..Ab-s21gF5B-dAoYmMq9gb5vfYnQOrpECaWuU_vcTMmTofYzOaO0YPKcdAvXoUw--NTUZp9zrK4w3z9HPyHPBDw\",\"proofPurpose\":\"assertionMethod\",\"type\":\"JsonWebSignature2020\",\"verificationMethod\":\"did:key:z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL#z6Mkeu6eroi9VuHsqxtkWHxKS4egHtVH4snzRtuFFtUYwavL\"},\"validFrom\":\"2022-10-11T10:19:31Z\",\"issuanceDate\":\"2022-10-11T10:19:31Z\",\"type\":[\"VerifiableCredential\",\"VerifiableAttestation\",\"VerifiableId\"]}],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:my.domain\",\"created\":\"2022-10-11T10:23:26Z\",\"domain\":\"https://api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"proofPurpose\":\"authentication\",\"verificationMethod\":\"did:web:my.domain#c5b11445be0e4d37863170df3328630b\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..WqpWOUqaLf8D4aw40aS5R-h-_ZvF6YX1qhVOPULlPUuwP-8WdmfqV5jiwjx_-OL6t55v2ipPGVhY6Sfa47h5DQ\"}}"
}
```
{% endtab %}

{% tab title="Response body" %}
```
{
    "verificationType": "VERIFIABLE_PRESENTATION",
    "verified": true
}
```
{% endtab %}
{% endtabs %}

### Import credential

The `/v1/vc/import` endpoint imports a verifiable credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```
The credential string
```
{% endtab %}

{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Import the _UniversityDegree_ credential.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://core.ssikit.walt.id/v1/vc/import' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '"{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\",\"https:\/\/www.w3.org\/2018\/credentials\/examples\/v1\"],\"credentialSubject\":{\"degree\":{\"name\":\"Bachelor of Science and Arts\",\"type\":\"BachelorDegree\"},\"id\":\"did:web:my.domain\"},\"id\":\"urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270\",\"issued\":\"2022-10-07T09:53:41.369913097Z\",\"issuer\":{\"id\":\"did:web:walt.id\"},\"validFrom\":\"2022-10-07T09:53:41.369917079Z\",\"issuanceDate\":\"2022-10-07T09:53:41.369917079Z\",\"type\":[\"VerifiableCredential\",\"UniversityDegreeCredential\"],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:walt.id\",\"created\":\"2022-10-07T09:53:41Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ\"}}"'
```
{% endtab %}

{% tab title="Request body" %}
```
"{\"@context\":[\"https:\/\/www.w3.org\/2018\/credentials\/v1\",\"https:\/\/www.w3.org\/2018\/credentials\/examples\/v1\"],\"credentialSubject\":{\"degree\":{\"name\":\"Bachelor of Science and Arts\",\"type\":\"BachelorDegree\"},\"id\":\"did:web:my.domain\"},\"id\":\"urn:uuid:d36986f1-3cc0-4156-b5a4-6d3deab84270\",\"issued\":\"2022-10-07T09:53:41.369913097Z\",\"issuer\":{\"id\":\"did:web:walt.id\"},\"validFrom\":\"2022-10-07T09:53:41.369917079Z\",\"issuanceDate\":\"2022-10-07T09:53:41.369917079Z\",\"type\":[\"VerifiableCredential\",\"UniversityDegreeCredential\"],\"proof\":{\"type\":\"Ed25519Signature2018\",\"creator\":\"did:web:walt.id\",\"created\":\"2022-10-07T09:53:41Z\",\"domain\":\"https:\/\/api.preprod.ebsi.eu\",\"nonce\":\"dc2be572-cca4-43dc-9903-0fec1dcf786f\",\"jws\":\"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..7EYkgjNRJ_hh0F5kONnPfrC4PLvg1g82czeANllDngsbk36a8lnHSlwersSqY0tdER4xIe7vbNVzi39C2DZTDQ\"}}"
```
{% endtab %}
{% endtabs %}
