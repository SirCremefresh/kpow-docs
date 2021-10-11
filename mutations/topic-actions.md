---
description: Use kPow to create and manage Kafka topics
---

# Topics

## Prerequisites

* You have setup the correct [access control permissions](../authorization/overview.md) in kPow to allow `TOPIC_CREATE` and `TOPIC_EDIT`
* You have setup the [correct ACLs](../installation/minimum-acl-permissions.md) if you have enabled ACLs in your Kafka Cluster

## Topic Create

Topic create can be found in the navigation menu under the **Topic** menu item.

By default, the form will use the cluster's default replication factor and number of partitions. You can specify your own values for both.

![Topic create at a glance](<../.gitbook/assets/Screen Shot 2021-04-29 at 3.51.44 pm.png>)

### Configuration

You can add configuration options to your topic by using the **Add configuration** dropdown and selecting the custom configuration you would like to add to your topic.

![Topic create configuration in kPow](<../.gitbook/assets/Screen Shot 2021-04-29 at 3.54.12 pm.png>)

Clicking the **Show description **link will open up the documentation accordion for the configuration item. \
The contents of the description include the configuration item's documentation, its type, default and common values. Common values are the top-5 most common values set on your cluster. Clicking on one of these values will pre-fill the configuration form for the item.

![Documentation about compression.type.](<../.gitbook/assets/Screen Shot 2021-04-29 at 3.57.49 pm.png>)

### Copy configuration 

Within the UI you can also copy the configuration of other topics within a cluster. For example if you select **\__consumer_offsets** from the dropdown, this will pre-fill the configuration of **\__consumer_offsets** into the form.

### kafka-topics.sh export

If you do not wish to grant kPow the ability to mutate your cluster's topics, you can still use the Topic Create form to build out your request. On the right-hand side of the form is the Kafka Script equivalent, which can be piped into `kafka-topics.sh` . This will reactively update as you fill out the form.

![An example of the Kafka Script Equivalent inside of kPow's Topic Create UI](<../.gitbook/assets/Screen Shot 2021-04-29 at 4.00.59 pm.png>)

## Topic Edit

To edit topic configuration, navigate to **Configuration** within the **Topic** menu item of kPow's main navigation menu.

### Filtering

You can use the Topic Configuration filters on the top-most menu to filter down the configuration table.

The top-level filters allow you to filter by topic or config item. If you click the slider icon (advanced filters), you can filter config by source, importance and whether the config item is read only.



![kPow's Topic Configuration filters.](<../.gitbook/assets/Screen Shot 2021-04-29 at 4.15.11 pm.png>)

### Topic actions

Topic actions are visible by hovering over the actions icon, the last column of a row in the topic configuration UI. Available actions include viewing documentation and editing config

![Actions available for \__consumer_offsets' cleanup.policy](<../.gitbook/assets/Screen Shot 2021-04-29 at 4.17.33 pm (1).png>)

### Editing config

Clicking the **Edit Config** item inside a topic config item's action menu will bring up the edit config modal. This modal looks similar to the Topic Create UI, and will allow you to edit the config item. 

![The Edit Config modal for \__consumer_offsets' cleanup.policy](<../.gitbook/assets/Screen Shot 2021-04-29 at 4.23.46 pm.png>)
