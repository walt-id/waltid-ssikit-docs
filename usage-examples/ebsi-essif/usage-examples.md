# SSIKit usage examples for interaction with EBSI/ESSIF

The following subsections show several examples of interaction with the EBSI/ESSIF frameworks using the SSIKit command line interface, REST APIs and library SDK.

For more information about the EBSI/ESSIF support built into SSI Kit, refer to section [**EBSI/ESSIF - European SSI and blockchain infrastructures**](ecosystems-interoperability/ebsi-essif.md).

## EBSI DID registration

This use case describes the steps, which are required to register a DID on the EBSI blockchain.

### CLI

Key generation (type ECDSA Secp256k1, which is required for signing ETH transactions)

    ./ssikit.sh key gen -a Secp256k1
    => keyId: 7db4b285984640d485842c0b1ccdcf92

Generation of the DID document

    ./ssikit.sh did create -m ebsi -k 7db4b285984640d485842c0b1ccdcf92
    => DID: did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg

EBSI/ESSIF Onboarding flow.
> As prerequisite, the bearer token (validity of 15 min) from https://app.preprod.ebsi.eu/users-onboarding must be placed in file `data/ebsi/bearer-token.txt`

    ./ssikit.sh essif onboard --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg

After successfully completing the onboarding process, the Verifiable Authorization (validity of 6 months) from the Ebsi Onboarding Service is placed
in `data/ebsi/verifiable-authorization.json`

EBSI/ESSIF Auth API flow

    ./ssikit.sh essif auth-api --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg

After successfully completing the Auth API flow, the decrypted EBSI Access Token (validity of 15min) can be accessed in file: `/home/pp/dev/walt/data/ebsi/ebsi_access_token.json`

EBSI/ESSIF DID registration

    ./ssikit.sh essif did register --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg

DID Resolution (only to check if the DID was correctly anchored with the EBSI blockchain)

    ./ssikit.sh did resolve --did did:ebsi:241ou8rtrYnBokFALv3PGFeTRYQuLdyZnpFk3wFFhhiDKdLg

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

### REST API

First pull the latest container

    docker pull waltid/ssikit

Starting the container as RESTful service

    docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0

Key generation (type ECDSA Secp256k1, which is required for signing ETH transactions)

    curl -X POST "http://127.0.0.1:7000/v1/key/gen" -H  "accept: application/json" -H  "Content-Type: application/json" -d "{\"keyAlgorithm\":\"ECDSA_Secp256k1\"}"

Generation of the DID document

    curl -X POST "http://127.0.0.1:7000/v1/did/create" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"method\":\"ebsi\",\"keyAlias\":\"751da5b181e64475a811a374ae1a6923\"}"
    =>  did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY

EBSI/ESSIF Onboarding flow

    curl -X POST "http://127.0.0.1:7004/v1/client/onboard" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"bearerToken\":\"eyJhbGciOiJFUzI1NksiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2MzEwODYxODUsImlhdCI6MTYzMTA4NTI4NSwiaXNzIjoiZGlkOmVic2k6NGpQeGNpZ3ZmaWZaeVZ3eW01emp4YUtYR0pUdDdZd0Z0cGc2QVh0c1I0ZDUiLCJvbmJvYXJkaW5nIjoicmVjYXB0Y2hhIiwidmFsaWRhdGVkSW5mbyI6eyJhY3Rpb24iOiJsb2dpbiIsImNoYWxsZW5nZV90cyI6IjIwMjEtMDktMDhUMDc6MTQ6NDRaIiwiaG9zdG5hbWUiOiJhcHAucHJlcHJvZC5lYnNpLmV1Iiwic2NvcmUiOjAuOSwic3VjY2VzcyI6dHJ1ZX19.InIzqVIAON07zuFkt6afLv3q6IO9XuqcmiH8CnVo6lMfFQMBv1Uz91-gkn__0RuYzzTgzPWBCmUn8E3tw_xE5Q\",\"did\":\"did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY\"}"

EBSI/ESSIF Auth flow

    curl -X POST "http://127.0.0.1:7004/v1/client/auth" -H  "accept: text/plain" -H  "Content-Type: text/plain" -d "did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY"

EBSI/ESSIF DID registration

    curl -X POST "http://127.0.0.1:7004/v1/client/registerDid" -H  "accept: text/plain" -H  "Content-Type: text/plain" -d "did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY"

DID Resolution (only to check if the DID was correctly anchored with the EBSI blockchain)

    curl -X POST "http://127.0.0.1:7000/v1/did/resolve" -H  "accept: text/plain" -H  "Content-Type: application/json" -d "{\"did\":\"did:ebsi:22tCpv2yh4EJLm6o18JiS2AebaQAL6QcHH83mS6Cz94QumtY\"}"

### Code example

