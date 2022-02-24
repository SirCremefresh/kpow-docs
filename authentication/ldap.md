---
description: Authenticate Users with Jetty JAAS LdapLoginModule
---

# LdapLoginModule

Configure kPow to read authentication and role information from LDAP.

{% hint style="info" %}
For specifics on JAAS / LDAP configuration see the [Jetty LdapLoginModule](https://www.eclipse.org/jetty/documentation/jetty-10/operations-guide/index.html#og-ldaploginmodule) **** docs.
{% endhint %}

## Form or Basic Authentication?

{% hint style="info" %}
Form-based authentication is the default login mechanism for Kpow.
{% endhint %}

kPow supports both form-based and basic authentication. To use basic authentication, set:

```
JETTY_AUTH_METHOD=basic
```

## Configuration

To enable LdapLoginModule authentication you must:

* Create a JAAS configuration file
* Set the **`AUTH_PROVIDER_TYPE=jetty` ** environment variable.
* Start the JAR or Docker container with `-Djava.security.auth.login.config=/path/to/jaas.conf`

### JAAS Configuration

Create a JAAS LDAP configuration file (the **kpow** realm is very important).

{% hint style="info" %}
See the [Kpow Secure Configuration Guide](https://github.com/operatr-io/kpow/tree/main/secure-config) for details of **bindPassword encryption**.
{% endhint %}

```
## Your configuration will vary depending on your LDAP setup

kpow {
  io.kpow.jaas.spi.LdapLoginModule required
  useLdaps="false"
  debug="true"
  contextFactory="com.sun.jndi.ldap.LdapCtxFactory"
  hostname="localhost"
  port="10389"
  bindDn="uid=admin,ou=system"
  bindPassword="AES:ARAOyh4tygxSknnTNknnuFXG+PYr0oLlN9UO/0XSq4RSOw=="
  authenticationMethod="simple"
  forceBindingLogin="true"
  userBaseDn="OU=Users,DC=example,DC=com"
  userRdnAttribute="uid"
  userIdAttribute="uid"
  userPasswordAttribute="userPassword"
  roleBaseDn="OU=Groups,DC=example,DC=com"
  roleNameAttribute="roleName"
  roleMemberAttribute="uniqueMember"
  roleObjectClass="groupOfUniqueNames";
};
```

### JAAS Debugging

To debug JAAS LDAP connections, first add `debug="true"` to your config:

```
kpow {
  io.kpow.jaas.spi.LdapLoginModule required
  debug="true"
  ...
  ...
```

Then turn on Jetty JAAS debug-level logging, see [Application Logs](../installation/application-logs.md) for example configuration.

Finally to (optionally) debug LDAP connection errors, enable Jetty IGNORE level logs by starting kPow with the following Java system variable:

```
-Dorg.eclipse.jetty.util.log.IGNORED=true
```

Once configured you will find debug log lines in your application logs that provide insight into how the LdapLoginModule is operating.

### Environment Configuration

To activate Jetty JAAS authentication set the environment variable `AUTH_PROVIDER_TYPE=jetty`

### JAR Startup

Specify the JAAS config file by setting the following system property when starting the JAR:

&#x20; `-Djava.security.auth.login.config=/path/to/jaas.conf`&#x20;

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

Set the environment variable:

&#x20;`JAVA_TOOL_OPTIONS=-Djava.security.auth.login.config=/path/to/jaas.conf`

{% hint style="info" %}
**Note:** When your JAAS config is on the **host** machine and not within the container you will need to configure a docker volume mount so that kPow can read that configuration:

**`docker run --volume="/config/path:/config/path/" -p 3000:3000 --env-file ...`**
{% endhint %}

When starting the docker container you will see logging output similar to:

```bash
Picked up JAVA_TOOL_OPTIONS: -Djava.security.auth.login.config=/path/to/jaas.conf
```

## User Experience

When configured your users will be prompted to authenticate on each new browser session.

![](../.gitbook/assets/screen-login.png)
