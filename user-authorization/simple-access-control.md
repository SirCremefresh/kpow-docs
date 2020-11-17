---
description: Secure kPow with Simple Environment Variable Global Controls
---

# Simple Access Control

{% hint style="warning" %}
**Important:** Simple Access Control configuration is ignored if you configure [RBAC](role-based-access-control.md).
{% endhint %}

Each [**Action**](overview.md#user-actions) can be enabled by setting a corresponding environment variable on system startup.

```text
## Allow users to create new topics 
ALLOW_TOPIC_CREATE=true
```

Simply choose the **Action**, prepend with **ALLOW\_**  set the environment variable, and start kPow.

