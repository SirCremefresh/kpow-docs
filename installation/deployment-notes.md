---
description: Run kPow on platforms such as Kubernetes and ECS/Fargate
---

# Deployment Notes

## Templates

The [operatr-io/infra GitHub repository](https://github.com/operatr-io/infra) contains example configurations for deploying kPow to orchestration platforms such as:

* ECS/Fargate \(more notes found in our [AWS Marketplace](aws-marketplace.md) guide\)
* Kubernetes + Helm
* Red Hat Openshift \(more notes found in our [OpenShift](openshift.md) guide

## Liveness and Readiness Endpoints

kPow's health check endpoint is served as a GET request at `/healthy`. This path can be used as a liveness probe from within your orchestration platform of choice.

* The `/healthy` endpoint returns a `200` status code if the kPow instance is healthy. 
* The `/healthy` endpoint returns a `503` status code if the kPow instance is unhealthy \(see: [Error states + strategies](deployment-notes.md#error-states-strategies)\)
* The `/healthy` endpoint does not require any user authentication to access. 

The `/up` endpoint can be used for readiness probes. It always returns a `200` status when kPow's HTTP server is up and reachable.

## Error States + Strategies

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

## Reverse Proxies + Load Balancers

Set the `HTTP_FORWARDED=true` environment variable to ensure that redirects respect the correct scheme when terminating SSL at the proxy.

{% hint style="info" %}
kPow serves all of its HTTP traffic at the specified`PORT`\(defaulting to 3000\). 
{% endhint %}

This port serves both websockets connections and general HTTP traffic.

Most reverse proxies and load balancers work out of the box with kPow, but special consideration is needed when configuring websockets, or when the reverse proxy is responsible for SSL termination.

See HTTPS Connections for documentation on how to configure HTTPS traffic for kPow.

{% hint style="warning" %}
Configure `HTTP_FORWARDED` in conjunction with Jetty Authentication to ensure that redirects to the login page maintain the correct connection scheme.
{% endhint %}

### NGINX Configuration

#### Standard Configuration 

A standard `nginx.conf` 

```text
  server {
    listen       80;
    server_name  localhost;

     location /  {
      proxy_pass http://localhost:3000/;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      proxy_cache_bypass $http_upgrade;
      proxy_headers_hash_max_size 512;
      proxy_headers_hash_bucket_size 128;
     }
}
```

#### Custom Path Configuration

This configuration might be useful if you want to serve kPow at a custom path such as `/kpow` . This scenario might be useful if your company has a suite of tools that you want to have grouped at a single HTTP endpoint.

```text
server {
  listen       80;
  server_name  localhost;

   location /prometheus/ { 
     # configuration options for your prometheus server go here...
   }

   location /kpow/  {
      proxy_pass http://localhost:3000/;
      rewrite /kpow/(.*) /$1 break;
      proxy_redirect http://localhost/ /kpow/;

      proxy_http_version 1.1;

      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      proxy_cache_bypass $http_upgrade;
      proxy_headers_hash_max_size 512;
      proxy_headers_hash_bucket_size 128;
     }
}
```



