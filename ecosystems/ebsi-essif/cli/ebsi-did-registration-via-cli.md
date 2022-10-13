# EBSI DID Registration (via CLI)

Create a directory for the generated data (if not present already)

```
mkdir -p data/ebsi
```

Paste your bearer token from https://app.preprod.ebsi.eu/users-onboarding in file _data/ebsi/bearer-token.txt_

```
cat > data/ebsi/bearer-token.txt 
```

Use the **walt.id** command line tool for creating and registering the DID EBSI.

```
"<cli-tool>" can be replaced with the startup-script "./ssikit.sh" (when running the code-base)

e.g. ./ssikit.sh  key gen -a Secp256k1

"<cli-tool>" can be replaced with  "docker run -itv $(pwd)/data:/app/data" (when running Docker)

In case of Docker add: "-p 7000-7003:7000-7003" when the REST APIs are required.
In case of Docker add: "-v $(pwd)/templates:/app/templates" when VC templates should be used.

e.g. docker run -itv $(pwd)/data:/app/data -v $(pwd)/templates:/app/templates -p 7000-7003:7000-7003 ssikit vc -h
```

Create the DID controlling key and the ETH signing key. Note, that if a Secp256k1 DID controlling key is used, then the same key will be used for signing the ETH transaction automatically.

```
<cli-tool>  key gen -a Secp256k1
```

Create the DID document

```
<cli-tool> did -m ebsi -k <keyId>
```

Run the onboarding flow in order to receive the Verifiable Authentication, which is valid for 6 months

```
<cli-tool> essif onboard -d <did-ebsi>
```

Run the auth-api flow for getting a short lived (15min) access token for write access to the ledger

```
<cli-tool> essif auth-api -d <did-ebsi>
```

Register the DID on the ledger. Optionally the key for signing the ETH transaction can be specified (parameter _k_), if it is another key then the DID controlling key

```
<cli-tool> essif did register -d <did-ebsi> 
```

Resolve DID EBSI from the command line or directly via the Swagger interface https://api.preprod.ebsi.eu/docs/?urls.primaryName=DID%20Registry%20API#/DID%20Registry/get-did-registry-v2-identifier

```
<cli-tool> did resolve --did <did-ebsi> 
```
