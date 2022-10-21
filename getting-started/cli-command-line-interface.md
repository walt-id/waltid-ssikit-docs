# CLI | Command Line Interface

### Installation & Running the Project

Choos between a Docker or a JVM-based runtime.

{% tabs %}
{% tab title="Docker" %}
Make sure you have Docker build environment installed on your machine.



1. Pulling the project directly from DockerHub

```
docker pull waltid/ssikit
```



2\. Setting and alias for convenience

```
alias ssikit="docker container run -p 7000-7004:7000-7004 -itv $(pwd)/data:/app/data docker.io/waltid/ssikit"
```



3\. Getting an overview of the commands and options available

```
ssikit -h
```
{% endtab %}

{% tab title="Local" %}
Make sure you have  a JDK 16+ build environment including Gradle installed on your machine.



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

If you want to get a more detailed overview of the options provided for building the project on your machine, please refer to [building the project](build.md).

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



### Components

You can now dive deeper into the different components forming the SSI Kit and their functionality provided:

* [Key Management](cli-command-line-interface/key-management.md)
* [Decentralized Identifiers](cli-command-line-interface/decentralized-identifiers.md)
* [Verifiable Credentials](cli-command-line-interface/verifiable-credentials.md)

