---
noIndex: true
---

# Dependency (JVM)

The SSI Kit can also be used as direct dependency for JVM-based applications. In this case an existing application can easily be enhanced with SSI functionality.

### Dependency

The following illustrates how the SSI Kit can be used via Gradle or Maven (look for the current version on GitHub [https://github.com/walt-id/waltid-ssikit](https://github.com/walt-id/waltid-ssikit))

**Gradle**

```
implementation("id.walt:waltid-ssikit:VERSION")
```

**Maven**

```
  <dependency>
        <groupId>id.walt</groupId>
        <artifactId>waltid-ssikit</artifactId>
        <version>VERSION</version>
   </dependency>
```

Required Maven repos:

```
https://maven.walt.id/repository/waltid/
https://maven.walt.id/repository/waltid-ssi-kit/
```

{% hint style="info" %}
You can find the latest version [here](https://github.com/walt-id/waltid-ssikit/releases). Make sure when adding the version you add it without the 'v' in front.
{% endhint %}

### Examples

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td>Examples on how to issue and verify Verifiable Credentials in a Java project.</td><td></td><td><a href="https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/java/id/walt/ssikitexamples">https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/java/id/walt/ssikitexamples</a></td></tr><tr><td><strong>Kotlin</strong></td><td>Examples on how to issue and verify Verifiable Credentials in a Kotlin project.</td><td></td><td><a href="https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/kotlin/id/walt/ssikitexamples">https://github.com/walt-id/waltid-ssikit-examples/tree/master/src/main/kotlin/id/walt/ssikitexamples</a></td></tr></tbody></table>
