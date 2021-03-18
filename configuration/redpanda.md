---
description: Use kPow to monitor your Redpanda clusters
---

# Redpanda

## What is Redpanda?

Redpanda is a Kafka® compatible event streaming platform. No Zookeeper®, no JVM, and no code changes required.

Read more about Red Panda [here](https://vectorized.io/)

Because kPow does not use Kafka's JMX metrics or require a Zookeeper® connection, all of kPow's metrics are fully supported when using Redpanda!

## Configuration

Example kPow configuration when connecting to a single-node Redpanda cluster running inside Docker:

```
docker run -ti -p 9092:9092 vectorized/redpanda:latest
```

```text
 BOOTSTRAP="127.0.0.1:9092"
 REPLICATION_FACTOR="1"
 CLUSTER_ID="red-panda"
 REDPANDA="true"
```

**Note**: an extra environment variable `CLUSTER_ID` is required, as Redpanda does not provide a cluster ID when making an admin client request.   
The `CLUSTER_ID` must be unique across all clusters defined in kPow, and can be any unique identifier

The `REDPANDA` environment var is required to get around the open issue that Redpanda does not support the `message.timestamp.type = LogAppendTime` config value, which kPow requires internally for its snapshot topics. Once [this issue](https://github.com/vectorizedio/redpanda/issues/626) has been resolved, this environment variable will become deprecated.

## Limitations

The vast majority of kPow's features work with Redpanda, with the exception of:

* Broker disk information/metrics - as the admin client request does not return any log details

