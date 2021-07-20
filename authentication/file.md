---
description: Authenticate Users with Jetty JAAS PropertyFileLoginModule
---

# PropertyFileLoginModule

Configure kPow to read authentication and role information from a property file.

Use the exact configuration in this guide to restrict access to the following user/password/roles:

* admin/admin/kafka-admins
* jetty/jetty/kafka-users
* other/other/kafka-admins+kafka-users
* plain/plain/content-administrators
* user/password/kafka-users

{% hint style="info" %}
**See:** [**Jetty PropertyFileLoginModule**](https://www.eclipse.org/jetty/documentation/jetty-10/operations-guide/index.html#og-propertyfileloginmodule) ****guide to update user and password configuration.
{% endhint %}

## Configuration

To enable PropertyFileLoginModule authentication:

* Create a JAAS configuration file
* Create a users property file
* Set the **`AUTH_PROVIDER_TYPE=jetty`** environment variable.
* Start the JAR or Docker container with `-Djava.security.auth.login.config=/path/to/jaas.conf`

### JAAS Configuration

Create a JAAS PropertyFile configuration file \(the **kpow** realm is very important\).

```text
kpow {
        org.eclipse.jetty.jaas.spi.PropertyFileLoginModule required
        file="/opt/kpow/user.props";
      };
```

Create a users property file **at the path configured in your JAAS config**.

```text
# This file defines users passwords and roles for a HashUserRealm
#
# The format is
#  <username>: <password>[,<rolename> ...]
#
# Passwords may be clear text, obfuscated or checksummed.  The class
# org.eclipse.jetty.util.security.Password should be used to generate obfuscated
# passwords or password checksums
#
# If DIGEST Authentication is used, the password must be in a recoverable
# format, either plain text or OBF:.
#
# Credentials are jetty/jetty, admin/admin, other/other, plain/plain,
#                 user/password, and digest/digest
#
jetty: MD5:164c88b302622e17050af52c89945d44,kafka-users
admin: CRYPT:adpexzg3FUZAk,kafka-admins
other: OBF:1xmk1w261u9r1w1c1xmq,kafka-admins,kafka-users
plain: plain,content-administrators
user: password,kafka-users
# This entry is for digest auth.  The credential is a MD5 hash of
# username:realmname:password
digest: MD5:6e120743ad67abfbc385bc2bb754e297,kafka-users
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
**Note:** The JVM provides an environment variable called `JAVA_TOOL_OPTIONS` that can be used in place of system properties. We use this to thread the JAAS config to Docker.
{% endhint %}

Set the env var `JAVA_TOOL_OPTIONS=-Djava.security.auth.login.config=/path/to/jaas.conf`

{% hint style="info" %}
**Note:** When your JAAS config is on the **host** machine and not within the container you will need to configure a docker volume mount so that kPow can read that configuration:

**`docker run --volume="/config/path:/config/path/" -p 3000:3000 --env-file ...`**
{% endhint %}

When starting the docker container you will see logging output similar to:

```bash
Picked up JAVA_TOOL_OPTIONS: -Djava.security.auth.login.config=/path/to/jaas.conf
```

## Form or Basic Authentication?

kPow supports both form-based and basic authentication.

**Form authentication is the default.** To basic authentication, set the environment variable:

```text
JETTY_AUTH_METHOD=basic
```

## User Experience

When configured your users will be prompted to authenticate on each new browser session.

![](../.gitbook/assets/screen-login.png)

