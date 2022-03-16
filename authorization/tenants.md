---
description: Restrict Access to Kafka Resources by User Role
---

# Multi-Tenancy

## Introduction

Multi-Tenancy allows you to configure kPow to restrict visibility of Kafka resources.

See the article [How to manage Kafka visibility with Multi-Tenancy](https://kpow.io/how-to/manage-kafka-visibility-with-multi-tenancy/) for an overview.

### **About Tenants**

A tenant restricts the set of Kafka resources that are accessible to a user role from all the resources available to kPow. A user role may be assigned multiple tenants.

When operating within a tenant a user can only see resources included by that tenant, they will also see a fully consistent synthetic cluster-view of their aggregated resources.

The overall user experience is simply of a restricted set of Kafka resources as if they were truly the only resources in the system.

{% hint style="info" %}
A user can only **create** resources valid to their tenant.
{% endhint %}

Tenant configuration is defined within your Role Based Access Configuration YAML file.

A tenant can:

* Include or exclude topics by name, prefix, or suffix, e.g. tx-topic, tx-top\*, \*-topic
* Include or exclude groups by name, prefix, or suffix, e.g. tx-group, tx-grou\*, \*-group
* Include or exclude full resources, e.g Kafka clusters, Schema registries, or Connect clusters
* Be assigned to one or many user roles

#### Inferred Resources

Most resources are evaluated atomically as included or excluded.

Where a group is included, any topics that group consumes from are automatically included. This is in order to keep the synthetic cluster-view consistent. These resources are called **inferred** resources.

#### Resource Evaluation

A tenant determines what resources are visible with the following logic:

* Initially, all resources are implicitly excluded.
* Explicitly included resources are added.
* Inferred resources are added.
* Exclusions are applied last.

### Multi-Tenancy Use Cases

The primary use for multi-tenancy is to provide different views of Kafka resources to different teams within your organisation.

Consider a kPow that is connected to three Kafka Clusters (Dev, UAT, Prod), each having 200 topics and 200 groups, two Connect installations and one Schema Registry. ****&#x20;

You can create tenants that:

* Contain Kafka resources connected to or within Dev and UAT (or any combination of clusters)
* Contain specific topics or groups. E.g `my-topic` or `my-grou*`
* Include or exclude Connect or Schema resource in their entirety
* Any combination of the above.

The secondary use is to exclude groups and topics of no interest to your organisation.

For example, kPow provides two default tenants when you have none specifically configured:&#x20;

* Global: All Kafka resources
* kPow Hidden: All Kafka resources with kPow internal groups and topics excluded

## Configuration

Within your [RBAC yaml configuration file](role-based-access-control.md) you can specify a top-level `tenants` key:

This configuration matches the **default tenants** that kPow provides if you have none configured.

```yaml
tenants:
  - name: "Global"
    description: "All configured Kafka resources."
    resources:
      - include:
          - [ "*" ]
    roles:
      - "*"
  - name: "kPow Hidden"
    description: "All configured Kafka resources except internal kPow resources and __consumer_offsets."
    resources:
      - include:
          - [ "*" ]    
      - exclude:
          - [ "cluster", "*", "topic", "oprtr*" ]
          - [ "cluster", "*", "topic", "__oprtr*" ]
          - [ "cluster", "*", "topic", "__consumer_offsets" ]
          - [ "cluster", "*", "group", "oprtr*" ]
    roles:
      - "*"
```

### Fields

Each tenant is configured with a name, description, resources, and roles.

### name

| Key  | Required | Type   | Description             |
| ---- | -------- | ------ | ----------------------- |
| name | Y        | String | The name of the tenant. |

The `name` field will be the assigned name of the tenant used within kPow's UI. It must be unique.

### description

| Key         | Required | Type   | Description                    |
| ----------- | -------- | ------ | ------------------------------ |
| description | N        | String | The description of the tenant. |

The optional `description` field will be used within kPow's UI as a description when switching tenants.&#x20;

### resources

| Key       | Required | Type | Description                                                      |
| --------- | -------- | ---- | ---------------------------------------------------------------- |
| resources | Y        | List | A list of resources either included or excluded for this tenant. |

The `resources` field defines which resources are either included or excluded for this tenant.

Each item in the list is a map of either `include: [resource...]` or `exclude: [resouce...]`&#x20;

Where the resource refers to the path of the object you wish to include/exclude.&#x20;

For example: `["cluster",  "*", "topic", "tx_*"]`refers to any topic matching `tx_*`for any Kafka cluster defined in kPow.

### roles

| Key   | Required | Type | Description                                |
| ----- | -------- | ---- | ------------------------------------------ |
| roles | Y        | List | The list of roles assigned to this tenant. |

The `roles` field describes which roles (specified by your [auth provider](../authentication/overview.md#kpow-and-user-authentication)) are assigned to this tenant.

For more details about resources refer to the [RBAC documentation](role-based-access-control.md#resources).&#x20;

## User Experience

kPow users with a single tenant are automatically entered into that tenant on session start.

kPow users with multiple tenants have the option of choosing and switching tenant:

![](../.gitbook/assets/kpow-select-tenant.png)

Once a tenant is selected the user the chooses a cluster (if multi-cluster is configured)

![](../.gitbook/assets/kpow-select-cluster.png)

A user can switch tenants at any time by selecting the top-left user context menu

![](<../.gitbook/assets/kpow-switch-tenant (1).png>)

Once a tenant is selected the user is presented an internally consistent view of a synthetic set of Kafka resources that matches the tenant exactly.

Here is an example of the Cluster view in two tenants in our demo environment.

Each tenant provides a different synthetic view of the Kafka resources configured with kPow.

### **Global Tenant**

This tenant has 230 topics, 3.9GB replica disk and is receiving 762 writes/s

![](../.gitbook/assets/kpow-demo-tenant-1.png)

### Transaction Tenant

This tenant has 200 topics, 86.8MB replica disk and is receiving 1.75 writes/s.

It looks strikingly different because `tx-*` topics are generated event topics in our demo environment.

![](../.gitbook/assets/kpow-demo-tenant-2.png)

