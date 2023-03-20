# Onboarding & DIDs

This use case describes the steps, which are required to register a DID on the EBSI blockchain.

## CLI

Key generation (type ECDSA Secp256k1, which is required for signing ETH transactions)

```
./ssikit.sh key gen -a Secp256k1
=> keyId: 7db4b285984640d485842c0b1ccdcf92
```

Generation of the DID document

```
./ssikit.sh did create -m ebsi -k 7db4b285984640d485842c0b1ccdcf92
=> DID: did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg
```

EBSI/ESSIF Onboarding flow.

> As prerequisite, the bearer token (validity of 15 min) from [https://app-pilot.ebsi.eu/users-onboarding/v2](https://app-pilot.ebsi.eu/users-onboarding/v2) must be placed in file `data/ebsi/bearer-token.txt`

```
./ssikit.sh essif onboard --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg
```

After successfully completing the onboarding process, the Verifiable Authorization (validity of 6 months) from the Ebsi Onboarding Service is placed in `data/ebsi/verifiable-authorization.json`

EBSI/ESSIF Auth API flow

```
./ssikit.sh essif auth-api --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg
```

After successfully completing the Auth API flow, the decrypted EBSI Access Token (validity of 15min) can be accessed in file: `/home/pp/dev/walt/data/ebsi/ebsi_access_token.json`

EBSI/ESSIF DID registration

```
./ssikit.sh essif did register --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg
```

DID Resolution (only to check if the DID was correctly anchored with the EBSI blockchain)

```
./ssikit.sh did resolve --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg
```

The resulting DID document from the EBSI blockchain:

```
{
  "authentication": [
    "did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg#7db4b285984640d485842c0b1ccdcf92"
  ],
  "@context": [
    "https://w3id.org/did/v1"
  ],
  "id": "did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg",
  "verificationMethod": [
    {
      "controller": "did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg",
      "id": "did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg#7db4b285984640d485842c0b1ccdcf92",
      "publicKeyJwk": {
        "alg": "ES256K",
        "crv": "secp256k1",
        "kid": "7db4b285984640d485842c0b1ccdcf92",
        "kty": "EC",
        "use": "sig",
        "x": "wpFN5Pi6v3MiM6B5Awd4lqZk1usQQDDUAvVNXqXp4uw",
        "y": "iHVFCdaeIYbZheeQOtBCUpWCtoQhfPCx5N5MQuhbEFo"
      },
      "type": "Secp256k1VerificationKey2018"
    }
  ]
}
```

## REST API

First pull the latest container

```
docker pull waltid/ssikit
```

Starting the container as RESTful service

```
docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0
```

Key generation (type ECDSA Secp256k1, which is required for signing ETH transactions)

```
curl -X POST "http://127.0.0.1:7000/v1/key/gen" -H  "accept: application/json" -H  "Content-Type: application/json" -d "{\"keyAlgorithm\":\"ECDSA_Secp256k1\"}"
```

Generation of the DID document

```
curl -X POST "http://127.0.0.1:7000/v1/did/create" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"method\":\"ebsi\",\"keyAlias\":\"751da5b181e64475a811a374ae1a6923\"}"
=>  did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY
```

EBSI/ESSIF Onboarding flow

```
curl -X POST "http://127.0.0.1:7004/v1/client/onboard" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"bearerToken\":\"eyJhbGciOiJFUzI1NksiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2MzEwODYxODUsImlhdCI6MTYzMTA4NTI4NSwiaXNzIjoiZGlkOmVic2k6NGpQeGNpZ3ZmaWZaeVZ3eW01emp4YUtYR0pUdDdZd0Z0cGc2QVh0c1I0ZDUiLCJvbmJvYXJkaW5nIjoicmVjYXB0Y2hhIiwidmFsaWRhdGVkSW5mbyI6eyJhY3Rpb24iOiJsb2dpbiIsImNoYWxsZW5nZV90cyI6IjIwMjEtMDktMDhUMDc6MTQ6NDRaIiwiaG9zdG5hbWUiOiJhcHAucHJlcHJvZC5lYnNpLmV1Iiwic2NvcmUiOjAuOSwic3VjY2VzcyI6dHJ1ZX19.InIzqVIAON07zuFkt6afLv3q6IO9XuqcmiH8CnVo6lMfFQMBv1Uz91-gkn__0RuYzzTgzPWBCmUn8E3tw_xE5Q\",\"did\":\"did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY\"}"
```

EBSI/ESSIF Auth flow

```
curl -X POST "http://127.0.0.1:7004/v1/client/auth" -H  "accept: text/plain" -H  "Content-Type: text/plain" -d "did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY"
```

EBSI/ESSIF DID registration

```
curl -X POST "http://127.0.0.1:7004/v1/client/registerDid" -H  "accept: text/plain" -H  "Content-Type: text/plain" -d "did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY"
```

DID Resolution (only to check if the DID was correctly anchored with the EBSI blockchain)

```
curl -X POST "http://127.0.0.1:7000/v1/did/resolve" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"did\":\"did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY\"}"
```

## Code example

The [did:ebsi example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/java/id/walt/ssikitexamples/DidEbsi.java) shows how to register an EBSI DID in Java.

```
    KeyService keyService = KeyService.Companion.getService();
    DidEbsiService didEbsiService = DidEbsiService.Companion.getService();

    var keyId = keyService.generate(KeyAlgorithm.ECDSA_Secp256k1);
 
    var didEbsi = DidService.INSTANCE.create(DidMethod.ebsi, keyId.getId());

    EssifClient.INSTANCE.onboard(didEbsi, null);

    EssifClient.INSTANCE.authApi(didEbsi);

    didEbsiService.registerDid(didEbsi, ethKeyId.getId());
```

##
