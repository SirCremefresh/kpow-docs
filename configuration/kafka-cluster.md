---
description: Connect kPow to Apache Kafka®
---

# Kafka Cluster

## Requirements

kPow requires **at least on Kafka cluster** to operate.

When configuring **Multi-Cluster** installations the first cluster configured is your **Primary Cluster** and contains all the snapshot, metrics, and audit metadata for the installation.

## Compatibility

kPow is compatible with **Apache Kafka 1.0+.**

kPow has been tested and is compatible with [Apache Kafka](https://kafka.apache.org/), [Red Had AMQ Streams](https://www.redhat.com/en/resources/amq-streams-datasheet), [Aiven Managed Kafka](https://aiven.io/kafka), [Instaclustr Managed Kafka](https://www.instaclustr.com/products/managed-apache-kafka/), [Confluent Platform](https://www.confluent.io/product/confluent-platform) and [Confluent Cloud](https://www.confluent.io/confluent-cloud)**\***.

**\***Some disk related metrics and telemetry are not available when using kPow with Confluent Cloud.

## Configuration

kPow connects to a Kafka cluster with **exactly the same configuration** as a Kafka consumer or producer.

This configuration may be familiar to you, and is provided to kPow by **environment variables.**

The list of connection variables follows, many are optional. Consult the **Kafka client docs** for more info.

| **Variable** | Description |
| :--- | :--- |
| **BOOTSTRAP** | The Kafka cluster bootstrap URL |
| **SECURITY\_PROTOCOL** | PLAINTEXT, SSL, SASL\_PLAINTEXT, or SASL\_SSL |
| **SASL\_MECHANISM** | GSSAPI, AUTHBEARER, SCRAM, PLAIN, |
| **SASL\_JAAS\_CONFIG** | Java Authentication and Authorization Service config |
| **SSL\_KEYSTORE\_LOCATION** | The path to a keystore for auth with certificates |
| **SSL\_KEYSTORE\_PASSWORD** | The password to access the auth keystore |
| **SSL\_KEY\_PASSWORD** | The password of the key within the keystore |
| **SSL\_KEYSTORE\_TYPE** | The file format of the keystore file |
| **SSL\_KEYMANAGER\_ALGORITHM** | The key manager algorithm used for SSL  |
| **SSL\_TRUSTSTORE\_LOCATION** | The path to a truststore for auth with certificates |
| **SSL\_TRUSTSTORE\_PASSWORD** | The password to access the auth truststore |
| **SSL\_TRUSTSTORE\_TYPE** | The file format of the truststore file |
| **SSL\_TRUSTMANAGER\_ALGORITHM** | The trust manager algorithm user for SSL |
| **SSL\_ENDPOINT\_IDENTIFICATION\_ALGORITHM** | Often required when authenticating via SSL |
| **SSL\_PROVIDER** | Name of the security provider used for SSL |
| **SSL\_CIPHER\_SUITES** | A list of cipher suites |
| **SSL\_PROTOCOL** | TLS, TLSv1.1, or TLSv1.2 |
| **SSL\_ENABLED\_PROTOCOLS** | The list of protocols enabled for SSL |
