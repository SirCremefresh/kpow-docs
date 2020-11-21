---
description: Get started with kPow for in two minutes.
---

# Quick Start

This page provides Quick Start instructions for [**Docker**](quick-start.md#docker-quick-start) and [**JAR** ](quick-start.md#jar-quick-start)installations.

## Docker Quick Start

To connect the latest kPow Docker image to a single, unsecured Kafka Cluster:

* Get a [**Free Trial License**](../about/trials-and-licenses.md).
* Create a **`config.env`** file containing your connection, license, and feature variables.

```text
## The Kafka Bootstrap URL for your cluster (Required).
BOOTSTRAP=kafka-1:9092,kafka-2:9092,kafka-3:9092

## Your license details (Required).
LICENSE_ID=1c99v4-f690-4a4f-b144-73de2369444a
LICENSE_CODE=TRIAL_30D
LICENSEE=My Corp
LICENSE_EXPIRY=2020-09-05
LICENSE_SIGNATURE=17D6DB591EF4A2F...

## Optional from here:

## Name your Operatr installation (this appears in the UI)
ENVIRONMENT_NAME=Trade Book (Staging)

## Operatr Feature Flags (See: RBAC for per user controls):

## Allow users to create new topics 
ALLOW_TOPIC_CREATE=true

## Allow users to delete topics 
ALLOW_TOPIC_DELETE=true

## Allow users to edit topic configuration
ALLOW_TOPIC_EDIT=true

## Allow users to view topic data
ALLOW_TOPIC_INSPECT=true

## Allow users to produce messages to topics
ALLOW_TOPIC_PRODUCE=true

## ... etc (see guide for more configuration flags).
```

* Start the latest kPow container with your **`config.env`** file.

```text
docker run -p 3000:3000 -m1G --env-file ./config.env operatr/kpow:latest
```

* kPow is now running on **`http://localhost:3000`**

## JAR Quick Start

To connect the latest [kPow JAR](https://operatr.io/releases) to a single, unsecured Kafka cluster:

* Get a [**Free Trial License**](../about/trials-and-licenses.md).
* Download [**the latest kPow JAR**](https://kpow.io/releases/).
* Create a**`start-kpow.sh`** that sets environment variables and starts the JAR

**Note:** Quoting may be required for some variables

```text
BOOTSTRAP="kafka-1:9092,kafka-2:9092,kafka-3:9092" \
LICENSE_ID=1c99v4-f690-4a4f-b144-73de2369444a \
LICENSE_CODE=TRIAL_30D \
LICENSEE="My Corp" \
LICENSE_EXPIRY=2020-09-05 \
LICENSE_SIGNATURE=17D6DB591EF4A2F... \
ENVIRONMENT_NAME="Trade Book (Staging)" \
ALLOW_TOPIC_CREATE=true \
ALLOW_TOPIC_DELETE=true \
ALLOW_TOPIC_EDIT=true \
ALLOW_TOPIC_INSPECT=true \
ALLOW_TOPIC_PRODUCE=true \
java -jar -Xmx1G ./kpow-latest.jar
```

* Run **`chmod +x start-kpow.sh`** then **`./start-kpow.sh`**
* kPow is now running on **`http://localhost:3000`**

