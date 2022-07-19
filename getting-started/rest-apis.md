# REST APIs

This sections outlines the APIs of the SSI Kit:

* Signatory API
* Custodian API
* Auditor API
* Core API
* ESSIF Connector API

To review the Swagger doc of each API, you can either use the API which is [general available](https://core.ssikit.walt-test.cloud/) to get an overview of the different endpoints or run the project locally: &#x20;

&#x20;run the **serve** command of the CLI tool and navigate to the corresponding web pages:

```
    ./ssikit.sh serve
```

or with Docker:

```
    docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0
```

* Signatory API: http://127.0.0.1:7001
* Custodian API: http://127.0.0.1:7002
* Auditor API: http://127.0.0.1:7003
* Core API: http://127.0.0.1:7000
* ESSIF API: http://127.0.0.1:7004

{% hint style="info" %}
The Core API exposes most of the funtionalities provided by the SSI Kit, however newer features will only be released in the other API endpoints. Therefore, it is recommended to use the Signatory API, Custodian API and Auditor API for most use cases.
{% endhint %}
