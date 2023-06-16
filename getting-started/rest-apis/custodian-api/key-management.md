# Key management

Key management functions include:

* [List](#list-keys) - lists the available keys
* [Load](#load-key) - loads a key specified by its alias
* [Generate](#generate-key) - generate a key using the specified algorithm
* [Import](#import-key) - imports a key
* [Delete](#delete-key) - deletes a specific key
* [Export](#export-key) - exports public and private key parts (if supported by the underlying keystore)

## List keys

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

## Load key

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

## Generate key

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

E.g. Generate a key using the _EdDSA\_Ed25519_ algorithm.

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

## Import key

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

## Delete key

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

## Export key

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