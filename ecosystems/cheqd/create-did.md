# Create DID

DID _cheqd_ scheme is supported with the same functionality as the other DID schemes (see [decentralized-identifiers.md](../../getting-started/cli-command-line-interface/decentralized-identifiers.md "mention") for command-line interface or [#decentralised-identifiers](../../getting-started/rest-apis/core-api.md#decentralised-identifiers "mention") for REST API). Creating a `did:cheqd` will also onboard with the [Universal Registrar](https://uniregistrar.io). The created DID can be checked at [https://resolver.cheqd.net/1.0/identifiers/{your-did}](https://resolver.cheqd.net/1.0/identifiers/%7Byour-did%7D) or using the [Universal Resolver](https://dev.uniresolver.io).

`did:cheqd` requires keys of type `Ed25519`. They can be either:

* [imported](../../usage-examples/key-management/key-import.md) into SSIKit - and further used when creating the did by specifying the `kid`
* or [created](../../usage-examples/key-management/key-generation.md) with SSIKit
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

{% swagger method="post" path="/" baseUrl="https://core.ssikit.walt.id/v1/did/create" summary="Create a did:cheqd document on the test or main network" expanded="false" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="method" required="true" %}
did schema (use cheqd)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="network" %}
mainnet or testnet
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```
did:cheqd:testnet:dc3a71fb-be38-4145-a80a-dfc67628ab53
```
{% endswagger-response %}
{% endswagger %}

