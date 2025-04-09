---
noIndex: true
---

# Cryptographic keys

The following key management functions are available:

* [list](cryptographic-keys.md#list-key-ids) - list of key ids
* [load](cryptographic-keys.md#load-key) - load the public key in _JWK_ format
* [delete](cryptographic-keys.md#delete-key) - delete key
* [generate](cryptographic-keys.md#generate-key) - generate key
* [import](cryptographic-keys.md#import-key) - import key
* [export](cryptographic-keys.md#export-key) - export key

## List key ids

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

## Load key

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

## Delete key

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

## Generate key

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

## Import key

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

## Export key

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
