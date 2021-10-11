---
description: Manage Schemas and Subjects with kPow
---

# Schema Registry

## Access Control

User permissions to Kafka cluster resources are defined by [**Schema actions.**](../authorization/overview.md#user-actions)****

## **Configuration**

kPow supports [Confluent Schema Registry](https://github.com/confluentinc/schema-registry) and [AWS Glue Schema Registry](https://github.com/awslabs/aws-glue-schema-registry).

kPow connects to a Schema registry with **environment variables**.

### Confluent Scheme Registry

| Variable                         | Description                                                                                                                                                       |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SCHEMA_REGISTRY_NAME**         | UI and logs friendly name for this Schema registry                                                                                                                |
| **SCHEMA_REGISTRY_URL**          | The client connection URL for your registry                                                                                                                       |
| **SCHEMA_REGISTRY_AUTH**         | USER_INFO if basic authentication is configured                                                                                                                   |
| **SCHEMA_REGISTRY_USER**         | Username if basic authentication is configured                                                                                                                    |
| **SCHEMA_REGISTRY_PASSWORD**     | Password if basic authentication is configured                                                                                                                    |
| **SCHEMA_REGISTRY_RESOURCE_IDS** | Optional, comma separated list of unique ids. Only specify when configuring multiple [s](kafka-connect.md#configuring-multiple-connect-clusters)chema registries. |

### AWS Glue Schema Registry

| Variable                   | Description                                                      |
| -------------------------- | ---------------------------------------------------------------- |
| **SCHEMA_REGISTRY_NAME**   | UI and logs friendly name for this Schema registry               |
| **SCHEMA_REGISTRY_ARN**    | The ARN of your AWS Glue Schema Registry                         |
| **SCHEMA_REGISTRY_REGION** | The Region of your AWS Glue Schema Registry (default: us-east-1) |

### Configuring Multiple Schema Registries

kPow supports multiple Schema Registries associated to a single Kafka cluster. 

To configure multiple Schema Registries, use the environment variable `SCHEMA_REGISTRY_RESOURCE_IDS` to define a comma separated list of Schema Registries. kPow uses the resource ID as a prefix in the environment variable.

Example configuration when configuring two Schema Registries:

```
SCHEMA_REGISTRY_RESOURCE_IDS=US1,EU2

US1_SCHEMA_REGISTRY_URL="https://us1.schema-registry.mycorp.org"
US1_SCHEMA_REGISTRY_AUTH="USER_INFO"
US1_SCHEMA_REGISTRY_USER="****"
US1_SCHEMA_REGISTRY_PASSWORD="****"

EU2_SCHEMA_REGISTRY_URL="https://eu2.schema-registry.mycorp.org"
EU2_SCHEMA_REGISTRY_AUTH="USER_INFO"
EU2_SCHEMA_REGISTRY_USER="****"
EU2_SCHEMA_REGISTRY_PASSWORD="****"
```

![kPow's startup log message confirming it has connected to both Schema Registries.](<../.gitbook/assets/Screen Shot 2021-03-29 at 4.14.03 pm.png>)

Multiple Schema Registries are navigable via the left hand or context menus.

![kPow's navigation menu when multiple Schema Registries have been configured.](<../.gitbook/assets/Screen Shot 2021-03-29 at 4.12.11 pm.png>)
