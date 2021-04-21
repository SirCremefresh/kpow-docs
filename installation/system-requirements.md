---
description: kPow Minimum System Requirements
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

## Resources

kPow uses the following resources:

* A Kafka AdminClient to snapshot and update Kafka Cluster resources
* A SchemaRegistryClient to snapshot and update Schema and Subject resources
* The Connect REST API to snapshot and update Kafka Connect resources
* A Kafka Consumer to inspect data on topics
* A Kafka Producer to produce data to topics

kPow must be connected to **at least on Kafka Cluster**.

