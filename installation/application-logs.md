---
description: Configure kPow Application Logs
---

# Application Logs

kPow uses [**Logback**](http://logback.qos.ch/) to record application logs to **stdout**.

Configure kPow to write application logs to disk \(or any other supported Logback appender\) and control the log levels by providing a Logback configuration file.

{% hint style="info" %}
**Note:** Kafka logging is verbose, we recommend tuning it to ERROR logs only.
{% endhint %}

This example **turns on Jetty JAAS debug logging** and writes logs to a file called kpow-log.txt:

```markup
<configuration>
    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>kpow-log.txt</file>
        <append>true</append>
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} %-5level [%thread] %logger{36} – %m%n</pattern>
        </encoder>
    </appender>
    
    <logger name="kafka" level="ERROR"/>
    <logger name="org.apache.kafka" level="ERROR"/>
    <logger name="org.eclipse.jetty.jaas.spi" level="DEBUG"/> 
    <logger name="org.eclipse.jetty.security.authentication" level="DEBUG"/>
 
   <root level="INFO">
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```

Provide your custom Logback configuration to kPow as a Java system variable:

```bash
java -Dlogback.configurationFile=/kpow/custom-logback.xml -jar /kpow/kpow-latest.jar
```

The kPow Docker Container can be configured with the `JAVA_TOOL_OPTIONS` environment variable:

```bash
JAVA_TOOL_OPTIONS=-Dlogback.configurationFile=/kpow/custom-logback.xml
```

In this specific example we turn on debug logging for Jetty JAAS authentication methods \(LDAP, etc.\). 

To put JAAS into debug mode also requires **debug="true"** in your JAAS config file:

```text
kpow {
         org.eclipse.jetty.jaas.spi.PropertyFileLoginModule required
         debug="true"
         file="dev-resources/jaas/hash-realm.properties";
     };
```

Once configured, application logs are written to file and JAAS debug output is visible:

```text
09:26:32.135 INFO  [oprtr.compute.snapshots.v2-44318b10-b719-46db-96ea-f97495cdce8f-StreamThread-2] operatr.compute-v2 – oprtr.compute.snapshots.v2: streams state changed from REBALANCING to RUNNING
09:26:32.287 INFO  [oprtr.compute.metrics.v2-6126ee6c-0253-4a5d-8d66-cbd3b0a4b0bb-StreamThread-2] operatr.compute-v2 – oprtr.compute.metrics.v2: streams state changed from REBALANCING to RUNNING
09:26:39.349 INFO  [OperatrScheduler_Worker-1] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [9] configuration captured in 204 ms
09:26:39.605 INFO  [OperatrScheduler_Worker-1] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [9] configuration captured in 256 ms
09:26:41.409 DEBUG [qtp1357054363-56] o.e.j.j.spi.PropertyFileLoginModule – setupPropertyUserStore: Starting new PropertyUserStore. PropertiesFile: dev-resources/jaas/hash-realm.properties refreshInterval: 0
09:26:41.416 DEBUG [qtp1357054363-56] o.e.j.j.spi.PropertyFileLoginModule – Checking PropertyUserStore dev-resources/jaas/hash-realm.properties for admin
09:26:41.417 DEBUG [qtp1357054363-56] o.e.j.j.spi.PropertyFileLoginModule – Found: admin in PropertyUserStore dev-resources/jaas/hash-realm.properties
09:26:41.429 INFO  [qtp1357054363-58] operatr.auth.jetty – login -> user: admin, roles: #{"content-administrators" "kafka-admins" "server-administrators"}
09:27:05.449 INFO  [OperatrScheduler_Worker-3] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [38] kafka telemetry snapshots captured in 440 ms
09:28:05.250 INFO  [OperatrScheduler_Worker-7] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [38] kafka telemetry snapshots captured in 243 ms
09:29:05.350 INFO  [OperatrScheduler_Worker-1] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [38] kafka telemetry snapshots captured in 343 ms
09:30:05.257 INFO  [OperatrScheduler_Worker-5] operatr.observe.kafka – R9AvkXfHTsCiI8g3E_5EVA: [38] kafka telemetry snapshots captured in 250 ms
```

See the [Logback](http://logback.qos.ch/) site for full information on configuration options like rolling file appenders.

