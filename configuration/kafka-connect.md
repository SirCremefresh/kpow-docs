---
description: Create and Control Connectors and Tasks with kPow
---

# Kafka Connect

{% hint style="info" %}
kPow will manage **one Connect cluster per configured Kafka cluster.**
{% endhint %}

## Access Control

User permissions to Kafka cluster resources are defined by [**Connect actions.**](../user-authorization/overview.md#user-actions)\*\*\*\*

## **Configuration**

kPow connects to a Connect cluster with **environment variables**.

| Variable | Description |
| :--- | :--- |
| **CONNECT\_REST\_URL** | The client connection URL for your connect cluster |
| **CONNECT\_AUTH** | BASIC if basic authentication is configured |
| **CONNECT\_BASIC\_AUTH\_USER** | Username if basic authentication is configured |
| **CONNECT\_BASIC\_AUTH\_PASS** | Password if basic authentication is configured |
| **CONNECT\_OFFSET\_STORAGE\_TOPIC** | \(Optional\) Topic that holds connect offsets |
| **CONNECT\_PERMISSIVE\_SSL** | True if SSL certificate validation should be disabled |

