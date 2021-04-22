---
description: Connect kPow to Apache Kafka®
---

# Kafka Cluster

{% hint style="info" %}
Set the **ENVIRONMENT\_NAME** variable to provide a UI friendly name for your Kafka cluster.
{% endhint %}

## Requirements

kPow requires **at least one configured Kafka cluster** to operate.

When configuring [**Multi-Cluster**](multi-cluster.md) ****installations the first cluster configured is your **Primary Cluster** and contains all the snapshot, metrics, and audit metadata for the installation.

Each configured Kafka cluster can have **one** associated Schema registry and/or Kafka connect cluster.

## Compatibility

kPow is compatible with **Apache Kafka 1.0+.**

kPow has been tested and is compatible with [Apache Kafka](https://kafka.apache.org/), [Amazon MSK](https://aws.amazon.com/msk/), [Red Had AMQ Streams](https://www.redhat.com/en/resources/amq-streams-datasheet), [Aiven Managed Kafka](https://aiven.io/kafka), [Instaclustr Managed Kafka](https://www.instaclustr.com/products/managed-apache-kafka/), [Confluent Platform](https://www.confluent.io/product/confluent-platform) and [Confluent Cloud](https://www.confluent.io/confluent-cloud)**\*,** [Azure Event Hubs\*](https://azure.microsoft.com/en-us/services/event-hubs/), [Redpanda\*](https://vectorized.io/redpanda).

**\***Some disk related metrics and telemetry are not available when using kPow with Confluent Cloud, Azure Event Hubs or Redpanda.

## FIPS

kPow is capable of integrating with FIPS compliant Kafka clusters.

Contact [support@operatr.io](mailto:support@operatr.io) for assistance.

## Access Control

User permissions to Kafka cluster resources are defined by [**Cluster actions.**](../authorization/overview.md#user-actions)\*\*\*\*

## Configuration

kPow connects to a Kafka cluster with **exactly the same configuration** as a Kafka consumer or producer.

This configuration may be familiar to you, and is provided to kPow by **environment variables.**

The list of connection variables follows, many are optional. Consult the **Kafka client docs** for more info.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Variable</b>
      </th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>ENVIRONMENT_NAME</b>
      </td>
      <td style="text-align:left">Optional, UI friendly label for this cluster and resources</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CLUSTER_ID</b>
      </td>
      <td style="text-align:left">Optional, unique identifier for the cluster. Required when connecting
        to <a href="azure-event-hubs.md">Azure Event Hubs</a> or <a href="redpanda.md">Redpanda</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>BOOTSTRAP</b>
      </td>
      <td style="text-align:left">The Kafka cluster bootstrap URL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>REDPANDA</b>
      </td>
      <td style="text-align:left">Optional, set to <code>true</code> if you are connecting to a <a href="redpanda.md">Redpanda</a> cluster.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>AZURE_EVENT_HUBS</b>
      </td>
      <td style="text-align:left">Optional, set to <code>true</code> if you are connecting to an <a href="azure-event-hubs.md">Azure Event Hubs</a> cluster</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SECURITY_PROTOCOL</b>
      </td>
      <td style="text-align:left">PLAINTEXT, SSL, SASL_PLAINTEXT, or SASL_SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SASL_MECHANISM</b>
      </td>
      <td style="text-align:left">GSSAPI, AUTHBEARER, SCRAM, PLAIN,</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SASL_JAAS_CONFIG</b>
      </td>
      <td style="text-align:left">Java Authentication and Authorization Service config</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYSTORE_LOCATION</b>
      </td>
      <td style="text-align:left">The path to a keystore for auth with certificates</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYSTORE_PASSWORD</b>
      </td>
      <td style="text-align:left">The password to access the auth keystore</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEY_PASSWORD</b>
      </td>
      <td style="text-align:left">The password of the key within the keystore</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYSTORE_TYPE</b>
      </td>
      <td style="text-align:left">The file format of the keystore file</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYMANAGER_ALGORITHM</b>
      </td>
      <td style="text-align:left">The key manager algorithm used for SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_TRUSTSTORE_LOCATION</b>
      </td>
      <td style="text-align:left">The path to a truststore for auth with certificates</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_TRUSTSTORE_PASSWORD</b>
      </td>
      <td style="text-align:left">The password to access the auth truststore</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_TRUSTSTORE_TYPE</b>
      </td>
      <td style="text-align:left">The file format of the truststore file</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_TRUSTMANAGER_ALGORITHM</b>
      </td>
      <td style="text-align:left">The trust manager algorithm user for SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_ENDPOINT_IDENTIFICATION_ALGORITHM</b>
      </td>
      <td style="text-align:left">Often required when authenticating via SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_PROVIDER</b>
      </td>
      <td style="text-align:left">Name of the security provider used for SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_CIPHER_SUITES</b>
      </td>
      <td style="text-align:left">A list of cipher suites</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_PROTOCOL</b>
      </td>
      <td style="text-align:left">TLS, TLSv1.1, or TLSv1.2</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_ENABLED_PROTOCOLS</b>
      </td>
      <td style="text-align:left">The list of protocols enabled for SSL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYSTORE_KEY</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>Private key in the format specified by <code>SSL_KEYSTORE_TYPE</code>.
          See: <a href="https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key">KIP-651</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_KEYSTORE_CERTIFICATE_CHAIN</b>
      </td>
      <td style="text-align:left">Certificate chain in the format specified by <code>SSL_KEYSTORE_TYPE</code>.
        See: <a href="https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key">KIP-651</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL_TRUSTSTORE_CERTIFICATES</b>
      </td>
      <td style="text-align:left">Trusted certificates in the format specified by <code>SSL_KEYSTORE_TYPE</code>.
        See: <a href="https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key">KIP-651</a>
      </td>
    </tr>
  </tbody>
</table>

