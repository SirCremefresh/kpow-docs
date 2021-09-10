---
description: Integrate the kPow Audit Log and Slack
---

# Slack Integration

kPow can send [**Audit Log**](data-governance.md) records to your Slack, all you need to do is configure a webhook.

![](../.gitbook/assets/snippet-slack.png)

## Configuration

1. Add an [**Incoming Webhooks**](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks) integration to your Slack.
2. Select a channel and click the "Add Incoming WebHooks integration" button
3. Copy the "Webhook URL" value from the "Setup Instructions" form
4. Set the environment variable **`SLACK_WEBHOOK_URL`** with the value from the previous step.
5. Restart kPow, now audit items are posted to your slack!

### Verbosity

You can configure the verbosity with the `SLACK_WEBHOOK_VERBOSITY` environment variable. Options are:

* `MUTATIONS` \(default\) - only mutations will be sent via the webhook
* `QUERIES` - only data inspect queries will be send via the webhook
* `ALL` - both mutations and queries will be sent via the webhook

