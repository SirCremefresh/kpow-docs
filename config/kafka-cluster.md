---
description: Connect kPow to Apache Kafka®
---

# Kafka Cluster

{% hint style="info" %}
The **ENVIRONMENT\_NAME **variable provides a UI friendly name for your Kafka cluster.
{% endhint %}

## Requirements

kPow requires **at least one configured Kafka cluster** to operate.

When configuring [**Multi-Cluster**](multi-cluster.md)** **installations the first cluster configured is your **Primary Cluster** and contains all the snapshot, metrics, and audit metadata for the installation.

A Kafka cluster can have **multiple **associated Schema registries and/or Kafka connect clusters.

## Compatibility

kPow is compatible with **Apache Kafka 1.0+.**

kPow has been tested and is compatible with [Apache Kafka](https://kafka.apache.org), [Amazon MSK](https://aws.amazon.com/msk/), [Red Had AMQ Streams](https://www.redhat.com/en/resources/amq-streams-datasheet), [Red Hat OpenShift Streams for Apache Kafka](https://developers.redhat.com/products/red-hat-openshift-streams-for-apache-kafka/overview), [Aiven Managed Kafka](https://aiven.io/kafka), [Instaclustr Managed Kafka](https://www.instaclustr.com/products/managed-apache-kafka/), [Confluent Platform](https://www.confluent.io/product/confluent-platform), and [Confluent Cloud](https://www.confluent.io/confluent-cloud).

kPow has been confirmed to work with Azure Event Hubs\* and Redpanda, though these platforms are not officially supported and all kPow features may not be available.

**\***Some disk related metrics and telemetry are not available when using kPow Azure Event Hubs.

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

kPow connects to a Kafka with **the same configuration** as a Kafka consumer or producer.

This configuration may be familiar to you, and is provided to kPow by **environment variables.**

The list of connection variables follows, many are optional. See the [**Kafka client docs**](https://kafka.apache.org/documentation/#adminclientconfigs) for more.

Need to create a Keystore from certificate files? This [Stackoverflow answer](https://stackoverflow.com/questions/906402/how-to-import-an-existing-x-509-certificate-and-private-key-in-java-keystore-to/8224863#8224863) might help.

| **Variable**                                 | Description                                                                                                                                                                                                                                          |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ENVIRONMENT\_NAME**                        | Optional, UI friendly label for this cluster and resources                                                                                                                                                                                           |
| **CLUSTER\_ID**                              | Optional, unique identifier for the cluster. Required when connecting to [Azure Event Hubs](azure-event-hubs.md) or [Redpanda](redpanda.md).                                                                                                         |
| **BOOTSTRAP**                                | The Kafka cluster bootstrap URL                                                                                                                                                                                                                      |
| **KAFKA\_VARIANT**                           | 'EVENT\_HUBS' for Azure Event Hubs or 'RHOSAK' for Red Had OpenShift Streams for Apache Kafka, otherwise do not set.                                                                                                                                 |
| **SECURITY\_PROTOCOL**                       | PLAINTEXT, SSL, SASL\_PLAINTEXT, or SASL\_SSL                                                                                                                                                                                                        |
| **SASL\_MECHANISM**                          | GSSAPI, AUTHBEARER, SCRAM, PLAIN,                                                                                                                                                                                                                    |
| **SASL\_JAAS\_CONFIG**                       | Java Authentication and Authorization Service config                                                                                                                                                                                                 |
| **SSL\_KEYSTORE\_LOCATION**                  | The path to a keystore for auth with certificates                                                                                                                                                                                                    |
| **SSL\_KEYSTORE\_PASSWORD**                  | The password to access the auth keystore                                                                                                                                                                                                             |
| **SSL\_KEY\_PASSWORD**                       | The password of the key within the keystore                                                                                                                                                                                                          |
| **SSL\_KEYSTORE\_TYPE**                      | The file format of the keystore file                                                                                                                                                                                                                 |
| **SSL\_KEYMANAGER\_ALGORITHM**               | The key manager algorithm used for SSL                                                                                                                                                                                                               |
| **SSL\_TRUSTSTORE\_LOCATION**                | The path to a truststore for auth with certificates                                                                                                                                                                                                  |
| **SSL\_TRUSTSTORE\_PASSWORD**                | The password to access the auth truststore                                                                                                                                                                                                           |
| **SSL\_TRUSTSTORE\_TYPE**                    | The file format of the truststore file                                                                                                                                                                                                               |
| **SSL\_TRUSTMANAGER\_ALGORITHM**             | The trust manager algorithm user for SSL                                                                                                                                                                                                             |
| **SSL\_ENDPOINT\_IDENTIFICATION\_ALGORITHM** | Often required when authenticating via SSL                                                                                                                                                                                                           |
| **SSL\_PROVIDER**                            | Name of the security provider used for SSL                                                                                                                                                                                                           |
| **SSL\_CIPHER\_SUITES**                      | A list of cipher suites                                                                                                                                                                                                                              |
| **SSL\_PROTOCOL**                            | TLS, TLSv1.1, or TLSv1.2                                                                                                                                                                                                                             |
| **SSL\_ENABLED\_PROTOCOLS**                  | The list of protocols enabled for SSL                                                                                                                                                                                                                |
| **SSL\_KEYSTORE\_KEY**                       | <p><strong></strong></p><p>Private key in the format specified by <code>SSL_KEYSTORE_TYPE</code>. See: <a href="https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key">KIP-651</a></p> |
| **SSL\_KEYSTORE\_CERTIFICATE\_CHAIN**        | Certificate chain in the format specified by `SSL_KEYSTORE_TYPE`. See: [KIP-651](https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key)                                                |
| **SSL\_TRUSTSTORE\_CERTIFICATES**            | Trusted certificates in the format specified by `SSL_KEYSTORE_TYPE`. See: [KIP-651](https://cwiki.apache.org/confluence/display/KAFKA/KIP-651+-+Support+PEM+format+for+SSL+certificates+and+private+key)                                             |
