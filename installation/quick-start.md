---
description: Get started with kPow for in two minutes.
---

# Quick Start

This page provides Quick Start instructions for [**Docker**](quick-start.md#docker-quick-start) and [**JAR** ](quick-start.md#jar-quick-start)installations.

{% hint style="success" %}
Use our [**Helm**](https://github.com/operatr-io/kpow-helm-charts) and [**CloudFormation**](https://github.com/operatr-io/kpow-cloudformation) guides to get up and running in minutes.
{% endhint %}

## Docker Quick Start

{% hint style="info" %}
kPow Docker images are hosted at [**Docker Hub**](https://hub.docker.com/r/operatr/kpow)**.**
{% endhint %}

To connect the latest kPow Docker image to a single, unsecured Kafka Cluster:

* Get a [**Free Trial License**](../about/trials-and-licenses.md).
* Create a **`config.env`** file containing your connection, license, and feature variables.

```text
## The Kafka Bootstrap URL for your cluster (Required).
BOOTSTRAP=kafka-1:9092,kafka-2:9092,kafka-3:9092

## Your license details (Required).
## These parameters can be cut/paste from your license email
LICENSE_ID=1c99v4-f690-4a4f-b144-73de2369444a
LICENSE_CODE=TRIAL_30D
LICENSEE=My Corp
LICENSE_EXPIRY=2020-09-05
LICENSE_SIGNATURE=15CFFF969111DB6DCA142B6F1E0065F94A614251B80128D52C2CD45993A021AE10E90F57B90FF76CC1B992C16E54BCF1CBE7E5EE3124B3E585BE133774836A6EBB51B55E67EF60F4A435EBEC9F07A26CEABDCF6E3CF4137A33201E7662AF1F7986E57341E0EAEB884BBF320C348D62679F521259DAD1E03F6F79DB53D83CD41B

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

{% hint style="info" %}
Some variables may require quotes, and each line ends with a `\` character.
{% endhint %}

```text
BOOTSTRAP="kafka-1:9092,kafka-2:9092,kafka-3:9092" \
LICENSE_ID=1c99v4-f690-4a4f-b144-73de2369444a \
LICENSE_CODE=TRIAL_30D \
LICENSEE="My Corp" \
LICENSE_EXPIRY=2020-09-05 \
LICENSE_SIGNATURE=15CFFF969111DB6DCA142B6F1E0065F94A614251B80128D52C2CD45993A021AE10E90F57B90FF76CC1B992C16E54BCF1CBE7E5EE3124B3E585BE133774836A6EBB51B55E67EF60F4A435EBEC9F07A26CEABDCF6E3CF4137A33201E7662AF1F7986E57341E0EAEB884BBF320C348D62679F521259DAD1E03F6F79DB53D83CD41B \
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

