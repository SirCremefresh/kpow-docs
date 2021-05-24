---
description: kPow Exposes Prometheus Endpoints for Alerting and Reporting
---

# Prometheus Integration

{% hint style="info" %}
kPow's metrics egress endpoints follow the [OpenMetrics](https://openmetrics.io/) standard. This allows for kPow to integrate with your favourite observability tools such as [Prometheus](https://prometheus.io/docs/prometheus/latest/getting_started/), [New Relic](https://docs.newrelic.com/docs/integrations/prometheus-integrations/) or [Grafana](https://grafana.com/docs/grafana/latest/getting-started/getting-started-prometheus/) 
{% endhint %}

Use your favourite enterprise monitoring platform for alerting and to retain long-term Kafka telemetry.

## Configuration

To enable Prometheus endpoints set the following **environment variable.**

```bash
PROMETHEUS_EGRESS=true
```

## Getting Started

[This blog post](https://kpow.io/how-to/kafka-alerting-with-kpow-prometheus-and-alertmanager/) covers an introduction to alerting and monitoring with kPow + Prometheus + AlertManager.

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

## Sample Scraper Configuration

Sample Prometheus scraper configuration that we use to test kPow:

```text
scrape_configs:
  - job_name: 'operatr'
    metrics_path: '/metrics/v1'
    static_configs:
      - targets: ['host.docker.internal:3000']
  - job_name: 'operatr_streams'
    metrics_path: '/streams/v1'
    static_configs:
      - targets: ['host.docker.internal:3000']
  - job_name: 'operatr_offsets'
    metrics_path: '/offsets/v1'
    static_configs:
      - targets: ['host.docker.internal:3000']
```

