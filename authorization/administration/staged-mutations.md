---
description: Simple Workflow for Kafka Configuration Changes
---

# Staged Mutations

Staged mutations allow for an approval step on specific mutation actions. Staged mutations are configured through [Role Based Access Control](../role-based-access-control.md).

For example, a regular kPow user requests to create a topic and an administrator approves or denies this request. Once approved, the topic will be created on the Kafka cluster.

```yaml
admin_roles:
  - kafka-admins

policies:
  -
    actions:
      - TOPIC_CREATE
    effect: Allow
    resource:
      - "*"
    role: "kafka-admins"
  - actions:
      - TOPIC_CREATE
    effect: Stage
    resource:
      - "*"
    role: "kafka-users"
```

The above RBAC yaml describes how you would configure kPow for the scenario above. 

**Note**: the admin approving the staged mutation must also be allowed to invoke `TOPIC_CREATE` mutations for the resource being requested.

### Viewing mutation requests

From within the **Settings** page an administrator can navigate to the **Staged Mutations** tab.

![](<../../.gitbook/assets/Screen Shot 2021-06-11 at 10.42.57 am.png>)

From within the UI, an administrator can either approve or deny the request. 

After the mutation has been approved or denied, you can see the full history within the **Audit Log**

![](<../../.gitbook/assets/Screen Shot 2021-06-11 at 10.44.30 am.png>)

### Notifications

You can configure the [Slack integration](../../features/slack-integration.md) to be notified when a new mutation request has been made.
