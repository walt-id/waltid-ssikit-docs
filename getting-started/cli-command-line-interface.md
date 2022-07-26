# CLI | Command Line Interface



### Installation & Running the Project

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
{% tab title="Docker" %}
1. Pulling the project directly from DockerHub

```
alias ssikit="docker container run -p 7000-7004:7000-7004 -itv $(pwd)/data:/app/data docker.io/waltid/ssikit"
```



2\. Getting an overview of the commands and options available

```
ssikit -h
```
{% endtab %}

{% tab title="Local" %}
1. Clone the project

```
git clone https://github.com/walt-id/waltid-ssikit.git
```



2\. Change the folder

```
cd waltid-ssikit/
```



3\. Run the project&#x20;

The first time you run the command you will be asked to built the project. You can confirm the prompt.

```
./ssikit.sh -h
```

You will now see an overview of all the different commands and options available.



4\. Set an alias

To make it more convient to use, you can also set an alias as follows for the wrapper script:

```
alias ssikit="./ssikit.sh"
```



5\. Get the overview again

```
ssikit -h
```
{% endtab %}
{% endtabs %}

If you want to get a more detailed overview of the options provided for building the project on your machine, please refer to the [building the project](build/).

### Response configuration

For debug infos add "-v" e.g.:

```
ssikit -v

ssikit -v did create
```

### Example commands

```
ssikit key gen --algorithm Ed25519

ssikit key list

ssikit did create -m web

ssikit did resolve --did did:web:mattr.global

ssikit -v vc issue --issuer-did did:key:z6MkmNMF2... --subject-did did:key:zjkl2sd...

ssikit vc verify data/vc/created/vc-1614291790088-default.json

ssikit -v vc present data/vc/created/vc-1614291790088-default.json

ssikit vc verify -p data/vc/presented/vp-1614291892489.json
```



## API Service

To expose the API service using the CLI tool or the docker container, use one of the following commands:

Show all options for specifying bind address and ports:

```
./ssikit.sh serve --help
docker run -itv $(pwd)/data:/app/data -p 192.168.0.1:7000-7003:7000-7003 ssikit serve --help
```

On localhost only using the default ports 7000-7003

```
./ssikit.sh serve
```

Binding on all network interfaces, using the default ports 7000-7003

```
./ssikit.sh serve -b 0.0.0.0

docker run -itv $(pwd)/data:/app/data -p 7000-7003:7000-7003 ssikit serve -b 0.0.0.0
```

Binding on a specific network interface (e.g.: 192.168.0.1)

```
./ssikit.sh serve -b 192.168.0.1
```

Using docker one needs to bind to 0.0.0.0 in the container and limit the binding from outside using the docker run -p syntax like so:

```
docker run -itv $(pwd)/data:/app/data -p 192.168.0.1:7000-7003:7000-7003 ssikit serve -b 0.0.0.0
```

Use custom ports by using the -p (Core API), -e (ESSIF API), -s (Signatory API) command options

```
./ssikit.sh serve -p 8000 -e 8001 -s 8002

docker run -itv $(pwd)/data:/app/data -p 8000-8002:8000-8002 ssikit serve -b 0.0.0.0 -p 8000 -e 8001 -s 8002
```

### EBSI DID Registration (via CLI)

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
