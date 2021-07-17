---
description: Use kPow to monitor your Redpanda clusters
---

# Redpanda

## What is Redpanda?

Redpanda is a Kafka® compatible event streaming platform. Read more about Red Panda [here](https://vectorized.io/).

kPow has no reliance on Zookeeper or the JVM and is fully compatible with Redpanda.

## Quick Start

Start a single-node Redpanda cluster with the Docker container provided by Vectorized.

```
docker run -ti -p 9092:9092 vectorized/redpanda:latest
```

Configure kPow to connect to the local Redpanda cluster.

```text
BOOTSTRAP=127.0.0.1:9092
REPLICATION_FACTOR=1
CLUSTER_ID=red-panda
```

**Note**: an extra environment variable `CLUSTER_ID` is required, as Redpanda does not provide a cluster ID when making an admin client request. The `CLUSTER_ID` must be unique across all clusters defined in kPow, and can be any unique identifier.

Start your kPow instance and navigate to the UI.

![](../.gitbook/assets/kpow-overview.png)

