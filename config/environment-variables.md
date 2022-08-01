---
description: All the configuration options available to kPow
---

# Environment Variables

kPow is configured with these Environment Variables.

## Kafka

One instance of kPow can manage multiple Kafka Clusters and associated resources.

* See [Kafka Cluster](kafka-cluster.md) for Kafka environment variable reference
* See [Kafka Connect](kafka-connect/) for Connect environment variable reference
* See [Schema Registry](schema-registry.md) for Schema registry environment variable reference

## Web Server&#x20;

The kPow UI and Prometheus endpoints are served by [Jetty](https://www.eclipse.org/jetty/).

The server can be configured to serve the UI via HTTPS or on a different port, or to redirect correctly when fronted with an HTTPS-terminating proxy.

### LOG\_FORMAT

**Type:** String, **Default:** plain

Set to 'json' to have Kpow write application logs in JSON format.

### PORT

**Type:** Long, **Default**: 3000

The server port of the kPow UI.

### HTTP\_FORWARDED

**Type:** Boolean, **Default:** false

{% hint style="info" %}
See [Jetty HTTP\_FORWARDED module](https://www.eclipse.org/jetty/documentation/jetty-10/operations-guide/index.html#og-module-http-forwarded) for more information.
{% endhint %}

Configure when running kPow with Jetty Authentication and behind a reverse-proxy that is performing HTTP termination. When **true** the Jetty Authentication process will respect the HTTPS scheme when redirecting post-authentication.

### ENABLE\_HTTPS

**Type:** Boolean, **Default:** false

{% hint style="info" %}
See [HTTPS Connections](../features/https-connections.md) for more information.&#x20;
{% endhint %}

Serve the kPow UI via HTTPS (requires further configuration, below)

### **HTTPS\_SNI\_HOST\_CHECK**

**Type:** Boolean, **Default:** false

When SSL is configured, confirm that the certificate sent to the client matches the Host header.

### **HTTPS\_KEYSTORE\_LOCATION**

**Type:** String (e.g. /ssl/https.keystore.jks)

Path to the SSL Keystore.

### **HTTPS\_KEYSTORE\_TYPE**

**Type:** String, **Default:** JKS

Type of the SSL Keystore.

### **HTTPS\_KEYSTORE\_PASSWORD**

**Type:** String

Password of the SSL Keystore.

### **HTTPS\_TRUSTSTORE\_LOCATION**

**Type:** String (e.g. /ssl/https.truststore.jks)

Path to the SSL Truststore.

### **HTTPS\_TRUSTSTORE\_TYPE**

**Type:** String, **Default**: JKS

Type of the SSL Truststore.

### **HTTPS\_TRUSTSTORE\_PASSWORD**

**Type:** String

Password of the SSL Truststore

## Authentication

kPow supports Jetty (File, LDAP, DB, JAAS), SAML, OpenID and OAuth for authentication.

{% hint style="info" %}
See [User Authentication](../authentication/overview.md) for more details.
{% endhint %}

### AUTH\_PROVIDER\_TYPE

**Type:** Enum, **Values:** okta, github, saml, jetty, auth0

Your choice of Authentication provider, specify Jetty for LDAP, DB, File, or JAAS.

### OKTA\_ORGANISATION

**Type:** String

When using Okta authentication - the name of your Okta organisation.

### AUTH\_LANDING\_URI

**Type:** String (e.g. https://staging.operatr.z-corp.com)

The absolute URL to redirect to after successful login.

### **OPENID\_AUTH\_URI**

**Type:** String

The OpenID Auth URI, e.g.

* Github: [https://github.com/login/oauth/authorize](https://github.com/login/oauth/authorize)
* Github Enterprise: \[Server URL]/login/oauth/authorize

### OPENID\_API\_URI

**Type:** String

The OpenID API URI, e.g.

* Github: [https://api.github.com/user](https://api.github.com/user)
* Github Enterprise: \[Server URL]/api/v3/user

### OPENID\_TOKEN\_URI

**Type:** String

The OpenID Token URI, e.g.

* Github: [https://github.com/login/oauth/access\_token](https://github.com/login/oauth/access\_token)
* Github Enterprise: \[Server URL]/login/oauth/access\_token

### OPENID\_CLIENT\_ID

**Type:** String

The OpenID Client ID found in your configured OpenID App.

### OPENID\_CLIENT\_SECRET

**Type:** String

The OpenID Client Secret found in your configured OpenID App.

### **SAML\_RELYING\_PARTY\_IDENTIFIER**

**Type:** String

Your kPow Application ID

### SAML\_ACS\_URL

**Type:** String

The Assertion Consumer Service URL

### **SAML\_METADATA\_FILE**

**Type:** String (e.g. /path/to/metadata.xml)

The Metadata File from your SAML provider.

### SAML\_CERT

**Type:** String (e.g. /path/to/saml.cert)

Optional SAML Certificate

### **SAML\_SESSION\_S**

**Type:** Long, **Default:** 3600

The duration in seconds before re-authenticating SAML credentials.

### DEBUG\_SAML

**Type:** Boolean, **Default:** False

Enable SAML debug logging

### **JETTY\_AUTH\_METHOD**

**Type:** Enum, **Values:** form, basic, **Default:** form

When using Jetty Authentication, specifies to use form or basic-auth login UX

## Authorization

### **RBAC\_CONFIGURATION\_FILE**

**Type:** String (e.g. /path/to/rbac.yaml)

{% hint style="info" %}
See [Role Based Access Control](../authorization/role-based-access-control.md) for more information
{% endhint %}

The path to your RBAC configuration file (optional, requires Authentication enabled)

### Global Access Controls

{% hint style="info" %}
See [Global Access Controls](environment-variables.md#undefined) for more information
{% endhint %}

Apply global access controls like **ALLOW\_TOPIC\_CREATE**, etc.

## General

### **DATA\_POLICY\_CONFIGURATION\_FILE**

**Type:** String (e.g. /path/to/data-policies.yaml)

{% hint style="info" %}
See [Data Policies](../features/data-policies.md) for more information
{% endhint %}

The path to your kPow Data Policy Configuration.

### CUSTOM\_SERDES

**Type:** String (e.g. io.kpow.SerdeOne,io.kpow.SerdeTwo)

{% hint style="info" %}
See [Custom Serdes](../features/data-inspect/serdes.md#custom-serdes) for more information.
{% endhint %}

Comma separated names of custom Serdes that can be found on the classpath.

### DEFAULT\_HEADERS\_SERDES

**Type:** String (e.g. JSON)

The default headers Serde to use when inspecting data.

### DEFAULT\_KEY\_SERDES

**Type:** String (e.g. JSON)

The default key Serde to use when inspecting data.

### DEFAULT\_VALUE\_SERDES

**Type:** String (e.g. AVRO)

The default value Serde to use when inspecting data.

### **AVAILABLE\_KEY\_SERDES**

**Type:** String (e.g. JSON,String)

Comma separated list of key Serdes to present when inspecting data.

### **AVAILABLE\_VALUE\_SERDES**

**Type:** String (e.g. JSON,String)

Comma separated list of value Serdes to present when inspecting data.

### NUM\_PARTITIONS

**Type:** Long, **Default:** 12

The number of partitions for kPow's internal topics.

### REPLICATION\_FACTOR

**Type:** Long, **Default:** 3

The replication factor of kPow's internal topics.

### REQUEST\_TIMEOUT\_MS

**Type:** Long, **Default:** 30000

The `request.timeout.ms` setting for kPow's internal consumer groups.

### **MAX\_PRODUCE\_REQUEST\_SIZE**

**Type:** Long, **Default:** 1000000

The `max.produce.request.size` setting for kPow's internal producers

### **PROMETHEUS\_EGRESS**

**Type:** Boolean, **Default:** false

{% hint style="info" %}
See [Prometheus Integration](../features/prometheus/) for more information.
{% endhint %}

Enable Prometheus endpoints for metrics and offsets egress.

### **PROMETHEUS\_LABEL\_ENV**

**Type:** Boolean, **Default**: True

Include your ENVIRONMENT\_NAME as 'env' label on Prometheus metrics.

### SNAPSHOT\_SIMPLE\_GROUPS

**Type:** Boolean, **Default:** True

Take observations of V1 consumer groups (simple groups including Flink consumers).

### SNAPSHOT\_PARALLELISM

**Type:** Long, **Default:** 3

The level of parallelism configured for kPow telemetry capture and snapshotting.

### SNAPSHOT\_DEBUG

**Type:** Boolean, **Default:** False

Add additional logging messages to help debug snapshotting.

### LIVE\_ MODE\_ENABLED

**Type**: Boolean, **Default:** True

{% hint style="info" %}
See [Live mode](../features/live-mode.md) for more information.
{% endhint %}

Allow your users to switch to Live Mode.

### **LIVE\_MODE\_PERIOD\_MS**

**Type:** Long, **Default:** 60000

Live Mode will prompt you to continue after this period has elapsed.

### **LIVE\_MODE\_INTERVAL\_MS**

**Type:** Long, **Default:** 3500

The amount of time between Live Mode snapshots.

### **LIVE\_MODE\_MAX\_CONCURRENT\_USERS**

**Type:** Long, **Default:** 2

The maximum number of concurrent Live Mode user sessions.

### SAMPLER\_TIMEOUT\_MS

**Type:** Long, **Default:** 7000

The maximum period of a single data inspect query.

### SAMPLER\_CONSUMER\_THREADS

**Type:** Long, **Default:** 6

The level of parallelism for a data inspect query.

### **SLACK\_WEBHOOK\_URL**

**Type:** String (e.g https://slack/webhook-url)

Send Audit Log messages to Slack.

### **SLACK\_WEBHOOK\_URL\_VERBOSITY**

**Type:** Enum, **Values:** Mutations, Queries, All, **Default:** Mutations

Select the type of Audit Log messages that are sent to Slack.

### **STREAMS\_ERROR\_STRATEGY**

**Type:** Enum, **Values:** LOG\_EXCEPTION_,_ LOG_\__AND\_EXIT, **Default:** LOG EXCEPTION

The strategy to use when kPow's internal Kafka Streams instance enters an ERROR state.

### STREAMS\_TASK\_TIMEOUT\_MS

**Type:** Long, **Default:** 300000

Configures kPow's internal streams `task.timeout.ms` value. See: [KIP-572](https://cwiki.apache.org/confluence/display/KAFKA/KIP-572%3A+Improve+timeouts+and+retries+in+Kafka+Streams) for more information.
