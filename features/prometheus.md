---
description: kPow Exposes Prometheus Endpoints for Alerting and Reporting
---

# Prometheus Integration

Use your favourite enterprise monitoring platform for alerting and to retain long-term Kafka telemetry.

## Configuration

To enable Prometheus endpoints set the following **environment variable.**

```bash
PROMETHEUS_EGRESS=true
```

## Endpoints

kPow provides Prometheus endpoints all metrics, all offsets, and the same by resource.

{% hint style="info" %}
kPow logs the path to each Prometheus endpoint on startup
{% endhint %}

```bash
* GET /metrics/v1 - all metrics
* GET /offsets/v1 - all topic offsets
* GET /offsets/v1/topic/[topic-name] - all topic offsets for specific topic, all clusters
* GET /metrics/v1/cluster/v-EEfIOXRqCDS6JpK0X0Pw - metrics for cluster Trade Book (Staging)
* GET /offsets/v1/cluster/v-EEfIOXRqCDS6JpK0X0Pw - offsets for cluster Trade Book (Staging)
* GET /metrics/v1/cluster/lkc-lo0o9 - metrics for cluster Outbound Payments (Staging)
* GET /offsets/v1/cluster/lkc-lo0o9 - offsets for cluster Outbound Payments (Staging)
* GET /metrics/v1/schema/a2f06a916672d71d675f - metrics for schema registry
```

