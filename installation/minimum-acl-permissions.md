---
description: Configuration to run kPow secured with Kafka ACLs
---

# Minimum ACL Permissions

{% hint style="info" %}
You can skip this page if you do not have Kafka ACLs enabled in your cluster/s
{% endhint %}

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

A **basic set** of Kafka ACLs that allows kPow to operate provides **ALLOW** on the following:

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

{% hint style="info" %}
Creating ACLs on a cluster with no existing ACL configuration can cause issues. 

Consult your cluster provider documentation first.

For example the [**Amazon MSK ACL Guide**](https://docs.aws.amazon.com/msk/latest/developerguide/msk-acls.html) ****warns not to set CLUSTER level ACLs and describes how to restrict access to topics while still allowing inter-broker replication.
{% endhint %}

Create a file containing client configuration for a user who has permissions to create ACLs.

```text
security.protocol=SASL_PLAINTEXT
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="admin" password="admin-secret";
```

The following commands use the kafka-acls.sh script provided by Apache Kafka to create the **basic set** of ACLs described above that allows kPow to operate.

```text
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --cluster '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation DescribeConfigs  --cluster '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Create --cluster '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Write --topic '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Read --topic '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --topic '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation DescribeConfigs --topic '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --group '*'
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Read --group '*'
```

That set of ACLs can then be listed using kafka-acls.sh.

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

