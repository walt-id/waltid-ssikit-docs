# VC Library

The **Vc Lib** is a typesafe implementation of W3C Verifiable Credentials in order to facilitate interoperability among various applications.&#x20;

The code-base as well as instructions how to use the library can be found at GitHub at: [https://github.com/walt-id/waltid-ssikit-vclib/](https://github.com/walt-id/waltid-ssikit-vclib/)

The library can be used independently as dependency for JVM-based applications. Furthermore, the Vc Lib is rolled out as part of the SSI Kit and determines which credential templates can be used in the Signatory (component for issuing credentials).&#x20;

The following command prints all credential templates which are currently maintained in the VC Lib and can be utilized in the SSI Kit.

`docker run -itv $(pwd)/data:/app/data waltid/ssikit:latest vc templates list`

![](<../.gitbook/assets/image (4) (1).png>)

