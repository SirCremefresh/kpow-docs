---
description: A reference of all prometheus metric
---

# Metrics Glossary

| Metric Name | Domain | Description |  |
| :--- | :--- | :--- | :--- |
| group\_offset\_delta | cluster | The total delta of offsets of a group \(consumed msgs/s\) |  |
| broker\_end\_delta | cluster | The total delta of end offsets of a broker \(produced msgs/s\) |  |
| topic\_offset\_delta | cluster | The total delta of all assignment offsets reading from a topic \(consumed msgs/s\) |  |
| broker\_offset\_lag | cluster | The total lag of all assignments reading from a broker |  |
| host\_offset\_delta | cluster | The total delta of all group member offsets served by a host \(consumed msgs/s\) |  |
| group\_state | cluster | The state of the consumer group, where the value is the ordinal of org.apache.kafka.common.ConsumerGroupState |  |
| topic\_offset\_lag | cluster | The total lag of all assignments reading from a topic |  |
| topic\_count | cluster | The number of topics in the Kafka cluster |  |
| topic\_end\_delta | cluster | The total delta of end offsets of a topic \(produced msgs/s\) |  |
| group\_count | cluster | The number of consumer groups in the Kafka cluster |  |
| topic\_bytes\_disk | cluster | The disk size in bytes of a topic |  |
| broker\_offset\_delta | cluster | The total delta of all assignment offsets reading from a broker \(consumed msgs/s\) |  |
| broker\_start\_delta | cluster | The total delta of start offsets of a broker \(deleted msgs/s\) |  |
| broker\_count | cluster | The number of brokers in the Kafka cluster |  |
| topic\_start\_delta | cluster | The total delta of start offsets of a topic \(deleted msgs/s\) |  |
| group\_offset\_lag | cluster | The total lag of all assignments of a group |  |
| host\_offset\_lag | cluster | The total lag of all group members served by a host |  |
| broker\_bytes\_disk | cluster | The disk size in bytes of a broker |  |
| connect\_task\_running\_total | connect | The aggregate number of connector tasks running |  |
| connect\_connector\_paused\_total | connect | The aggregate number of paused connectors |  |
| connect\_task\_total | connect | The total number of connector tasks |  |
| connect\_task\_failed\_total | connect | The aggregate number of connector tasks failed |  |
| connect\_connector\_total | connect | The total number of connectors |  |
| connect\_task\_unassigned\_total | connect | The aggregate number of connector tasks unassigned |  |
| connect\_connector\_task\_total | connect | The total number of tasks a connector has |  |
| connect\_connector\_task\_paused\_total | connect | The total number of paused tasks a connector has |  |
| connect\_connector\_failed\_total | connect | The aggregate number of failed connectors |  |
| connect\_connector\_task\_failed\_total | connect | The total number of failed tasks a connector has |  |
| connect\_connector\_unassigned\_total | connect | The aggregate number of unassigned connectors |  |
| connect\_task\_paused\_total | connect | The aggregate number of connector tasks paused |  |
| connect\_connector\_running\_total | connect | The aggregate number of running connectors |  |
| connect\_connector\_task\_running\_total | connect | The total number of running tasks a connector has |  |
| connect\_connector\_task\_unassigned\_total | connect | The total number of unassigned tasks a connector has |  |
| partition\_end | offset | The end offset of a topic partition |  |
| topic\_end\_sum | offset | The sum of all partition end offsets of a topic |  |
| partition\_start | offset | The start offset of a topic partition |  |
| capture\_schema\_telemetry | operatr |  |  |
| produce\_topic | operatr |  |  |
| capture\_connect\_telemetry | operatr |  |  |
| execute\_kafka\_subject | operatr |  |  |
| jvm\_memory\_heap\_used | operatr |  |  |
| execute\_kafka\_group-offset | operatr |  |  |
| query\_snapshots | operatr |  |  |
| execute\_kafka\_cluster | operatr |  |  |
| execute\_kafka\_topic-offset | operatr |  |  |
| inspect\_topic | operatr |  |  |
| jvm\_memory\_heap\_max | operatr |  |  |
| capture\_kafka\_telemetry | operatr |  |  |
| jvm\_memory\_heap\_committed | operatr |  |  |
| jvm\_memory\_non-heap\_committed | operatr |  |  |
| execute\_kafka\_group | operatr |  |  |
| jvm\_memory\_non-heap\_used | operatr |  |  |
| capture\_kafka\_configuration | operatr |  |  |
| execute\_kafka\_schema | operatr |  |  |
| jvm\_memory\_non-heap\_max | operatr |  |  |
| query\_metrics | operatr |  |  |
| execute\_kafka\_broker-config | operatr |  |  |
| execute\_kafka\_replica | operatr |  |  |
| execute\_kafka\_topic-config | operatr |  |  |
| execute\_kafka\_broker | operatr |  |  |
| registry\_subject\_count | schema | The number of subjects in the schema registry |  |

