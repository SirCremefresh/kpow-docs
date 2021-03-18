---
description: Use kPow to monitor your Confluent Cloud clusters
---

# Confluent Cloud

kPow works out of the box with Confluent Cloud, simply follow our [Kafka Cluster](kafka-cluster.md) configuration documentation to get started.

Extra configuration is required for kPow when monitoring multiple Confluent Cloud clusters that share the same bootstrap url, but have different authentication details. Read on to configure kPow in a multi-tenant scenario.

## Multi-Tenant Confluent Cloud

To connect to two clusters that share the same `BOOTSTRAP` , but are accessed with different auth credentials, provide a unique `CLUSTER_ID` environment variable for each cluster definition, for example:

```text
BOOTSTRAP=pkc-5nym1.us-east-1.aws.confluent.cloud:9092
CLUSTER_ID=confluent-cloud-dev
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=PLAIN
SASL_JAAS_CONFIG=org.apache.kafka.common.security.plain.PlainLoginModule required username="user-1" password="pass-1";
SSL_ENDPOINT_IDENTIFICATION_ALGORITHM=https

BOOTSTRAP_2=pkc-5nym1.us-east-1.aws.confluent.cloud:9092
CLUSTER_ID_2=confluent-cloud-stage
SECURITY_PROTOCOL_2=SASL_SSL
SASL_MECHANISM_2=PLAIN
SASL_JAAS_CONFIG_2=org.apache.kafka.common.security.plain.PlainLoginModule required username="user-2" password="pass-2";
SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_2=https
```

**Note**: the `CLUSTER_ID` environment variable must be unique across all clusters defined in kPow, and can be any unique identifier \(eg, the string `confluent-cloud-stage`\) 

## Limitations

The vast majority of kPow's features work with Confluent Cloud, with the exception of:

* Broker disk information/metrics - as the admin client request does not return any log details

