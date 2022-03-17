# Key Export

Keys can be exported in the JWK (default) and the PEM format. On default only the public key will be exported. Private keys my also be exported in case the underlying keystore supports that.

## CLI

```
./ssikit.sh key export <keyId>

./ssikit.sh key export -f PEM --priv 447709157adb4ac7aae3184aeb63ffa8
```

Obtain the keyId by running "./ssikit.sh key list".

## REST API

The conent of fiel ExportKeyRequest.json (request body) may look as follows: { "keyAlias": "769dd4d30a9b4fe3bcfdc932135acb9b", "format": "JWK", "exportPrivate": true }

```
curl --data "@ExportKeyRequest.json" -X POST "http://127.0.0.1:7000/v1/key/export"
```

## Code example

```
val keyId = KeyService.getService().export(keyAlias, KeyFormat.JWK, KeyType.PRIVATE)
```

Exporting keys in code is demonstrated as part of the [KeyManagement example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/kotlin/id/walt/ssikitexamples/KeyManagement.kt)

##
