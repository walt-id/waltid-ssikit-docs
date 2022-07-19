# REST APIs

This section outlines the APIs of the SSI Kit:

* Signatory API
* Custodian API
* Auditor API
* Core API
* ESSIF Connector API

To review the Swagger doc of each API, you can either use the API which is general available to get an overview of the different endpoints or run the project locally, and you will get the following endpoints exposed:

|                | Locally               | General Available                                                                      |
| -------------- | --------------------- | -------------------------------------------------------------------------------------- |
| Signatory API  | http://127.0.0.1:7001 | [https://signatory.ssikit.walt-test.cloud/](https://signatory.ssikit.walt-test.cloud/) |
| Custodian API  | http://127.0.0.1:7002 | [https://custodian.ssikit.walt-test.cloud/](https://custodian.ssikit.walt-test.cloud/) |
| Auditor API    | http://127.0.0.1:7003 | [https://auditor.ssikit.walt-test.cloud/](https://auditor.ssikit.walt-test.cloud/)     |
| Core API       | http://127.0.0.1:7000 | [https://core.ssikit.walt-test.cloud/](https://core.ssikit.walt-test.cloud/)           |
| ESSIF API      | http://127.0.0.1:7004 | [https://essif.ssikit.walt-test.cloud/](https://essif.ssikit.walt-test.cloud/)         |

{% hint style="info" %}
The Core API exposes most of the funtionalities provided by the SSI Kit, however newer features will only be released in the other API endpoints. Therefore, it is recommended to use the Signatory API, Custodian API and Auditor API for most use cases.
{% endhint %}

To have it locally served, run the **serve** command of the CLI tool and navigate to the corresponding web pages:

```
    ./ssikit.sh serve
```

or with Docker:

```
    docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0
    
```
