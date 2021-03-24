---
description: Manage Schemas and Subjects with kPow
---

# Schema Registry

{% hint style="info" %}
kPow will manage **one Schema registry per configured Kafka cluster.**
{% endhint %}

## Access Control

User permissions to Kafka cluster resources are defined by [**Schema actions.**](../authorization/overview.md#user-actions)\*\*\*\*

## **Configuration**

kPow connects to a Schema registry with **environment variables**.

| Variable | Description |
| :--- | :--- |
| **SCHEMA\_REGISTRY\_NAME** | UI and logs friendly name for this Schema registry |
| **SCHEMA\_REGISTRY\_URL** | The client connection URL for your registry |
| **SCHEMA\_REGISTRY\_AUTH** | USER\_INFO if basic authentication is configured |
| **SCHEMA\_REGISTRY\_USER** | Username if basic authentication is configured |
| **SCHEMA\_REGISTRY\_PASSWORD** | Password if basic authentication is configured |

