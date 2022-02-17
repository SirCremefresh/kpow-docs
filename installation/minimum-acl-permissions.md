---
description: Configuration to run kPow secured with Kafka ACLs
---

# Minimum ACL Permissions

Kafka has the ability to restrict access to objects and operations within a cluster through the use of [Kafka Access Control Lists](https://kafka.apache.org/documentation/#security\_authz) (ACLs). This is different to kPow's own [Role Based Access Controls](../authorization/role-based-access-control.md).

{% hint style="info" %}
You can skip this page if you do not have Kafka ACLs enabled in your cluster/s
{% endhint %}

When your cluster is secured with Kafka ACLs the Kafka user identified by the cluster connection credentials provided to kPow will need to have a minimum level of permissions for kPow to operate.

### kPow Required Permissions

kPow needs the ability to read and write internal topics and read internal groups.

kPow checks for the following internal topics in your **primary cluster** (the first bootstrap in your configuration) on startup and will attempt to create them if required:

```
__oprtr_metric_pt1m
__oprtr_snapshot_state
__oprtr_audit_log
oprtr.compute.metrics.v2-oprtr_metric_v2_pt1m-changelog
oprtr.compute.snapshots.v2-oprtr_snaphot_state_v2-changelog
```

You can manually create these topics if you prefer, see [Create kPow Topics](minimum-acl-permissions.md#create-kpow-topics).

Once started, kPow creates two internal streaming compute applications:

```
oprtr.compute.metrics.v2
oprtr.compute.snapshots.v2
```

At a minimum, kPow must be able to read and write to and from these internal topics, must be able to read as those groups, and must have permissions to describe clusters, topics, configuration, and groups.

A **basic set** of Kafka ACLs that allows kPow to operate provides **ALLOW** on the following:

| Kafka Resource | Kafka ACL       | Detail                                     |
| -------------- | --------------- | ------------------------------------------ |
| Cluster        | Describe        | `*`                                        |
| Cluster        | DescribeConfigs | `*`                                        |
| Cluster        | Create          | `* (if not manually creating kpow topics)` |
| Topic          | Describe        | `*`                                        |
| Topic          | DescribeConfigs | `*`                                        |
| Topic          | Read            | `* or kpow topics only`                    |
| Topic          | Write           | `* or kpow topics only`                    |
| Group          | Describe        | `*`                                        |
| Group          | Read            | `* or kpow groups only`                    |

kPow **does not read from or write to topics other than internal ones** as a part of normal operation.

### Feature Specific ACLS

The following ACLS are optional and only required if you intend to permit the associated kPow action.

See [User Authorization](../authorization/overview.md#user-actions) for a description of kPow User Actions and Controls.

| Kafka Resource | Kafka ACL     | Required for User Action |
| -------------- | ------------- | ------------------------ |
| Cluster        | Alter         | `ACL_EDIT`               |
| Cluster        | AlterConfigs  | `BROKER_EDIT`            |
| Cluster        | Create        | `TOPIC_CREATE`           |
| Topic          | AlterConfigs  | `TOPIC_EDIT`             |
| Topic          | Create        | `TOPIC_CREATE`           |
| Topic          | Delete        | `TOPIC_DELETE`           |
| Topic          | Read          | `TOPIC_INSPECT`          |
| Topic          | Write         | `TOPIC_PRODUCE`          |
| Group          | Read / Delete | `GROUP_EDIT`             |

### Configuring Kafka ACLS

{% hint style="info" %}
Creating ACLs on a cluster with no existing ACL configuration can cause issues.&#x20;

Consult your cluster provider documentation first.

For example the [**Amazon MSK ACL Guide**](https://docs.aws.amazon.com/msk/latest/developerguide/msk-acls.html) **** describes extra ACLs required to allow inter-broker replication, and suggests not to set CLUSTER level ACLs.
{% endhint %}

Create a file containing client configuration for a user who has permissions to create ACLs.

```
security.protocol=SASL_PLAINTEXT
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="admin" password="admin-secret";
```

The following commands use the kafka-acls.sh script provided by Apache Kafka to create the **basic set** of ACLs described above that allows kPow to operate plus the ALTER CLUSTER ACL that allows kPow to create and delete ACLs.

```
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --cluster '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation DescribeConfigs  --cluster '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Create --cluster '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Write --topic '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Read --topic '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --topic '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation DescribeConfigs --topic '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Describe --group '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Read --group '*'
./kafka-acls.sh --bootstrap-server 127.0.0.1:9092 --command-config client.conf --add --allow-principal User:kpow --operation Alter --cluster '*'
```

That set of ACLs can then be listed using kafka-acls.sh.

```
./kafka-acls.sh -bootstrap-server 127.0.0.1:9092 --command-config client.conf --list

Current ACLs for resource `ResourcePattern(resourceType=GROUP, name=*, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=READ, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)

Current ACLs for resource `ResourcePattern(resourceType=TOPIC, name=*, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=READ, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=WRITE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE_CONFIGS, permissionType=ALLOW)

Current ACLs for resource `ResourcePattern(resourceType=CLUSTER, name=kafka-cluster, patternType=LITERAL)`:
 	(principal=User:kpow, host=*, operation=DESCRIBE_CONFIGS, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=DESCRIBE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=CREATE, permissionType=ALLOW)
	(principal=User:kpow, host=*, operation=ALTER, permissionType=ALLOW)
```

### Create kPow Topics

Using the same client configuration file as above, the following script correctly creates the required internal kPow topics. You can run this script and create these topics on the **primary cluster** in which you expect kPow to keep data.

```
./kafka-topics.sh --create \
         --bootstrap-server 127.0.0.1:9092 \
         --command-config client.conf \
         --topic __oprtr_audit_log \
         --config compression.type=gzip \
         --config segment.bytes=104857600 \
         --config retention.ms=-1
./kafka-topics.sh --create \
         --bootstrap-server 127.0.0.1:9092 \
         --command-config client.conf \
         --topic __oprtr_metric_pt1m \
         --config compression.type=gzip \
         --config segment.bytes=104857600 \
         --config retention.ms=86400000 \
         --config segment.ms=43200000
./kafka-topics.sh --create \
         --bootstrap-server 127.0.0.1:9092 \
         --command-config client.conf \
         --topic __oprtr_snapshot_state \
         --config compression.type=gzip \
         --config segment.bytes=104857600 \
         --config retention.ms=86400000 \
         --config message.timestamp.type=LogAppendTime \
         --config segment.ms=43200000
./kafka-topics.sh --create \
         --bootstrap-server 127.0.0.1:9092 \
         --command-config client.conf \
         --topic oprtr.compute.metrics.v2-oprtr_metric_v2_pt1m-changelog \
         --config cleanup.policy=compact,delete \
         --config segment.bytes=52428800 \
         --config retention.ms=5400000 \
         --config message.timestamp.type=CreateTime \
         --config segment.ms=1800000
./kafka-topics.sh --create \
         --bootstrap-server 127.0.0.1:9092 \
         --command-config client.conf \
         --topic oprtr.compute.snapshots.v2-oprtr_snaphot_state_v2-changelog \
         --config cleanup.policy=compact,delete \
         --config segment.bytes=26214400 \
         --config retention.ms=604800000 \
         --config message.timestamp.type=CreateTime \
         --config segment.ms=604800000
```