The [DidEbsi example](https://github.com/walt-id/waltid-ssikit-examples/blob/master/src/main/java/id/walt/ssikitexamples/DidEbsi.java) shows how to register a DID EBSI in Java.

        KeyService keyService = KeyService.Companion.getService();
        DidEbsiService didEbsiService = DidEbsiService.Companion.getService();

        var keyId = keyService.generate(KeyAlgorithm.ECDSA_Secp256k1);
     
        var didEbsi = DidService.INSTANCE.create(DidMethod.ebsi, keyId.getId());

        EssifClient.INSTANCE.onboard(didEbsi, null);

        EssifClient.INSTANCE.authApi(didEbsi);

        didEbsiService.registerDid(didEbsi, ethKeyId.getId());

[comment]: <> (## EBSI Trusted Issuer Registry)

[comment]: <> (## EBSI Trusted Schema Registry)

## EBSI Issuer/Holder & Verifier

This is a holistic SSI use case, which demonstrates the setup of two identities for an _Issuer_ and a _Holder_ on the EBSI ledger. It furthermore shows the steps to issue two diploma
credentials to the _Holder_ (e.g student), which then creates a Verifiable Presentation including both credentials in order to be verified. The _Verifier_ then resolves the DIDs from the
EBSI ledger and uses the corresponding public keys to verify the signatures from the issued credentials.

### CLI

Creating a work-dir for all three parties of the trust triangle (Issuer, Holder & Verifier)

    mkdir issuer
    mkdir holder
    mkdir verifier

Setting up the Issuer (generating a key, EBSI DID and registering it on the EBSI ledger)

    cd issuer/
    docker run -itv $(pwd)/data:/app/data waltid/ssikit key gen -a Secp256k1
    docker run -itv $(pwd)/data:/app/data waltid/ssikit did create -m ebsi -k 48ff0d51910c4dc4b05b420547a05f9f
    cat > data/bearer-token.txt    
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif onboard --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC data/bearer-token.txt
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif auth-api --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif did register --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC 

Setting up the Holder (generating a key, EBSI DID and registering it on the EBSI ledger)

    cd ../holder/
    docker run -itv $(pwd)/data:/app/data waltid/ssikit key gen -a Secp256k1
    docker run -itv $(pwd)/data:/app/data waltid/ssikit did create -m ebsi -k 2c497f88593b4db9a571fb7146606fc2
    cat > data/bearer-token.txt   
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif onboard --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr data/bearer-token.txt
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif auth-api --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr
    docker run -itv $(pwd)/data:/app/data waltid/ssikit essif did register --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr

Setting up the Verifier (only run ssikit in order to initialize the work-dir)

    cd ../verifier/
    docker run -itv $(pwd)/data:/app/data waltid/ssikit -h

Issuing two credentials, one Bachelor & one Master degree (values are defined by running the interactive shell). Both credentials are based on
the [VerifiableDiploma Template](https://github.com/walt-id/waltid-ssikit-vclib/blob/master/src/test/resources/serialized/VerifiableDiploma.json)

    cd ../issuer/
    docker run -itv $(pwd)/data:/app/data waltid/ssikit vc issue -i did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC -s did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr -t VerifiableDiploma --interactive data/bachelor.json
    docker run -itv $(pwd)/data:/app/data waltid/ssikit vc issue -i did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC -s did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr -t VerifiableDiploma --interactive data/master.json
    cp data/master.json data/bachelor.json ../holder/data

Creating the Verifiable Presentation containing both - the Master and the Bachelor credential

    cd ../holder/
    docker run -itv $(pwd)/data:/app/data waltid/ssikit vc present --holder-did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr data/master.json data/bachelor.json
    cp data/vc/presented/vp-1632686198721.json ../verifier/data

Verifying the Verifiable Presentation by resolving DIDs (public keys) from the EBSI ledger and verifying the signatures from each VC (Bachelor & Master degree credential) and from
the VP itself.

    docker run -itv $(pwd)/data:/app/data waltid/ssikit vc verify -p TrustedIssuerDidPolicy -p TrustedSubjectDidPolicy -p JsonSchemaPolicy -p SignaturePolicy data/vp-1632686198721.json

    Output:    
    Walt.ID SSI-Kit 1.0-SNAPSHOT (running on Java 16.0.2+7-67)

    Verifying from file data/vp-1632686198721.json ...

    Results:
    
    TrustedIssuerDidPolicy:          true
    TrustedSubjectDidPolicy:                 true
    JsonSchemaPolicy:                true
    Verified:                true

> Note that the order of the policies does matter. The TrustedIssuerDidPolicy & TrustedSubjectDidPolicy are verifying the presents of the DIDs on the EBSI ledger, and if they are,
the keys are imported to the key-store. Once the keys are available, the SignaturePolicy can be applied in order to verify each signature.
