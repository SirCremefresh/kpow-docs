---
description: Use kPow to monitor your Redpanda clusters
---

# Redpanda

{% hint style="warning" %}
kPow is not officially supported with Redpanda.

You may experience reduced function or unpredictable behaviour when using kPow with Redpanda. **kPow Support is strictly limited to Apache Kafka only.**
{% endhint %}

## What is Redpanda?

Redpanda is a Kafka® compatible event streaming platform. Read more about Red Panda [here](https://vectorized.io/).

## Quick Start

Start a single-node Redpanda cluster with the Docker container provided by Vectorized.

See: [https://vectorized.io/docs/quick-start-docker/](https://vectorized.io/docs/quick-start-docker/) for details of multi-broker setups.

```
docker run -d --pull=always --name=redpanda-1 --rm \
-p 9092:9092 \
docker.vectorized.io/vectorized/redpanda:latest \
redpanda start \
--overprovisioned \
--smp 1  \
--memory 1G \
--reserve-memory 0M \
--node-id 0 \
--check=false
```

Configure kPow to connect to the local Redpanda cluster.

{% hint style="warning" %}
You must provide a unique **CLUSTER\_ID** for each Redpanda Bootstrap configured
{% endhint %}

```
ENVIRONMENT_NAME=Redpanda
BOOTSTRAP=127.0.0.1:9092
REPLICATION_FACTOR=1
CLUSTER_ID=red-panda-1
```

Start your kPow instance and navigate to the UI.

![](../.gitbook/assets/kpow-overview.png)
