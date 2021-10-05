---
description: kPow Privacy and Transparency
---

# Data Collection

This page contains information on how we capture product telemetry and how you can opt out.

Data collection is subject to our [EULA](https://kpow.io/eula/) and [Privacy Policy](https://operatr.io/privacy/).

## How Do I Opt Out?

You can opt out of product telemetry by setting the environment variable:

```text
ALLOW_UI_ANALYTICS="false"
```

When that environment variable is configured kPow does not record or send any product telemetry.

Note: If you are using kPow with a 30-day trial license, turning analytics off is not supported.

## How Do We Collect Product Telemetry?

The kPow UI records product usage with [Google Analytics](https://marketingplatform.google.com/about/analytics/).

We receive the standard Google Analytics data set \(page views, location, etc\). We also receive a small number of custom events when you take user action \(topic-create, topic-delete, sample-topic, etc\).

## Do We Collect Sensitive Data?

No. 

The telemetry we capture is restricted to product specific information like page view or user action.

Page views **do not include query strings or url fragments** \(which do contain sensitive data\).

We do not capture any specifics of your Kafka cluster/s or anything beyond standard google analytics and your interaction with our product user interface.

We may collect your License ID in our analytics events, as described in our [EULA](https://kpow.io/eula/).

## Why Do We Collect Product Telemetry?

Google Analytics is the only mechanism we have to understand how our product is being used.

kPow is designed to run in air-gapped, security conscious environments. When we release new features or tweak our UI it helps to understand how these feature or changes are received by our users.

