---
description: Use kPow to monitor your Confluent Cloud clusters
---

# Confluent Cloud

kPow works out of the box with Confluent Cloud, simply follow our [Kafka Cluster](kafka-cluster.md) configuration documentation to get started.

Extra configuration is required for kPow when monitoring multiple Confluent Cloud clusters that share the same bootstrap url, but have different authentication details. Read on to configure kPow in a multi-tenant scenario.

## Confluent Cloud Metrics API integration

Configure this integration to allow kPow to capture extra telemetry about your Confluent Cloud clusters:

* Broker disk information \(`io.confluent.kafka.server/retained_bytes`\)
* Active connection count \(`io.confluent.kafka.server/active_connection_count`\)

To enable this integration, first create a [new API key](https://confluent.cloud/settings/api-keys) in Confluent Cloud.

Next, add these additional environment variables to your kPow's deployment:

```
CONFLUENT_API_KEY=XXXYYYZZZZ
CONFLUENT_API_SECRET=XXXYYYZZZZYYYZZZZ
```

kPow will now collect telemetry about your Confluent Cloud cluster using the [Metrics API](https://api.telemetry.confluent.cloud/docs). Once configured disk metrics/stats will start appearing in kPow's UI.

Confluent Cloud metrics will also be available via kPow's [Prometheus integration](../features/prometheus/).

### API Limitations

Confluent Cloud's metrics API has the [following limitations](https://api.telemetry.confluent.cloud/docs#section/Client-Considerations-and-Best-Practices):

* Maximum of 50 requests per minute per IP address
* Maximum of 1000 results returned per metrics query

By default, kPow will scrape disk information for all topic partitions. Given Confluent Cloud's imposed limitations it may not be feasible to query at a topic-partition granularity. For example, if you have over 50, 000 partitions in your cluster, you will exceed the imposed rate limiting.

Because of these limitations, telemetry gathered using Confluent Cloud's metrics API will not be available when in [live mode](../features/live-mode.md).

### Configuration

#### CONFLUENT\_DISK\_MODE

To get around the API limitations imposed by Confluent Cloud's metrics API, kPow has an additional environment variable: `CONFLUENT_DISK_MODE`.

Currently two modes are supported:

* `COMPLETE` \(default\): data is queried at a topic-partition granularity, all replica disk information is complete.
* `INFERRED`: data is queried at a topic granularity. Topic-partition replica disk information is estimated based on other kPow telemetry \(number of messages in partition, average size of record, etc\). Replica disk information at a topic granularity is complete.

If you are bumping up against any of the Confluent Cloud API limitations, it is recommended to set `CONFLUENT_DISK_MODE=INFERRED` if you are comfortable with the topic-partition replica disk data being estimated.

#### CONFLUENT\_METRICS\_URL

If you are using the self-managed Confluent Platform, you can set `CONFLUENT_METRICS_URL=https://my-metrics-endpoint`. 

The default metrics endpoint is `https://api.telemetry.confluent.cloud/v2/metrics/cloud/query`

#### CONFLUENT\_PARALLELISM

Specifies the number of parallel HTTP requests made to the Metrics API when collecting disk telemetry. Defaults to 8.

## Multi-Tenant Confluent Cloud

To connect to two clusters that share the same `BOOTSTRAP` , but are accessed with different auth credentials, provide a unique `CLUSTER_ID` environment variable for each cluster definition, for example:

```text
BOOTSTRAP=pkc-5nym1.us-east-1.aws.confluent.cloud:9092
CLUSTER_ID=confluent-cloud-dev
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=PLAIN
SASL_JAAS_CONFIG=org.apache.kafka.common.security.plain.PlainLoginModule required username="user-1" password="pass-1";
SSL_ENDPOINT_IDENTIFICATION_ALGORITHM=https
CONFLUENT_API_KEY=XXXYYYZZZZ
CONFLUENT_API_SECRET=XXXYYYZZZZYYYZZZZ

BOOTSTRAP_2=pkc-5nym1.us-east-1.aws.confluent.cloud:9092
CLUSTER_ID_2=confluent-cloud-stage
SECURITY_PROTOCOL_2=SASL_SSL
SASL_MECHANISM_2=PLAIN
SASL_JAAS_CONFIG_2=org.apache.kafka.common.security.plain.PlainLoginModule required username="user-2" password="pass-2";
SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_2=https
CONFLUENT_API_KEY_2=XXXYYYZZZZ
CONFLUENT_API_SECRET_2=XXXYYYZZZZYYYZZZZ
```

**Note**: the `CLUSTER_ID` environment variable must be unique across all clusters defined in kPow, and can be any unique identifier \(eg, the string `confluent-cloud-stage`\) 



