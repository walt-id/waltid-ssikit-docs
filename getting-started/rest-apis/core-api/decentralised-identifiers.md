# Decentralised identifiers

The following DID management functions are available:

* [list](#list-dids) - list DIDs
* [load](#load-did) - load DID
* [delete by url](#delete-did) - delete by DID url
* [create](#create-did) - create DID
* [resolve](#resolve-did) - resolve DID
* [import](#import-did) - import DID

## List DIDs

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

## Load DID

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

E.g. Load the DID = `did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z`.

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

## Delete DID

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

E.g. Delete the DID = `did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z`.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'DELETE' \
  'https://core.ssikit.walt.id/v1/did/did%3Akey%3Az6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z' \
  -H 'accept: application/json'
```
{% endtab %}
{% endtabs %}

## Create DID

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
    "method": "string",
    "keyAlias": "string",
    "method-dependent-options": "..."
}
```
{% endtab %}

{% tab title="Response body schema" %}
```
The DID url string
```
{% endtab %}
{% endtabs %}

The `method` and `keyAlias` properties are common for all _did-method_ requests,
`method` being required, while `keyAlias` - optional 
(if not specified, a new key will be automatically created using the default algorithm
according to the _did-method_).
The method-dependent options have default values, if not specified otherwise.
Below are the available properties by _did-method_.

{% tabs %}
{% tab title="key" %}
```json
{
    "method": "key",
    "keyAlias": "string",
    "isJwk": "boolean"
}
```
* `isJwk` (default) - _false_

{% endtab %}
{% tab title="web" %}
```json
{
  "method": "web",
  "keyAlias": "string",
  "didWebDomain": "string",
  "didWebPath": "string"
}
```
* `didWebDomain` (default) - _"walt.id"_
* `didWebPath` (default) - _empty-string_

{% endtab %}
{% tab title="ebsi" %}
```json
{
    "method": "ebsi",
    "keyAlias": "string",
    "version": "int"
}
```
* `version` (default) - _1_

{% endtab %}
{% tab title="cheqd" %}
```json
{
    "method": "cheqd",
    "keyAlias": "string",
    "network": "string"
}
```
* `network` (default) - _"testnet"_

{% endtab %}
{% tab title="iota" %}
```json
{
    "method": "iota",
    "keyAlias": "string"
}
```
{% endtab %}
{% tab title="jwk" %}
```json
{
    "method": "jwk",
    "keyAlias": "string"
}
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

## Resolve DID

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

E.g. Resolve the DID = `did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa`.

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

## Import DID

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

E.g. Import the DID = `did:key:z6MkqmaCT2JqdUtLeKah7tEVfNXtDXtQyj4yxEgV11Y5CqUa`.

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