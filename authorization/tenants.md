---
description: Configure multi-tenancy for your kPow instance
---

# Tenants

{% hint style="info" %}
Multi-tenancy is currently in feature preview. Contact [support@operatr.io](mailto:support@operatr.io) to get access! 
{% endhint %}

## Introduction

Tenancy represents the top level in your hierarchy. You can define the resources available to each tenant, such as Kafka clusters, topics or groups.

For example, there might be three different teams sharing the same Kafka cluster. Each team might only want to view metrics+resources that relate to their Kafka topics + consumer groups. 

You can assign a tenant to multiple roles that come in from your specified [authentication provider](../authentication/overview.md#kpow-and-user-authentication). 

## Configuration

Within your [RBAC yaml configuration file](role-based-access-control.md) you can specify a top-level `tenants` key:

```yaml
tenants:
  - name: "Connect"
    description: "Access to Connect Clusters + Connect Resources"
    roles:
      - connect-admins
    resources:
      - include: ["connect",  "*"]
      - exclude: ["cluster", "*", "topic", "connect_pii_topic"]
      - include: ["cluster", "*", "group", "connect*"]
      - include: ["cluster", "*", "topic", "connect*"]
      - include: ["cluster", "*", "topic", "kpow-connect*"]
```

In this particular example we have create a tenant named Connect that has access to all Kafka Connect clusters, any topic matching `connect*` or `kpow-connect*`, and any consumer group matching `connect*`. The topic `connect_pii_topic` will be excluded from kPow's UI/metrics calculation. 

Only users who has been assigned the role `connect-admins` will be 

### name

| Key | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Y | String | The name of the tenant. |

The `name` field will be the assigned name of the tenant used within kPow's UI. It must be unique.

### Description

| Key | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| description | N | String | The description of the tenant. |

The optional `description` field will be used within kPow's UI as a description when switching tenants. 

###   roles

| Key | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| roles | Y | List | The list of roles assigned to this tenant. |

The `roles` field describes which roles \(specified from your [authentication provider](../authentication/overview.md#kpow-and-user-authentication)\) are assigned to this tenant.

### resources

| Key | Required | Type | Description |
| :--- | :--- | :--- | :--- |
| resources | Y | List | A list of resources either included or excluded for this tenant. |

The `resources` field defines which resources are either included or excluded for this tenant.

Each item in the list is a map of either `include: [resource...]` or `exclude: [resouce... ]` 

Where the resource refers to the path of the object you wish to include/exclude. 

For example: `["cluster",  "*", "topic", "tx_*"]`refers to any topic matching `tx_*`for any Kafka cluster defined in kPow.

For more details about resources refer to the [RBAC documentation](role-based-access-control.md#resources). 

