# Key Import

The SSI Kit allows importing of private and public JWK keys. Based on the _**kid**_ of the JWK key the key object in the underlying key store will be created and can be accessed further on.

The JWK key in file key.json, may look like:

{"kty":"EC","use":"sig","crv":"secp256k1","kid":"1de48338fc1040cb8cf32bb3f1580176","x":"uKMK0Sbkema87A6-0gGBjqKwD3gJIwer--As\_jgHeBs","y":" JTuepzr9At5U0atJFq2xGkSUMniQZ2L2D9vbYnEV8BY","alg":"ES256K"}

## CLI

```
./ssikit.sh key import key.json
```

## REST API

```
curl --data "@key.json" -X POST "http://localhost:7000/v1/key/import"
```

## Code example

```
val keyId = KeyService.getService().import(privKeyJwk)
```

Importing keys in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)
