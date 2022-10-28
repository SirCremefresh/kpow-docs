---
description: Secure kPow with Simple Environment Variable Global Controls
---

# Simple Access Control

{% hint style="warning" %}
**Important:** Simple Access Control configuration is ignored if you configure [RBAC](role-based-access-control.md).
{% endhint %}

Each [**Action**](overview.md#user-actions) can be enabled by setting a corresponding environment variable on system startup.

```
ALLOW_TOPIC_INSPECT=true      # Allow users to read topic key and value data
ALLOW_TOPIC_PRODUCE=true      # Allow users to write new messages to topics
ALLOW_TOPIC_CREATE=true       # Allow users to create new topics
ALLOW_TOPIC_EDIT=true         # Allow users to edit topic configuration
ALLOW_TOPIC_DELETE=true       # Allow users to delete topics
ALLOW_TOPIC_TRUNCATE=true     # Allow users to delete messages
ALLOW_GROUP_EDIT=true         # Allow users to delete consumer groups and reset consumer offsets
ALLOW_BROKER_EDIT=true        # Allow users to edit broker configuration
ALLOW_ACL_EDIT=true           # Allow users to create and delete Kafka ACLs
ALLOW_SCHEMA_CREATE=true      # Allow users to create new schemas and subjects
ALLOW_SCHEMA_EDIT=true        # Allow users to edit schemas and subjects
ALLOW_CONNECT_CREATE=true     # Allow users to create new connectors
ALLOW_CONNECT_EDIT=true       # Allow users to edit, pause, stop, and restart connectors and tasks
```

Simply choose the **Action**, prepend with **ALLOW\_**  set the environment variable, and start kPow.
