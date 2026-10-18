---
icon: gear-complex-api
---

# API for Developers

**dlibs-api** is the official API for the **DBans** punishment system. It allows other plugins to interact with DBans: create and revoke punishments, query player information, and listen to punishment events.

**Version:** 1.0.0\
**Repository:** [http://85.209.135.51:8081/repository/maven-releases/](http://85.209.135.51:8081/repository/maven-releases/)

***

## 🚀 Getting Started

### Maven Repository

Add the repository to your `pom.xml`:

{% tabs %}
{% tab title="pom.xml" %}
{% code lineNumbers="true" %}
```xml
<repositories>
    <repository>
        <id>demro-repo</id>
        <url>http://85.209.135.51:8081/repository/maven-releases/</url>
    </repository>
</repositories>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Add the dependency to your `pom.xml`:

{% tabs %}
{% tab title="pom.xml" %}
{% code lineNumbers="true" %}
```xml
<dependencies>
    <dependency>
        <groupId>me.demro.dlibs</groupId>
        <artifactId>dlibs-api</artifactId>
        <version>1.0.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Important:** Use `scope=provided` because the API is already bundled with DBans. Do not shade it into your plugin.
{% endhint %}

### Gradle

{% tabs %}
{% tab title="build.gradle" %}
{% code lineNumbers="true" %}
```groovy
repositories {
    maven {
        url 'http://85.209.135.51:8081/repository/maven-releases/'
        allowInsecureProtocol = true   // if using HTTP without SSL
    }
}

dependencies {
    compileOnly 'me.demro.dlibs:dlibs-api:1.0.0'
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Manual Installation (without Maven)



If you cannot use Maven, download the JAR from the repository and place it in your `libs` folder:

{% code lineNumbers="true" %}
```
http://85.209.135.51:8081/repository/maven-releases/me/demro/dlibs/dlibs-api/1.0.0/dlibs-api-1.0.0.jar
```
{% endcode %}

Then add it to your classpath or use system scope (not recommended for distribution).
