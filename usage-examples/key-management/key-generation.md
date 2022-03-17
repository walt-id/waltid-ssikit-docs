# Key Generation

The SSI Kit facilitates the convenient generation of cryptographic keys. Currently, the following asymmetric key types are supported:

* EdDSA E22519
* ECDSA Secp256k1

By calling the key generation command the algorithm can be defined, whereas the default algorithm is _**EdDSA E22519**_ in case no parameter is provided.

## CLI

```
./ssikit.sh key gen -a Secp256k1
```

## REST API

Body in GenKeyRequest.json: { "keyAlgorithm":"ECDSA\_Secp256k1" }

```
curl --data "@GenKeyRequest.json" -X POST "http://0.0.0.0:7000/v1/key/gen"
```

## Code example

```
val keyId = KeyService.getService().generate(KeyAlgorithm.EdDSA_Ed25519)
```

Key generation in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)
