# Dependency (JVM)

The SS Kit can also be used as direct dependency for JVM-based applications. In this case an existing application can easily be enhanced with SSI functionality.

The following illustrates how the SS Kit can be used via Gradle or Maven (look for the current version on GitHub [https://github.com/walt-id/waltid-ssikit](https://github.com/walt-id/waltid-ssikit))

**Gradle**

```
implementation("id.walt:waltid-ssi-kit:VERSION")
```

**Maven**

```
  <dependency>
        <groupId>id.walt</groupId>
        <artifactId>waltid-ssi-kit</artifactId>
        <version>VERSION</version>
   </dependency>
```

Required Maven repos:

```
https://maven.walt.id/repository/waltid/
https://maven.walt.id/repository/waltid-ssi-kit/
```
