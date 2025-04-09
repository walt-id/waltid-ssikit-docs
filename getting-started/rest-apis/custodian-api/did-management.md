---
noIndex: true
---

# Did management

DID management functions enable the following:

* [List](did-management.md#list-did) - lists the available DIDs
* [Load](did-management.md#load-did) - loads a DID by the specified id
* [Delete](did-management.md#delete-did) - deletes a DID by the specified url
* [Create](did-management.md#create-did) - creates a new DID
* [Resolve](did-management.md#resolve-did) - resolves a DID to a document
* [Import](did-management.md#import-did) - import a DID

For more info on DIDs, go [here](../../../ssi-kit/ssi-kit/what-is-ssi/technologies-and-concepts/decentralised-identifiers-dids.md).

## List DID

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

## Load DID

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

## Delete DID

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

## Create DID

The `/did/create` endpoint creates a DID.

{% tabs %}
{% tab title="curl" %}
```shell
curl -X 'POST' \
  'https://custodian.ssikit.walt.id/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}

{% tab title="Request body schema" %}
```json
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

The `method` and `keyAlias` properties are common for all _did-method_ requests, `method` being required, while `keyAlias` - optional (if not specified, a new key will be automatically created using the default algorithm according to the _did-method_). The method-dependent options have default values, if not specified otherwise. Below are the available properties by _did-method_.

{% tabs %}
{% tab title="key" %}
```json
{
    "method": "key",
    "keyAlias": "string",
    "useJwkJcsPub": "boolean"
}
```

* `useJwkJcsPub` (default) - _false_ - specifies whether to create a did:key using the jwk\_jcs-pub multicodec (code: [0xeb51](https://github.com/multiformats/multicodec/blob/master/table.csv#L516))
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

E.g. Create a DID using the `web` method having the domain set to `walt.id`.

{% tabs %}
{% tab title="curl" %}
```shell
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
```json
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

## Resolve DID

The `/did/resolve` endpoint resolves a DID.

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

E.g. Reslove the DID having id = `did:key:z6MkkLmAVeM3P6B2LJ2xGrK1wVojCoephK4G9VrCcct42ADX`.

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

## Import DID

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

E.g. Import DID having id = `did:key:z6Mkm8NbvDnnxJ2t5zLGSkYGCWZiqq11Axr58xQ3ZG1Jss3z`.

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
