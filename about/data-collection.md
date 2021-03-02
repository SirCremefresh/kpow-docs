---
description: kPow Privacy and Transparency
---

# Data Collection

This page contains information on how we capture product telemetry and how you can opt out.

Data collection is subject to our [EULA](https://kpow.io/eula/) and [Privacy Policy](https://operatr.io/privacy/).

## How Do I Opt Out?

Trial users cannot opt out of product telemetry.

Licensed users can configure the following environment variable to opt out of product telemetry.

```text
ALLOW_UI_ANALYTICS="false"
```

## How Do We Collect Product Telemetry?

The kPow UI records product usage with [Google Analytics](https://marketingplatform.google.com/about/analytics/).

We receive the standard Google Analytics data set \(page views, location, etc\). We also receive a small number of custom events when you take user action \(topic-create, topic-delete, sample-topic, etc\).

## Do We Collect Sensitive Data?

No. 

The telemetry we capture is restricted to product specific information like page view or user action. 

We do not capture any specifics of your Kafka cluster/s or anything beyond standard google analytics and your interaction with our product user interface.

We may collect your License ID in our analytics events, as described in our [EULA](https://kpow.io/eula/).

## Why Do We Collect Product Telemetry?

Google Analytics is the only mechanism we have to understand how our product is being used.

kPow is designed to run in air-gapped, security conscious environments. When we release new features or tweak our UI it helps to understand how these feature or changes are received by our users.

