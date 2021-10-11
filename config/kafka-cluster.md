---
description: Connect kPow to Apache Kafka®
---

# Kafka Cluster

{% hint style="info" %}
Set the **ENVIRONMENT_NAME **variable to provide a UI friendly name for your Kafka cluster.
{% endhint %}

## Requirements

kPow requires **at least one configured Kafka cluster** to operate.

When configuring [**Multi-Cluster**](multi-cluster.md)** **installations the first cluster configured is your **Primary Cluster** and contains all the snapshot, metrics, and audit metadata for the installation.

Each configured Kafka cluster can have **one **associated Schema registry and/or Kafka connect cluster.

## Compatibility

kPow is compatible with **Apache Kafka 1.0+.**

kPow has been tested and is compatible with [Apache Kafka](https://kafka.apache.org), [Amazon MSK](https://aws.amazon.com/msk/), [Red Had AMQ Streams](https://www.redhat.com/en/resources/amq-streams-datasheet), [Aiven Managed Kafka](https://aiven.io/kafka), [Instaclustr Managed Kafka](https://www.instaclustr.com/products/managed-apache-kafka/), [Confluent Platform](https://www.confluent.io/product/confluent-platform) and [Confluent Cloud](https://www.confluent.io/confluent-cloud)**\*, **[Azure Event Hubs\*](https://azure.microsoft.com/en-us/services/event-hubs/), [Redpanda\*](https://vectorized.io/redpanda).

**\***Some disk related metrics and telemetry are not available when using kPow with Confluent Cloud, Azure Event Hubs or Redpanda.

## FIPS

kPow is capable of integrating with FIPS compliant Kafka clusters.

Contact [support@operatr.io](mailto:support@operatr.io) for assistance.

## Access Control

User permissions to Kafka cluster resources are defined by [**Cluster actions.**](../authorization/overview.md#user-actions)****

## **AWS IAM Integration**

kPow supports [IAM Access Control for AWS MSK](https://docs.aws.amazon.com/msk/latest/developerguide/iam-access-control.html).

Simply set your kPow connection fields appropriately, e.g.

```
SSL_TRUSTSTORE_LOCATION=<PATH_TO_TRUST_STORE_FILE>
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=AWS_MSK_IAM
SASL_JAAS_CONFIG=software.amazon.msk.auth.iam.IAMLoginModule required;
SASL_CLIENT_CALLBACK_HANDLER_CLASS=software.amazon.msk.auth.iam.IAMClientCallbackHandler
```

See the AWS documentation for more information, including JAAS config for named profiles.

## Configuration

kPow connects to a Kafka cluster with **exactly the same configuration** as a Kafka consumer or producer.

This configuration may be familiar to you, and is provided to kPow by **environment variables.**

The list of connection variables follows, many are optional. Consult the [**Kafka client docs**](https://kafka.apache.org/documentation/#adminclientconfigs) for more info.

| **Variable**                              | Description                                                                                                                                                                                                                                          |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ENVIRONMENT_NAME**                      | Optional, UI friendly label for this cluster and resources                                                                                                                                                                                           |
| **CLUSTER_ID**                            | Optional, unique identifier for the cluster. Required when connecting to [Azure Event Hubs](azure-event-hubs.md) or [Redpanda](redpanda.md).                                                                                                         |
| **BOOTSTRAP**                             | The Kafka cluster bootstrap URL                                                                                                                                                                                                                      |
| **AZURE_EVENT_HUBS**                      | Optional, set to `true` if you are connecting to an [Azure Event Hubs](azure-event-hubs.md) cluster                                                                                                                                                  |
| **SECURITY_PROTOCOL**                     | PLAINTEXT, SSL, SASL_PLAINTEXT, or SASL_SSL                                                                                                                                                                                                          |
| **SASL_MECHANISM**                        | GSSAPI, AUTHBEARER, SCRAM, PLAIN,                                                                                                                                                                                                                    |
| **SASL_JAAS_CONFIG**                      | Java Authentication and Authorization Service config                                                                                                                                                                                                 |
| **SSL_KEYSTORE_LOCATION**                 | The path to a keystore for auth with certificates                                                                                                                                                                                                    |
| **SSL_KEYSTORE_PASSWORD**                 | The password to access the auth keystore                                                                                                                                                                                                             |
| **SSL_KEY_PASSWORD**                      | The password of the key within the keystore                                                                                                                                                                                                          |
| **SSL_KEYSTORE_TYPE**                     | The file format of the keystore file                                                                                                                                                                                                                 |
| **SSL_KEYMANAGER_ALGORITHM**              | The key manager algorithm used for SSL                                                                                                                                                                                                               |
| **SSL_TRUSTSTORE_LOCATION**               | The path to a truststore for auth with certificates                                                                                                                                                                                                  |
| **SSL_TRUSTSTORE_PASSWORD**               | The password to access the auth truststore                                                                                                                                                                                                           |
| **SSL_TRUSTSTORE_TYPE**                   | The file format of the truststore file                                                                                                                                                                                                               |
| **SSL_TRUSTMANAGER_ALGORITHM**            | The trust manager algorithm user for SSL                                                                                                                                                                                                             |
| **SSL_ENDPOINT_IDENTIFICATION_ALGORITHM** | Often required when authenticating via SSL                                                                                                                                                                                                           |
| **SSL_PROVIDER**                          | Name of the security provider used for SSL                                                                                                                                                                                                           |
| **SSL_CIPHER_SUITES**                     | A list of cipher suites                                                                                                                                                                                                                              |
| **SSL_PROTOCOL**                          | TLS, TLSv1.1, or TLSv1.2                                                                                                                                                                                                                             |
| **SSL_ENABLED_PROTOCOLS**                 | The list of protocols enabled for SSL                                                                                                                                                                                                                |
| **SSL_KEYSTORE_KEY**                      | <p><strong></strong></p><p>Private key in the format specified by <code>SSL_KEYSTORE_TYPE</code>. See: <a href="https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key">KIP-651</a></p> |
| **SSL_KEYSTORE_CERTIFICATE_CHAIN**        | Certificate chain in the format specified by `SSL_KEYSTORE_TYPE`. See: [KIP-651](https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key)                                                |
| **SSL_TRUSTSTORE_CERTIFICATES**           | Trusted certificates in the format specified by `SSL_KEYSTORE_TYPE`. See: [KIP-651](https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key)                                             |
