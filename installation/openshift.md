---
description: Quick start guide to running kPow on OpenShift
---

# OpenShift

{% hint style="info" %}
kPow is available to purchase on the [**Red Hat Marketplace**](https://marketplace.redhat.com/en-us/products/operatr-for-apache-kafka)**.**
{% endhint %}

## Basics

{% hint style="success" %}
kPow is compatible with **Red Hat AMQ Streams**
{% endhint %}

kPow is available as an Operator on the Red Hat Marketplace and OperatorHub.

Installed in one click and requiring little configuration, kPow will manage and monitor your Kafka resources (including Clusters, Schema Registries, and Connect Installations) security and safely with all data stored in local topics within your cluster.

## Prerequisites

kPow has two prerequisites:

#### License

kPow requires a license to operate, [get a 30-day free trial license in minutes](https://kpow.io/try).

If you purchase kPow on the Red Hat Marketplace a license will automatically be provisioned for you.

#### Kafka Cluster

kPow requires at least one Kafka Cluster bootstrap URL in order to start correctly

All configuration beyond License and Kafka bootstrap URL is optional.

## OperatorHub

### Install the kPow Operator

Select the `OperatorHub` from the `Operators` menu and search for **kPow.**

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.15.42 pm.png>)

Select **kPow** and click **Install**

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.18.20 pm.png>)

Select the install options. kPow instances are stateless, all data is stored in your Kafka Cluster, and we are committed to seamless upgrades - we recommend you select Automatic approval strategy.

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.31.11 pm.png>)

kPow is now available as an installed Operator in your OpenShift cluster!

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.32.35 pm.png>)

### Launch a kPow Instance

Select the kPow for Apache Kafka Operator

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.35.33 pm.png>)

#### Obtain a kPow License

kPow requires a license to run. You can start a 30-day free trial by following the link in the Operator summary (above). A trial license will be emailed to you within minutes of signing up.

#### Create a kPow Instance

kPow is configured almost entirely via environment variables.

There are some small number of optional configuration files (yaml and keystores) that you may need to configure depending on your requirements and/or environment. In each case you will provide those files to the kPow instance via secrets. Details of creating secrets and configuring files are in the Operator summary.

When you have a license and the bootstrap of your Kafka Cluster, click **Create Instance **then **YAML View**

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.41.44 pm.png>)

#### **Configure the kPow Instance**

The minimum configuration required to launch a kPow is **licence** and **bootstrap** details.

See the kPow Operator summary for details on advanced configuration options and secrets.

After setting the YAML options, click **Create**

#### **View Installed Operators**

Validate that the kPow instance is deployed successfully:

**Operators > Installed Operators > kPow for Apache Kafka > Kpow**

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 9.48.24 pm.png>)

#### View the kPow UI

Select the installed kPow instance from the list of kPows

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 10.01.38 pm.png>)

Select **Resources / kPow**

![](<../.gitbook/assets/Screen Shot 2021-03-26 at 10.03.00 pm.png>)

Click the **Location** URL to navigate to kPow and start using the product

![](../.gitbook/assets/kpow-overview.png)

## Get Help!

If you need any assistance installing or configuring kPow on OpenShift contact **support@operatr.io**

## Red Hat Marketplace

{% hint style="info" %}
Register your OpenShift cluster to purchase kPow on the Red Hat Marketplace
{% endhint %}

Installation of kPow from the Red Hat Marketplace requires the OpenShift cluster to be registered to the Marketplace Portal, including the roll out of the PullSecret in your cluster. 

Failure to register will result in an image pull authentication failure with the Red Hat registry.

