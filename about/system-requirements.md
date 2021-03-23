---
description: Built for Simplicity from Kafka and Clojure
---

# System Requirements

## Dependencies

kPow is provided as either a single Docker container or a JAR file.

kPow connects to your Kafka cluster \(and other Kafka resources\) to snapshot them every minute. Those snapshots are computed into metrics. Snapshots, metrics, an audit log, and any other data kPow requires to operate is held in local topics in your cluster.

Beyond at least one Kafka cluster kPow has **no further dependencies.**

## Memory and CPU

kPow can run with as little as **256MB** memory and **0.25** CPU.

We recommend **2GB** memory and **1** CPU for a standard installation but encourage you to experiment with constraining resources as much as possible.

## Memory Constraints

Our Docker container starts the JAR file with **initial and max memory constraints** set to 80% of the resources provided to the container.

```text
CMD java -XX:InitialRAMPercentage=80 -XX:MaxRAMPercentage=80 -jar /opt/operatr/lib/kpow.jar
```

Make sure you to set the memory available to the container on startup \(**-m1G** in this case\):

```text
docker run -p 3000:3000 -m1G --env-file ./kpow.env operatr/kpow:latest
```

If running in Kubernetes **ensure that your pod resources are set**. Preferably run with **pod QOS class guaranteed** by setting both the min and max memory and CPU to the same desired values.

When using the JAR file directly **ensure you set suitable memory constraints** with -Xmx and -Xms:

```text
BOOTSTRAP="your-bootstrap-url" java -Xms1G -Xmx1G -jar ./kpow-latest.jar
```

Failing to set memory constraints may cause kPow to consume more memory than required.

## Disk Space

kPow **does not use local disk** so does not require any particular storage beyond configuration.

kPow topics in your cluster may take up to **10GB** replicated disk ****with the default data retention of 1-week.

## Network

kPow must be installed in reasonably close proximity to your ****Kafka resources as network latency can impact the ability to snapshot and compute telemetry.

**Multi-Region Multi-Cluster** installations are not officially supported, though we are aware users have configured such installations with some success.

## Requirements and Permissions

kPow uses the following resources:

* A Kafka AdminClient to snapshot and update Kafka Cluster resources
* A SchemaRegistryClient to snapshot and update Schema and Subject resources
* The Connect REST API to snapshot and update Kafka Connect resources
* A Kafka Consumer to inspect data on topics
* A Kafka Producer to produce data to topics

kPow must be connected to **at least on Kafka Cluster**.

### Minimum Kafka ACL Permissions

kPow checks for the following internal topics in your **primary cluster** \(the first bootstrap in your configuration\) on startup and will attempt to create them if required:

```text
__oprtr_metric_pt1m
__oprtr_snapshot_state
__oprtr_audit_log
oprtr.compute.metrics.v2-oprtr_metric_v2_pt1m-changelog
oprtr.compute.snapshots.v2-oprtr_snapshot_materialized_v2-repartition
```

You can manually create these topics if you prefer, each with a replication factor of **3** and **12** partitions.

Once started, kPow creates two internal streaming compute applications:

```text
oprtr.compute.metrics.v2
oprtr.compute.snapshots.v2
```

At a minimum, kPow must be able to read and write to and from these internal topics, must be able to read as those groups, and must have permissions to describe clusters, topics, configuration, and groups.

A simple set of Kafka ACL that allows kPow to operate provides **ALLOW** on the following:

| Kafka Resource | Kafka ACL | Detail |
| :--- | :--- | :--- |
| Cluster | Describe | `*` |
| Cluster | DescribeConfigs | `*` |
| Cluster | Create | `* (if not manually creating internal topics)` |
| Topic | Describe | `*` |
| Topic | DescribeConfigs | `*` |
| Topic | Read | `* or internal topics only` |
| Topic | Write | `* or internal topics only` |
| Group | Describe | `*` |
| Group | Read | `* or internal groups only` |

kPow **does not read from or write to topics other than internal ones** as a part of normal operation.

### Feature Specific ACLS

The following ACLS are optional and only required if you intend to permit the associated kPow action.

See [User Authorization](../user-authorization/overview.md#user-actions) for a description of kPow User Actions and Controls.

| Kafka Resource | Kafka ACL | Required for User Action |
| :--- | :--- | :--- |
| Cluster | AlterConfigs | `BROKER_EDIT` |
| Cluster | Create | `TOPIC_CREATE` |
| Topic | AlterConfigs | `TOPIC_EDIT` |
| Topic | Create | `TOPIC_CREATE` |
| Topic | Delete | `TOPIC_DELETE` |
| Topic | Read | `TOPIC_INSPECT` |
| Topic | Write | `TOPIC_PRODUCE` |
| Group | Read / Delete | `GROUP_EDIT` |

