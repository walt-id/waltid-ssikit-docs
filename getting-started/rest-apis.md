# REST APIs

This sections outlines the APIs of the SSI Kit:

* Core API&#x20;
* Signatory API
* Custodian API
* Auditor API
* ESSIF Connector API

In order to review the Swagger doc of each API, run the **serve** command of the CLI tool and navigate to the corresponding web pages:

```
    ./ssikit.sh serve
```

or with Docker:

```
    docker run -itv $(pwd)/data:/app/data -p 7000-7004:7000-7004 waltid/ssikit -v serve -b 0.0.0.0
```

* Core API: http://127.0.0.1:7000
* Signatory API: http://127.0.0.1:7001
* Custodian API: http://127.0.0.1:7002
* Auditor API: http://127.0.0.1:7003
* ESSIF API: http://127.0.0.1:7004
