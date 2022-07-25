# REST APIs

### Installation & Running the Project

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
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
./ssikit.sh serve 
```
{% endtab %}

{% tab title="Docker" %}
Pull the docker container directly from docker hub and run the project

```
docker run -itv $(pwd)/data:/app/data waltid/ssikit serve
```

This will create a folder called data in your current directory as storge for the VC, DIDs, Keys and other things which need to be stored in order to provide all the fuctionality.
{% endtab %}
{% endtabs %}



After successfully running the project, you will have the endpoints, described below, available for use. Make sure to get a general overview of the functionality exposed by each endpoint by visiting the URL and inspecting the swagger docs hosted thereunder. You can also use the publicly hosted version on walt.id for reference.



**Exposed endpoints:**



| Type           | Locally               | General Available                                                                      |
| -------------- | --------------------- | -------------------------------------------------------------------------------------- |
| Signatory API  | http://127.0.0.1:7001 | [https://signatory.ssikit.walt-test.cloud/](https://signatory.ssikit.walt-test.cloud/) |
| Custodian API  | http://127.0.0.1:7002 | [https://custodian.ssikit.walt-test.cloud/](https://custodian.ssikit.walt-test.cloud/) |
| Auditor API    | http://127.0.0.1:7003 | [https://auditor.ssikit.walt-test.cloud/](https://auditor.ssikit.walt-test.cloud/)     |
| Core API       | http://127.0.0.1:7000 | [https://core.ssikit.walt-test.cloud/](https://core.ssikit.walt-test.cloud/)           |
| ESSIF API      | http://127.0.0.1:7004 | [https://essif.ssikit.walt-test.cloud/](https://essif.ssikit.walt-test.cloud/)         |

{% hint style="info" %}
The Core API exposes most of the funtionalities provided by the SSI Kit, however newer features will only be released in the other API endpoints. Therefore, it is recommended to use the Signatory API, Custodian API and Auditor API for most use cases.
{% endhint %}
