---
noIndex: true
---

# Build end-to-end use cases

This is a holistic SSI use case, which demonstrates the setup of two identities for an _Issuer_ and a _Holder_ on the EBSI blockchain. It also shows the steps to issue two diploma credentials to the _Holder_ (e.g student), which then creates a Verifiable Presentation including both credentials in order to be verified. The _Verifier_ then resolves the DIDs from the EBSI ledger and uses the corresponding public keys to verify the signatures from the issued credentials.

## CLI

Creating a work-dir for all three parties of the trust triangle (Issuer, Holder & Verifier)

```
mkdir issuer
mkdir holder
mkdir verifier
```

Setting up the Issuer (generating a key, EBSI DID and registering it on the EBSI ledger)

```
cd issuer/
docker run -itv $(pwd)/data:/app/data waltid/ssikit key gen -a Secp256k1
docker run -itv $(pwd)/data:/app/data waltid/ssikit did create -m ebsi -k 48ff0d51910c4dc4b05b420547a05f9f
cat > data/bearer-token.txt    
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif onboard --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC data/bearer-token.txt
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif auth-api --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif did register --did did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC 
```

Setting up the Holder (generating a key, EBSI DID and registering it on the EBSI ledger)

```
cd ../holder/
docker run -itv $(pwd)/data:/app/data waltid/ssikit key gen -a Secp256k1
docker run -itv $(pwd)/data:/app/data waltid/ssikit did create -m ebsi -k 2c497f88593b4db9a571fb7146606fc2
cat > data/bearer-token.txt   
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif onboard --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr data/bearer-token.txt
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif auth-api --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr
docker run -itv $(pwd)/data:/app/data waltid/ssikit essif did register --did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr
```

Setting up the Verifier (only run ssikit in order to initialize the work-dir)

```
cd ../verifier/
docker run -itv $(pwd)/data:/app/data waltid/ssikit -h
```

Issuing two credentials, one Bachelor & one Master degree (values are defined by running the interactive shell). Both credentials are based on the [VerifiableDiploma Template](https://github.com/walt-id/waltid-ssikit-vclib/blob/master/src/test/resources/serialized/VerifiableDiploma.json)

```
cd ../issuer/
docker run -itv $(pwd)/data:/app/data waltid/ssikit vc issue -i did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC -s did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr -t VerifiableDiploma --interactive data/bachelor.json
docker run -itv $(pwd)/data:/app/data waltid/ssikit vc issue -i did:ebsi:22NPNHrBUWCKDJWuvpJD5s2V7JZNQRQvajMHP9hiky57nfhC -s did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr -t VerifiableDiploma --interactive data/master.json
cp data/master.json data/bachelor.json ../holder/data
```

Creating the Verifiable Presentation containing both - the Master and the Bachelor credential

```
cd ../holder/
docker run -itv $(pwd)/data:/app/data waltid/ssikit vc present --holder-did did:ebsi:2YiP8ae91JPNQ86YQWvPytdBP8rfKZYR8r95CE8aZ1ooUatr data/master.json data/bachelor.json
cp data/vc/presented/vp-1632686198721.json ../verifier/data
```

Verifying the Verifiable Presentation by resolving DIDs (public keys) from the EBSI ledger and verifying the signatures from each VC (Bachelor & Master degree credential) and from the VP itself.

```
docker run -itv $(pwd)/data:/app/data waltid/ssikit vc verify -p TrustedIssuerDidPolicy -p TrustedSubjectDidPolicy -p JsonSchemaPolicy -p SignaturePolicy data/vp-1632686198721.json

Output:    
Walt.ID SSI-Kit 1.0-SNAPSHOT (running on Java 16.0.2+7-67)

Verifying from file data/vp-1632686198721.json ...

Results:

TrustedIssuerDidPolicy:          true
TrustedSubjectDidPolicy:                 true
JsonSchemaPolicy:                true
Verified:                true
```

> Note that the order of the policies does matter. The TrustedIssuerDidPolicy & TrustedSubjectDidPolicy are verifying the presents of the DIDs on the EBSI ledger, and if they are, the keys are imported to the key-store. Once the keys are available, the SignaturePolicy can be applied in order to verify each signature.
