---
description: >-
  ESSIF REST API functions.
---
# ESSIF API
[Swagger](https://essif.ssikit.walt.id/v1/swagger) | [ReDoc](https://essif.ssikit.walt.id/v1/redoc)

The _ESSIF API_ exposes the necessary endpoints for running the ESSIF specific flows between Issuers (incl. ESSIF Onboarding Services), Holders and Verifiers.

Aligned with the ESSIF terminology, the API is grouped by the User Wallet (wallet API for consumers / natural persons) and Enterprise Wallet (wallet API for organisations / legal entities).

Note that the EBSI/ESSIF specifications are expected to evolve which will be reflected in continuous updates of the proposed APIs.

The following functions are available:
* [onboard](essif-api.md#onboard) - EBSI onboarding flow, requests a Verifiable Authorization from EOS
* [authorize](essif-api.md#authorize) - ESSIF authorization flow
* [register did](essif-api.md#register-did) - registers DID on the EBSI blockchain
* [create timestamp](essif-api.md#create-timestamp) - creates a timestamp in EBSI ledger
* [load timestamp by id](essif-api.md#load-timestamp-by-id) - loads a timestamp by the timestamp id
* [load timestamp by hash](essif-api.md#load-timestamp-by-hash) - loads a timestamp by the transaction hash

## Onboard
The `/v1/client/onboard` endpoint onboards the specified DID to the EBSI blockchain. It runs the ESSIF onboard API and requires a _Bearer_ token, which can be acquired from https://app.preprod.ebsi.eu/users-onboarding.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/onboard' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "bearerToken": "string",
    "did": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
The VerifiableAuthorization credential string
```
{% endtab %}
{% endtabs %}

E.g. Onboard the did = _did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/onboard' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "bearerToken": "eyJhbGciOiJFUzI1NksiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2NjUzOTc0ODksImlhdCI6MTY2NTM5NjU4OSwiaXNzIjoiZGlkOmVic2k6emNHdnFnWlRIQ3Rramd0Y0tSTDdIOGsiLCJvbmJvYXJkaW5nIjoicmVjYXB0Y2hhIiwidmFsaWRhdGVkSW5mbyI6eyJhY3Rpb24iOiJsb2dpbiIsImNoYWxsZW5nZV90cyI6IjIwMjItMTAtMTBUMTA6MDk6NDZaIiwiaG9zdG5hbWUiOiJhcHAucHJlcHJvZC5lYnNpLmV1Iiwic2NvcmUiOjAuOSwic3VjY2VzcyI6dHJ1ZX19.Qth9uTf4uXoPR9PiykUKyLV6qsOXtG70gJRghRzu9qMtyQmfqVD5hx2YwBgoWF9jebLCcmVtbr1KxVjuNcy1Cg",
  "did": "did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "bearerToken": "eyJhbGciOiJFUzI1NksiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2NjUzOTc0ODksImlhdCI6MTY2NTM5NjU4OSwiaXNzIjoiZGlkOmVic2k6emNHdnFnWlRIQ3Rramd0Y0tSTDdIOGsiLCJvbmJvYXJkaW5nIjoicmVjYXB0Y2hhIiwidmFsaWRhdGVkSW5mbyI6eyJhY3Rpb24iOiJsb2dpbiIsImNoYWxsZW5nZV90cyI6IjIwMjItMTAtMTBUMTA6MDk6NDZaIiwiaG9zdG5hbWUiOiJhcHAucHJlcHJvZC5lYnNpLmV1Iiwic2NvcmUiOjAuOSwic3VjY2VzcyI6dHJ1ZX19.Qth9uTf4uXoPR9PiykUKyLV6qsOXtG70gJRghRzu9qMtyQmfqVD5hx2YwBgoWF9jebLCcmVtbr1KxVjuNcy1Cg",
    "did": "did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q"
}
```
{% endtab %}
{% tab title="Response body" %}
```
"{\"verifiableCredential\":{\"id\":\"vc:ebsi:authentication#b1a82eb3-9a29-429d-b440-91894ed07720\",\"issuer\":\"did:ebsi:zcGvqgZTHCtkjgtcKRL7H8k\",\"validFrom\":\"2022-10-10T11:35:23Z\",\"credentialSubject\":{\"id\":\"did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q\"},\"credentialSchema\":{\"id\":\"https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0x28d76954924d1c4747a4f1f9e3e9edc9ca965efbf8ff20e4339c2bf2323a5773\",\"type\":\"OID\"},\"issuanceDate\":\"2022-10-10T11:35:23Z\",\"expirationDate\":\"2023-04-10T11:35:23Z\",\"@context\":[\"https://www.w3.org/2018/credentials/v1\",\"https://www.w3.org/2018/credentials/examples/v1\",\"https://w3c-ccg.github.io/lds-jws2020/contexts/lds-jws2020-v1.json\"],\"type\":[\"VerifiableCredential\",\"VerifiableAuthorisation\"],\"proof\":{\"type\":\"EcdsaSecp256k1Signature2019\",\"created\":\"2022-10-10T11:35:23Z\",\"proofPurpose\":\"assertionMethod\",\"verificationMethod\":\"did:ebsi:zcGvqgZTHCtkjgtcKRL7H8k#keys-1\",\"jws\":\"eyJhbGciOiJFUzI1NksiLCJ0eXAiOiJKV1QifQ..WEwqx6kOJMA5Mk6xZ7uTfkZB8RDnAhnnIWInBH6BlJNjtsbzIfpHyzB11Gh1xWQVejD3i-0jnwxJyHs8m4JtuQ\"}}}"
```
{% endtab %}
{% endtabs %}

## Authorize
The `/v1/client/auth` runs the ESSIF authorization flow for the specified did.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/auth' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
The did string
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Run the authorization flow for did = _did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/auth' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q'
```
{% endtab %}
{% tab title="Request body" %}
```
did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q
```
{% endtab %}
{% endtabs %}

## Register DID
The `/v1/client/registerDid` endpoint registers the specified DID on the EBSI ledger.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/registerDid' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
The did url string
```
{% endtab %}
{% tab title="Response body schema" %}
```
Code 200
```
{% endtab %}
{% endtabs %}

E.g. Register did = _did:ebsi:zwdPobJGue3w86Gpqhq5Cni_ on the EBSI ledger.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/registerDid' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d 'did:ebsi:zwdPobJGue3w86Gpqhq5Cni'
```
{% endtab %}
{% tab title="Request body" %}
```
did:ebsi:zwdPobJGue3w86Gpqhq5Cni
```
{% endtab %}
{% endtabs %}

## Create timestamp
The `/v1/client/timestamp` endpoint creates a timestamp on the EBSI ledger, using the provided DID as a key. The data will be written to the data-field of the timestamp.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/timestamp' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '<request-body>'
```
{% endtab %}
{% tab title="Request body schema" %}
```
{
    "did": "string",
    "ethDidAlias": "string",
    "data": "string"
}
```
{% endtab %}
{% tab title="Response body schema" %}
```
The transaction hash
```
{% endtab %}
{% endtabs %}

E.g. Create a timestamp using did = _did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'POST' \
  'https://essif.ssikit.walt.id/v1/client/timestamp' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "did": "did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q",
  "data": "my-data"
}'
```
{% endtab %}
{% tab title="Request body" %}
```
{
    "did": "did:ebsi:zYubw2L8tCZSKKpAcMmCY2Q",
    "data": "my-data"
}
```
{% endtab %}
{% tab title="Response body" %}
```
0x9c60ca0094771afe4093b0e47260eb623d5d18140e188e671cf912609cd0e169
```
{% endtab %}
{% endtabs %}

## Load timestamp by id
The `/v1/client/timestamp/id/{timestampId}` endpoint loads the timestamp based on the provided parameter:
* timestampId - path parameter (required) - the timestamp id

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://essif.ssikit.walt.id/v1/client/timestamp/id/{timestampId}' \
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
The timestamp json object
```
{% endtab %}
{% endtabs %}

E.g. Load the timestamp having id = _uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv\_Q_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://essif.ssikit.walt.id/v1/client/timestamp/id/uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv_Q' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "blockNumber": 6434223,
    "data": "0x7b2274657374223a202234346239343965322d336661652d343564372d626666392d396464666436663666376134227d",
    "hash": "mEiBsHu0aNKVDJlqfyxS4pFYH4aFW86s0s60uJl+SmJT8aw",
    "href": "https://api.preprod.ebsi.eu/timestamp/v2/timestamps/uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv_Q",
    "timestamp": "2022-10-10T11:51:16.000Z",
    "timestampId": "uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv_Q",
    "timestampedBy": "0x635A4045A3f82d2C5597225614747c02998B112a",
    "transactionHash": "0x9c60ca0094771afe4093b0e47260eb623d5d18140e188e671cf912609cd0e169"
}
```
{% endtab %}
{% endtabs %}

## Load timestamp by hash
The `/v1/client/timestamp/txhash/{txhash}` endpoint loads the timestamp based on the provided parameter:
* txhash - path parameter (required) - the transaction hash

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://essif.ssikit.walt.id/v1/client/timestamp/txhash/{txhash}' \
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
The timestamp json object
```
{% endtab %}
{% endtabs %}

E.g. Load the timestamp having the transcation hash _0x9c60ca0094771afe4093b0e47260eb623d5d18140e188e671cf912609cd0e169_.

{% tabs %}
{% tab title="curl" %}
```
curl -X 'GET' \
  'https://essif.ssikit.walt.id/v1/client/timestamp/txhash/0x9c60ca0094771afe4093b0e47260eb623d5d18140e188e671cf912609cd0e169' \
  -H 'accept: application/json'
```
{% endtab %}
{% tab title="Response body" %}
```
{
    "blockNumber": 6434223,
    "data": "0x7b2274657374223a202234346239343965322d336661652d343564372d626666392d396464666436663666376134227d",
    "hash": "mEiBsHu0aNKVDJlqfyxS4pFYH4aFW86s0s60uJl+SmJT8aw",
    "href": "https://api.preprod.ebsi.eu/timestamp/v2/timestamps/uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv_Q",
    "timestamp": "2022-10-10T11:51:16.000Z",
    "timestampId": "uEiBEtXzl3QXshn5Z1V4dgZVtMlvnx3E1f2IWFDQVqzEv_Q",
    "timestampedBy": "0x635A4045A3f82d2C5597225614747c02998B112a",
    "transactionHash": "0x9c60ca0094771afe4093b0e47260eb623d5d18140e188e671cf912609cd0e169"
}
```
{% endtab %}
{% endtabs %}