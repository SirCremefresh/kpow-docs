---
description: A reference of all Prometheus metrics
---

# Metrics Glossary

| Metric | Type | Domain | Description |  |
| :--- | :--- | :--- | :--- | :--- |
| group\_offset\_delta | histogram | cluster | The total delta of offsets of a group \(consumed msgs/s\) |  |
| broker\_end\_delta | histogram | cluster | The total delta of end offsets of a broker \(produced msgs/s\) |  |
| cluster\_controller | gauge | cluster | The ID of the broker that is acting as the controller |  |
| topic\_offset\_delta | histogram | cluster | The total delta of all assignment offsets reading from a topic \(consumed msgs/s\) |  |
| broker\_offset\_lag | histogram | cluster | The total lag of all assignments reading from a broker |  |
| host\_offset\_delta | histogram | cluster | The total delta of all group member offsets served by a host \(consumed msgs/s\) |  |
| group\_state | gauge | cluster | The state of the consumer group, where the value is the ordinal of org.apache.kafka.common.ConsumerGroupState |  |
| broker\_urp | gauge | cluster | Partitions that are not fully replicated within the cluster. The value of the gauge is the broker id |  |
| topic\_offset\_lag | histogram | cluster | The total lag of all assignments reading from a topic |  |
| topic\_count | gauge | cluster | The number of topics in the Kafka cluster |  |
| streams\_client\_state | gauge | cluster | The state of the streams instance, where the value is the ordinal of org.apache.kafka.streams.KafkaStreams.State |  |
| topic\_end\_delta | histogram | cluster | The total delta of end offsets of a topic \(produced msgs/s\) |  |
| group\_count | gauge | cluster | The number of consumer groups in the Kafka cluster |  |
| topic\_bytes\_disk | gauge | cluster | The disk size in bytes of a topic |  |
| broker\_offset\_delta | histogram | cluster | The total delta of all assignment offsets reading from a broker \(consumed msgs/s\) |  |
| broker\_start\_delta | histogram | cluster | The total delta of start offsets of a broker \(deleted msgs/s\) |  |
| broker\_count | gauge | cluster | The number of brokers in the Kafka cluster |  |
| streams\_state | gauge | cluster | The aggregated streams state of the group, where the value is the ordinal of org.apache.kafka.streams.KafkaStreams.State |  |
| acl\_count | gauge | cluster | The number of ACLs in the Kafka cluster |  |
| topic\_start\_delta | histogram | cluster | The total delta of start offsets of a topic \(deleted msgs/s\) |  |
| group\_offset\_lag | histogram | cluster | The total lag of all assignments of a group |  |
| host\_offset\_lag | histogram | cluster | The total lag of all group members served by a host |  |
| broker\_bytes\_disk | gauge | cluster | The disk size in bytes of a broker |  |
| connect\_task\_running\_total | gauge | connect | The aggregate number of connector tasks running |  |
| connect\_connector\_paused\_total | gauge | connect | The aggregate number of paused connectors |  |
| connect\_task\_total | gauge | connect | The total number of connector tasks |  |
| connect\_task\_failed\_total | gauge | connect | The aggregate number of connector tasks failed |  |
| connect\_connector\_total | gauge | connect | The total number of connectors |  |
| connect\_task\_unassigned\_total | gauge | connect | The aggregate number of connector tasks unassigned |  |
| connect\_connector\_task\_total | gauge | connect | The total number of tasks a connector has |  |
| connect\_connector\_task\_paused\_total | gauge | connect | The total number of paused tasks a connector has |  |
| connect\_connector\_task\_state | gauge | connect | The state of the connector's task |  |
| connect\_connector\_failed\_total | gauge | connect | The aggregate number of failed connectors |  |
| connect\_connector\_task\_failed\_total | gauge | connect | The total number of failed tasks a connector has |  |
| connect\_connector\_unassigned\_total | gauge | connect | The aggregate number of unassigned connectors |  |
| connect\_task\_paused\_total | gauge | connect | The aggregate number of connector tasks paused |  |
| connect\_connector\_state | gauge | connect | The state of the connector |  |
| connect\_connector\_running\_total | gauge | connect | The aggregate number of running connectors |  |
| connect\_connector\_task\_running\_total | gauge | connect | The total number of running tasks a connector has |  |
| connect\_connector\_task\_unassigned\_total | gauge | connect | The total number of unassigned tasks a connector has |  |
| partition\_end | gauge | offset | The end offset of a topic partition |  |
| topic\_end\_sum | gauge | offset | The sum of all partition end offsets of a topic |  |
| partition\_start | gauge | offset | The start offset of a topic partition |  |
| capture\_schema\_telemetry | timer | operatr |  |  |
| produce\_topic | timer | operatr |  |  |
| capture\_connect\_telemetry | timer | operatr |  |  |
| execute\_kafka\_subject | timer | operatr |  |  |
| jvm\_memory\_heap\_used | gauge | operatr |  |  |
| execute\_kafka\_group-offset | timer | operatr |  |  |
| query\_snapshots | timer | operatr |  |  |
| execute\_kafka\_cluster | timer | operatr |  |  |
| execute\_kafka\_topic-offset | timer | operatr |  |  |
| inspect\_topic | timer | operatr |  |  |
| jvm\_memory\_heap\_max | gauge | operatr |  |  |
| capture\_kafka\_telemetry | timer | operatr |  |  |
| jvm\_memory\_heap\_committed | gauge | operatr |  |  |
| jvm\_memory\_non-heap\_committed | gauge | operatr |  |  |
| execute\_kafka\_group | timer | operatr |  |  |
| jvm\_memory\_non-heap\_used | gauge | operatr |  |  |
| capture\_kafka\_configuration | timer | operatr |  |  |
| execute\_kafka\_acl-config | timer | operatr |  |  |
| execute\_kafka\_schema | timer | operatr |  |  |
| jvm\_memory\_non-heap\_max | gauge | operatr |  |  |
| query\_metrics | timer | operatr |  |  |
| execute\_kafka\_broker-config | timer | operatr |  |  |
| execute\_kafka\_replica | timer | operatr |  |  |
| execute\_kafka\_topic-config | timer | operatr |  |  |
| execute\_kafka\_broker | timer | operatr |  |  |
| registry\_subject\_count | gauge | schema | The number of subjects in the schema registry |  |
| registry\_subject\_version | gauge | schema | The schema version of the subject |  |

