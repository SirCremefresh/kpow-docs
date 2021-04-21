---
description: Configuration to run kPow secured with Kafka ACLs
---

# Minimum ACL Permissions

{% hint style="info" %}
You can skip this page if you do not have Kafka ACLS enabled in your cluster/s
{% endhint %}

### Minimum Kafka ACL Permissions

kPow checks for the following internal topics in your **primary cluster** \(the first bootstrap in your configuration\) on startup and will attempt to create them if required:

```text
__oprtr_metric_pt1m
__oprtr_snapshot_state
__oprtr_audit_log
oprtr.compute.metrics.v2-oprtr_metric_v2_pt1m-changelog
oprtr.compute.snapshots.v2-oprtr_snapshot_materialized_v2-repartition
```

You can manually create these topics if you prefer, each with a replication factor of **3** and **12** partitions. 

Once started, kPow creates two internal streaming compute applications:

```text
oprtr.compute.metrics.v2
oprtr.compute.snapshots.v2
```

See [this guide](https://docs.confluent.io/platform/current/streams/developer-guide/security.html) to understand the importance of creating the internal topics with the right configuration.

At a minimum, kPow must be able to read and write to and from these internal topics, must be able to read as those groups, and must have permissions to describe clusters, topics, configuration, and groups.

A simple set of Kafka ACL that allows kPow to operate provides **ALLOW** on the following:

| Kafka Resource | Kafka ACL | Detail |
| :--- | :--- | :--- |
| Cluster | Describe | `*` |
| Cluster | DescribeConfigs | `*` |
| Cluster | Create | `* (if not manually creating kpow topics)` |
| Topic | Describe | `*` |
| Topic | DescribeConfigs | `*` |
| Topic | Read | `* or kpow topics only` |
| Topic | Write | `* or kpow topics only` |
| Group | Describe | `*` |
| Group | Read | `* or kpow groups only` |

kPow **does not read from or write to topics other than internal ones** as a part of normal operation.

### Feature Specific ACLS

The following ACLS are optional and only required if you intend to permit the associated kPow action.

See [User Authorization](../authorization/overview.md#user-actions) for a description of kPow User Actions and Controls.

| Kafka Resource | Kafka ACL | Required for User Action |
| :--- | :--- | :--- |
| Cluster | AlterConfigs | `BROKER_EDIT` |
| Cluster | Create | `TOPIC_CREATE` |
| Topic | AlterConfigs | `TOPIC_EDIT` |
| Topic | Create | `TOPIC_CREATE` |
| Topic | Delete | `TOPIC_DELETE` |
| Topic | Read | `TOPIC_INSPECT` |
| Topic | Write | `TOPIC_PRODUCE` |
| Group | Read / Delete | `GROUP_EDIT` |

### Configuring Kafka ACLS

Kafka ACLs can be set with the kafka-acls.sh script provided by Apache Kafka.

An example command to add the DescribeConfigs Topic permission is:

```text
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 \
  --command-config client.conf 
  --allow-principal User:kpow \
  --operation DescribeConfigs \
  --topic '*'
  --add \
  
Adding ACLs for resource `ResourcePattern(resourceType=TOPIC, name=*, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=DESCRIBE_CONFIGS, permissionType=ALLOW)
```

The simple set of ACLS described above for basic operation of kPow can be listed like so:

```text
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config command.conf --list

Current ACLs for resource `ResourcePattern(resourceType=CLUSTER, name=kafka-cluster, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=CREATE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE_CONFIGS, permissionType=ALLOW)

Current ACLs for resource `ResourcePattern(resourceType=TOPIC, name=*, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=WRITE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE_CONFIGS, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=READ, permissionType=ALLOW)

Current ACLs for resource `ResourcePattern(resourceType=GROUP, name=*, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=READ, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)
```

