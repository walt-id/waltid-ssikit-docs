---
noIndex: true
---

# Create DID

DID _cheqd_ scheme is supported with the same functionality as the other DID schemes (see [decentralized-identifiers.md](../../getting-started/cli-command-line-interface/decentralized-identifiers.md "mention") for command-line interface or [#decentralised-identifiers](../../getting-started/rest-apis/core-api/#decentralised-identifiers "mention") for REST API). Creating a `did:cheqd` will also onboard with the [Universal Registrar](https://uniregistrar.io). The created DID can be checked at [https://resolver.cheqd.net/1.0/identifiers/{your-did}](https://resolver.cheqd.net/1.0/identifiers/%7Byour-did%7D) or using the [Universal Resolver](https://dev.uniresolver.io).

`did:cheqd` requires keys of type `Ed25519`. They can be either:

* [imported](broken-reference) into SSIKit - and further used when creating the did by specifying the `kid`
* or [created](broken-reference) with SSIKit
  * standalone
  * by default when running the did-create command

### Using the CLI | Command Line Interface

[Detailed instructions](../../getting-started/cli-command-line-interface.md) on how to build and run the SSI-Kit's CLI.

E.g. create a `did:cheqd` on `testnet` and also create the key for it by default

```
ssikit did create -m cheqd -n testnet
```

or

```
ssikit did create -m cheqd --network testnet
```

### Using the REST API

[Detailed instructions](../../getting-started/rest-apis.md) on how to build and run the SSI-Kit's REST API.&#x20;

## Create a did:cheqd document on the test or main network

<mark style="color:green;">`POST`</mark> `https://core.ssikit.walt.id/v1/did/create/`

#### Request Body

| Name                                     | Type   | Description            |
| ---------------------------------------- | ------ | ---------------------- |
| method<mark style="color:red;">\*</mark> | String | did schema (use cheqd) |
| network                                  | String | mainnet or testnet     |

{% tabs %}
{% tab title="201: Created " %}
```
did:cheqd:testnet:dc3a71fb-be38-4145-a80a-dfc67628ab53
```
{% endtab %}
{% endtabs %}

