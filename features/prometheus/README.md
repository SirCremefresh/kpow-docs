---
description: Prometheus Endpoints for Long-Term Reporting and Alerting
---

# Prometheus Integration

{% hint style="info" %}
kPow's Prometheus egress endpoints follow the [OpenMetrics](https://openmetrics.io/) standard.

This allows you to integrate kPow to your favourite observability tools such as [Prometheus](https://prometheus.io/docs/prometheus/latest/getting\_started/), [New Relic](https://docs.newrelic.com/docs/integrations/prometheus-integrations/) or [Grafana](https://grafana.com/docs/grafana/latest/getting-started/getting-started-prometheus/) for long-term reporting dashboards and alerting.
{% endhint %}

## Configuration

{% hint style="warning" %}
Prometheus Endpoints are not secure, do not configure if kPow is publicly accessible.
{% endhint %}

To enable Prometheus endpoints set the following **environment variable.**

```bash
PROMETHEUS_EGRESS=true
```

## Getting Started

See our how-to blogpost on [alerting and monitoring with kPow, Prometheus, and AlertManager](https://kpow.io/how-to/kafka-alerting-with-kpow-prometheus-and-alertmanager/).

## Endpoints

kPow provides Prometheus endpoints for all metrics, offsets, and streams.

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

```
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
