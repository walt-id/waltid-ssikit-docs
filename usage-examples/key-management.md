---
description: Learn about key management.
---

# Key Management | Examples

This section outlines key management use cases that are covered by the SSI Kit. The use cases can be implemented and demonstrated either by usage of the CLI tool, the REST API or directly in code.

## Key Generation

The SSI Kit facilitates the convenient generation of cryptographic keys. Currently, the following asymmetric key types are supported:

* EdDSA E22519
* ECDSA Secp256k1

By calling the key generation command the algorithm can be defined, whereas the default algorithm is _**EdDSA E22519**_ in case no parameter is provided.

### CLI

```
./ssikit.sh key gen -a Secp256k1
```

### REST API

Body in GenKeyRequest.json: { "keyAlgorithm":"ECDSA\_Secp256k1" }

```
curl --data "@GenKeyRequest.json" -X POST "http://0.0.0.0:7000/v1/key/gen"
```

### Code example

```
val keyId = KeyService.getService().generate(KeyAlgorithm.EdDSA_Ed25519)
```

Key generation in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)

## Key Export

Keys can be exported in the JWK (default) and the PEM format. On default only the public key will be exported. Private keys my also be exported in case the underlying keystore supports that.

### CLI

```
./ssikit.sh key export <keyId>

./ssikit.sh key export -f PEM --priv 447709157adb4ac7aae3184aeb63ffa8
```

Obtain the keyId by running "./ssikit.sh key list".

### REST API

The conent of fiel ExportKeyRequest.json (request body) may look as follows: { "keyAlias": "769dd4d30a9b4fe3bcfdc932135acb9b", "format": "JWK", "exportPrivate": true }

```
curl --data "@ExportKeyRequest.json" -X POST "http://127.0.0.1:7000/v1/key/export"
```

### Code example

```
val keyId = KeyService.getService().export(keyAlias, KeyFormat.JWK, KeyType.PRIVATE)
```

Exporting keys in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)

## Key Import

The SSI Kit allows importing of private and public JWK keys. Based on the _**kid**_ of the JWK key the key object in the underlying key store will be created and can be accessed further on.

The JWK key in file key.json, may look like:

{"kty":"EC","use":"sig","crv":"secp256k1","kid":"1de48338fc1040cb8cf32bb3f1580176","x":"uKMK0Sbkema87A6-0gGBjqKwD3gJIwer--As\_jgHeBs","y":" JTuepzr9At5U0atJFq2xGkSUMniQZ2L2D9vbYnEV8BY","alg":"ES256K"}

### CLI

```
./ssikit.sh key import key.json
```

### REST API

```
curl --data "@key.json" -X POST "http://localhost:7000/v1/key/import"
```

### Code example

```
val keyId = KeyService.getService().import(privKeyJwk)
```

Importing keys in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)
