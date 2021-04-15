---
description: >-
  Deployment notes for running kPow on container platforms such as Kubernetes,
  ECS/Fargate
---

# Deployment Notes

## Templates

The [operatr-io/infra GitHub repository](https://github.com/operatr-io/infra) contains example configurations for deploying kPow to orchestration platforms such as:

* ECS/Fargate \(more notes found in our [AWS Marketplace](aws-marketplace.md) guide\)
* Kubernetes + Helm
* Red Hat Openshift \(more notes found in our [OpenShift](openshift.md) guide\)

## Resource limits

See [System Requirements](../about/system-requirements.md) for notes on configuring CPU/memory limits for kPow

## Liveness and Readiness endpoints

kPow's healthcheck endpoint is served as a GET request at `/healthy`. This path can be used as a liveness probe from within your orchestration platform of choice.

* The `/healthy` endpoint returns a `200` status code if the kPow instance is healthy. 
* The `/healthy` endpoint returns a `503` status code if the kPow instance is unhealthy \(see: [Error states + strategies](deployment-notes.md#error-states-strategies)\)
* The `/healthy` endpoint does not require any user authentication to access. 

The `/up` endpoint can be used for readiness probes. It always returns a `200` status when kPow's HTTP server is up and reachable.

## Error states + strategies

kPow runs an internal [Kafka Streams](https://kafka.apache.org/documentation/streams/) resource that may enter an `ERROR` state in certain scenarios where a Kafka Cluster becomes unavailable for a duration longer than the configured timeout+heartbeat. 

You can configure the `STREAMS_ERROR_STRATEGY` environment variable to handle this scenario. Possible strategies include:

* `LOG_EXCEPTION` - default, logs an error. Note: once kPow enters this ERROR state, snapshotting will continue, but the UI will be unavailable until the instance has been manually restarted.
* `LOG_AND_EXIT` - logs an error and exits the kPow process with a status code of `1`

{% hint style="info" %}
Note: it is recommended to configure a [liveness probe](deployment-notes.md#liveness-and-readiness-endpoints) over setting the `LOG_AND_EXIT` strategy. However, in scenarios such as deploying a JAR to an EC2 instance, configuring this strategy may be desirable.
{% endhint %}

## Availability

{% hint style="info" %}
Highly available + distributed kPow is in the backlog and coming soon!
{% endhint %}

At the moment, kPow is designed to be run as a single instance. When defining your task definition for kPow please ensure that the maximum number of instances does not exceed one.

