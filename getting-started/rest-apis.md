# REST API

Manage keys, DIDs, issue Verifiable Credentials, and verify them using the SSI-Kit's REST API.

### Installation & Running the Project

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
{% tab title="Docker" %}
Pull the docker container directly from docker hub and run the project

```
docker run -p 7000-7004:7000-7004 -itv $(pwd)/data:/app/data waltid/ssikit serve -b 0.0.0.0
```

This will create a folder called data in your current directory as storge for the VC, DIDs, Keys and other things which need to be stored in order to provide all the fuctionality.
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

3\. Run the project

The first time you run the command you will be asked to built the project. You can confirm the prompt.

```
./ssikit.sh serve 
```
{% endtab %}
{% endtabs %}

If you want to get a more detailed overview of the options provided for building the project on your machine, please refer to [building the project](build.md).

After successfully running the project, you will have the endpoints, described below, available for use.&#x20;

**Exposed endpoints:**

| Type                        | Locally               | General Available                                                      |
| --------------------------- | --------------------- | ---------------------------------------------------------------------- |
| Signatory API - For Issuers | http://127.0.0.1:7001 | [https://signatory.ssikit.walt.id/](https://signatory.ssikit.walt.id/) |
| Custodian API - For Holders | http://127.0.0.1:7002 | [https://custodian.ssikit.walt.id/](https://custodian.ssikit.walt.id/) |
| Auditor API - For Verifiers | http://127.0.0.1:7003 | [https://auditor.ssikit.walt.id/](https://auditor.ssikit.walt.id/)     |
| Core API                    | http://127.0.0.1:7000 | [https://core.ssikit.walt.id/](https://core.ssikit.walt.id/)           |
| ESSIF API                   | http://127.0.0.1:7004 | [https://essif.ssikit.walt.id/](https://essif.ssikit.walt.id/)         |

{% hint style="info" %}
The Core API exposes most of the funtionalities provided by the SSI Kit, however newer features will only be released in the other API endpoints. Therefore, it is recommended to use the Signatory API, Custodian API and Auditor API for most use cases.
{% endhint %}

### Next Steps

* [Issuance](rest-apis/signatory-api.md) - Learn how to issue credentials
* [Holders](rest-apis/custodian-api/) - Learn how to maintain secrets and sensitive data (e.g. keys, Verifiable Credentials)
* [Verifiers](rest-apis/auditor-api.md) - Learn how to verify credentials

### Tutorials

* [My First VC](../tutorials/my-first-vc.md) - Play through a whole use case from Issuance to Verification

