---
description: Use kPow to alter Kafka broker configuration and
---

# Brokers

## Prerequisites

* You have setup the correct [access control permissions](../authorization/overview.md) in kPow to allow `BROKER_EDIT` 
* You have setup the [correct ACLs](../installation/minimum-acl-permissions.md) if you have enabled ACLs in your Kafka Cluster

## Broker configuration

To edit topic configuration, navigate to **Configuration** within the **Broker** menu item of kPow's main navigation menu.

### Filtering

You can use the Broker Configuration filters on the top-most menu to filter down the configuration table.

The top-level filters allow you to filter by broker or config item. If you click the slider icon (advanced filters), you can filter config by source, importance and whether the config item is read only.

![Filtering broker configuration](<../.gitbook/assets/Screen Shot 2021-05-05 at 11.30.16 am.png>)

### Broker actions

Broker actions are visible by hovering over the actions icon, the last column of a row in the broker configuration UI. Available actions include viewing documentation and editing config

![Broker actions available in kPow](<../.gitbook/assets/Screen Shot 2021-05-05 at 11.32.49 am.png>)

### Editing config

Clicking the **Edit Config** item inside a topic config item's action menu will bring up the edit config modal. 

![Editing broker configuration](<../.gitbook/assets/Screen Shot 2021-05-05 at 11.36.24 am.png>)
