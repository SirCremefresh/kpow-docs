---
description: Manage Kafka Connect from within kPow
---

# Connect

## Prerequisites

* You have setup the correct [access control permissions](../authorization/overview.md) in kPow to allow `CONNECT_CREATE` and `CONNECT_EDIT`
* You have configured [Kafka Connect](../config/kafka-connect.md) within kPow

## Creating Connectors

Creating a new Connector can be found in the navigation menu under the **Connect** menu item.

The form will prompt you to create a connector for either a **sink** or a **source** and for which connector class. In this example we will create a new sink for the `S3SinkConnector`

![Selecting a connector class](<../.gitbook/assets/Screen Shot 2021-05-05 at 12.14.45 pm.png>)

Once you have selected the connector class you wish to create, the UI will populate with the connector's form. This will work for any standard connector and any customer connector you might have.

On the right-hand side, documentation will be available for the connector, export options will be available to create the connector via a REST call and any form errors will be displayed

![Create Connector form at a glance](<../.gitbook/assets/Screen Shot 2021-05-05 at 12.17.52 pm.png>)

Clicking on the "Show Description" button on any form item will bring up its documentation

![Documentation for the form item connector name](<../.gitbook/assets/Screen Shot 2021-05-05 at 12.18.40 pm.png>)

## Connector actions

You can manage running connectors from the **Explore** page found in the navigation menu under the **Connect** menu item.

### Source + Sink actions

![Actions available for sources + sinks](<../.gitbook/assets/Screen Shot 2021-05-05 at 12.21.56 pm (1).png>)

From within the source or sink table row actions you can: pause, restart or delete a connector and view/edit its config.

#### Editing config

{% hint style="info" %}
All sensitive config values will appear as redacted and do not get transferred in plaintext over the wire when editing config in kPow.
{% endhint %}

Clicking the **View Config** item in the connector actions menu will bring up the edit config form. If you do not have `CONNECT_EDIT` permissions, this form will be read only.

![Editing connect config](<../.gitbook/assets/Screen Shot 2021-05-05 at 2.22.48 pm (1).png>)

### Task actions

From within the **Tasks** table within the **Connect Explore** page, you can restart individual connect tasks or view any stacktraces if the connect task is in an **ERROR** state

![Connect task actions available](<../.gitbook/assets/Screen Shot 2021-05-05 at 2.25.13 pm.png>)
