---
description: Use kPow with your Azure Event Hubs namespace.
---

# Azure Event Hubs

## Prerequisites 

kPow can connect to your Azure Event Hubs namespace(s) if you have enabled Kafka Surface. \
You can read about using Event Hubs with Kafka [here](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview).

You can verify that Kafka Surface has been enabled, by navigating to your Event Hubs namespace overview inside the Microsoft Azure portal:

![Verifying Kafka Surface is enabled](<../.gitbook/assets/Screen Shot 2021-03-16 at 3.46.10 pm.png>)

## Configuration 

Once you have verified Kafka Surface is enabled, visit the [Security and authentication](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview#security-and-authentication) section of Azure's documentation to find Kafka configuration properties for each type of authentication mechanism.

For example, if you were to use [**Shared Access Signature (SAS)**](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview#shared-access-signature-sas)** **connection details, the environment variables passed to kPow would look like:

```
BOOTSTRAP=NAMESPACENAME.servicebus.windows.net:9093
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=PLAIN
SASL_JAAS_CONFIG=sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";
CLUSTER_ID=azure-event-hubs
AZURE_EVENT_HUBS=true
```

**Note**: an extra environment variable `CLUSTER_ID` is required, as Azure event hubs does not provide a cluster ID when making an admin client request. \
The `CLUSTER_ID` must be unique across all clusters defined in kPow, and can be any unique identifier (eg, the namespace name of your event hub) 

The `AZURE_EVENT_HUBS` environment variable must be set to `true` as Event Hubs does not support the topic configuration of `retention.ms` set to `-1` (which is set by kPow's [audit log](../features/data-governance.md) + Kafka Streams internal topics). Topics that normally have infinite retention will have a 7 day retention set in Event Hubs.

## Event Hubs limitations

The vast majority of kPow's features work with Azure Event Hubs, with the exception of:

* Broker disk information/metrics - as the admin client request does not return any log details
* Broker configuration - as the admin client request does not return any broker configuration details
