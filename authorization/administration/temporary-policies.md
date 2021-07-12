---
description: Manage Temporary Access to Kafka Resources with kPow
---

# Temporary Policies

Temporary Policies allow an admin to create temporary RBAC policies.

For example a Temporary Policy may grant `GROUP_EDIT` on a specific consumer group for a specific cluster for 30 minutes to a specific user role. 

Setting temporary policies is a feature available to [kPow Admins](./#administrators).

**Note**: an admin cannot assign temporary policies above their own permissions. For example, if creating a temporary policy for `GROUP_EDIT` , the admin must also be allowed to invoke `GROUP_EDIT` actions.

### Adding a Temporary Policy

From within the **Settings** page an administrator can navigate to the **Temporary Policies** tab.

![](../../.gitbook/assets/screen-shot-2021-06-23-at-2.26.08-pm.png)

### Manage Temporary Policies

From within the **Settings** page an administrator can navigate to the **Temporary Policies** tab.

![](../../.gitbook/assets/screen-shot-2021-06-11-at-11.05.12-am.png)

You can view all current temporary policies and remove temporary policies before they expire.

### Notifications

You can configure the [Slack Integration](../../features/slack-integration.md) to be notified when a new temporary policy has been made. 

All temporary policies are persisted to the [Audit Log](../../features/data-governance.md).

