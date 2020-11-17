---
description: Authenticate Users with Jetty JAAS JDBCLoginModule
---

# JDBCLoginModule

Configure kPow to read authentication and role information from a database via JDBC.

{% hint style="info" %}
**In Depth:** For specifics on JAAS / JSBC configuration see the [**Jetty JDBCLoginModule**](https://www.eclipse.org/jetty/documentation/current/jaas-support.html#jetty-jaas) ****docs.
{% endhint %}

## Form or Basic Authentication?

kPow supports both form-based and basic authentication.

**Form authentication is the default.** To basic authentication, set the environment variable:

```text
JETTY_AUTH_METHOD=basic
```

## Configuration

To enable LdapLoginModule authentication you must:

* Create a JAAS configuration file
* Set the **`AUTH_PROVIDER_TYPE=jetty`** environment variable.
* Start the JAR or Docker container with `-Djava.security.auth.login.config=/path/to/jaas.conf`

### JAAS Configuration

Create a JAAS JDBC configuration file \(the **kpow** realm is very important\).

```text
kpow {
      org.eclipse.jetty.jaas.spi.JDBCLoginModule required
      dbUrl="jdbc:hsqldb:."
      dbUserName="sa"
      dbDriver="org.hsqldb.jdbcDriver"
      userTable="myusers"
      userField="myuser"
      credentialField="mypassword"
      userRoleTable="myuserroles"
      userRoleUserField="myuser"
      userRoleRoleField="myrole";
      };
```

### Environment Configuration

To activate Jetty JAAS authentication set the environment variable **`AUTH_PROVIDER_TYPE=jetty`**

### JAR Startup

Specify the JAAS config file by setting the following system property when starting the JAR:

  `-Djava.security.auth.login.config=/path/to/jaas.conf` 

{% hint style="warning" %}
**Note:** System properties must come after **java** but before **-jar**.
{% endhint %}

```bash
AUTH_PROVIDER_TYPE=jetty \
<... more env vars ...> \
java -Djava.security.auth.login.config=/opt/kpow/jaas.conf -jar /opt/kpow/latest.jar 
```

### Docker Container Startup

{% hint style="info" %}
**Note:** The JVM provides an environment variable called `JAVA_TOOL_OPTIONS` that can be used in place of system properties. We use this the thread the JAAS config to Docker.
{% endhint %}

Set the env var `JAVA_TOOL_OPTIONS=-Djava.security.auth.login.config=/path/to/jaas.conf`

When starting the docker container you will see logging output similar to:

```bash
Picked up JAVA_TOOL_OPTIONS: -Djava.security.auth.login.config=/path/to/jaas.conf
```

## User Experience

When configured your users will be prompted to authenticate on each new browser session.

![](../.gitbook/assets/screen-login.png)

