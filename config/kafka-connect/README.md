---
description: Create and Control Connectors and Tasks with kPow
---

# Kafka Connect

## Access Control

User permissions to Kafka cluster resources are defined by [**Connect actions.**](../../authorization/overview.md#user-actions) ****&#x20;

## **Configuration**

kPow connects to a Connect cluster with **environment variables**.

| Variable                            | Description                                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CONNECT\_REST\_URL**              | The client connection URL for your connect cluster                                                                                                |
| **CONNECT\_AUTH**                   | BASIC if basic authentication is configured                                                                                                       |
| **CONNECT\_BASIC\_AUTH\_USER**      | Username if basic authentication is configured                                                                                                    |
| **CONNECT\_BASIC\_AUTH\_PASS**      | Password if basic authentication is configured                                                                                                    |
| **CONNECT\_OFFSET\_STORAGE\_TOPIC** | (Optional) Topic that holds connect offsets                                                                                                       |
| **CONNECT\_GROUP\_ID**              | (Optional) Unique string identifying worker cluster group                                                                                         |
| **CONNECT\_PERMISSIVE\_SSL**        | True if SSL certificate validation should be disabled                                                                                             |
| **CONNECT\_TIMEOUT\_MS**            | The timeout value in ms for all HTTP requests made to a Kafka Connect cluster. Default: 5000                                                      |
| **CONNECT\_RESOURCE\_IDS**          | Optional, comma separated list of unique ids. Only specify when configuring multiple [connect clusters](./#configuring-multiple-connect-clusters) |

### Configuring Multiple Connect Clusters

kPow supports multiple Kafka Connect clusters associated to a single Kafka cluster.&#x20;

To configure multiple Kafka Connect clusters, use the environment variable `CONNECT_RESOURCE_IDS` to define a comma separated list of Connect clusters. kPow uses the resource ID as a prefix in the environment variable.

Example configuration when configuring two Kafka Connect clusters:

```
CONNECT_RESOURCE_IDS=US1,EU2
US1_CONNECT_REST_URL=http://us1-connect.mycorp.org:8003
EU2_CONNECT_REST_URL=http://eu2-connect.mycorp.org:8003
```

In this example we have defined a connection to two Kafka Connect resources: `US1` and `EU2`

![kPow's startup log message confirming it has connected to both Connect clusters.](<../../.gitbook/assets/Screen Shot 2021-03-29 at 3.46.10 pm.png>)

Multiple Connect Clusters are navigable via the left hand or context menus.

![kPow's navigation menu when multiple Connect clusters have been configured.](<../../.gitbook/assets/Screen Shot 2021-03-29 at 3.48.55 pm.png>)







