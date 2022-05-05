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



| Variable                            | Description                                                                                             |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **SCHEMA\_REGISTRY\_NAME**          | UI and logs friendly name for this Schema registry                                                      |
| **SCHEMA\_REGISTRY\_URL**           | The client connection URL for your registry                                                             |
| **SCHEMA\_REGISTRY\_AUTH**          | USER\_INFO if basic authentication is configured                                                        |
| **SCHEMA\_REGISTRY\_USER**          | Username if basic authentication is configured                                                          |
| **SCHEMA\_REGISTRY\_PASSWORD**      | Password if basic authentication is configured                                                          |
| **SCHEMA\_REGISTRY\_RESOURCE\_IDS** | Optional, comma separated list of unique ids. Only specify when configuring multiple schema registries. |

#### Mutual TLS

The following environment variables can be used to configure Confluent schema registry connections with mutual TLS:

* SCHEMA\_REGISTRY\_SSL\_KEYSTORE\_LOCATION
* SCHEMA\_REGISTRY\_SSL\_KEYSTORE\_PASSWORD
* SCHEMA\_REGISTRY\_SSL\_KEY\_PASSWORD
* SCHEMA\_REGISTRY\_SSL\_KEYSTORE\_TYPE
* SCHEMA\_REGISTRY\_SSL\_KEYMANAGER\_ALGORITHM
* SCHEMA\_REGISTRY\_SSL\_TRUSTSTORE\_LOCATION
* SCHEMA\_REGISTRY\_SSL\_TRUSTSTORE\_PASSWORD
* SCHEMA\_REGISTRY\_SSL\_TRUSTSTORE\_TYPE
* SCHEMA\_REGISTRY\_SSL\_TRUSTMANAGER\_ALGORITHM
* SCHEMA\_REGISTRY\_SSL\_ENDPOINT\_IDENTIFICATION\_ALGORITHM
* SCHEMA\_REGISTRY\_SSL\_PROVIDER
* SCHEMA\_REGISTRY\_SSL\_CIPHER\_SUITES
* SCHEMA\_REGISTRY\_SSL\_PROTOCOL
* SCHEMA\_REGISTRY\_SSL\_ENABLED\_PROTOCOLS
* SCHEMA\_REGISTRY\_SSL\_SECURE\_RANDOM\_IMPLEMENTATION
* SCHEMA\_REGISTRY\_SSL\_KEYSTORE\_KEY
* SCHEMA\_REGISTRY\_SSL\_KEYSTORE\_CERTIFICATE\_CHAIN
* SCHEMA\_REGISTRY\_SSL\_TRUSTSTORE\_CERTIFICATES
* SCHEMA\_REGISTRY\_SSL\_ENGINE\_FACTORY\_CLASS

### AWS Glue Schema Registry

| Variable                     | Description                                                      |
| ---------------------------- | ---------------------------------------------------------------- |
| **SCHEMA\_REGISTRY\_NAME**   | UI and logs friendly name for this Schema registry               |
| **SCHEMA\_REGISTRY\_ARN**    | The ARN of your AWS Glue Schema Registry                         |
| **SCHEMA\_REGISTRY\_REGION** | The Region of your AWS Glue Schema Registry (default: us-east-1) |

### Configuring Multiple Schema Registries

kPow supports multiple Schema Registries associated to a single Kafka cluster.&#x20;

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
