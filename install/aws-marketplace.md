---
description: Purchase and Provision kPow on the AWS Marketplace
---

# AWS Marketplace

kPow is available to purchase via the AWS Marketplace.

When you subscribe to one of the [kPow products available on the AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=ab356f1d-3394-4523-b5d4-b339e3cca9e0) you are given access to a specific kPow AWS Marketplace Docker container that is functionally the same as the kPow Docker container available via [Dockerhub](https://hub.docker.com/r/operatr/kpow).

The AWS Marketplace Docker container makes a single call to [AWSMarketplaceMetering/registerUsage](https://docs.aws.amazon.com/marketplacemetering/latest/APIReference/API_RegisterUsage.html) when kPow starts, allowing AWS to check your subscription and meter your usage if you have chosen the hourly-metered product.

The kPow AWS Marketplace container is **automatically licensed** to the AWS account that subscribe

{% hint style="info" %}
See our [**AWS Marketplace Seller Profile**](https://aws.amazon.com/marketplace/seller-profile?id=ab356f1d-3394-4523-b5d4-b339e3cca9e0) to see every option for purchasing kPow on AWS.
{% endhint %}

