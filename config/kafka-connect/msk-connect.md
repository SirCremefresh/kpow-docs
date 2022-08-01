---
description: Integrate kPow with MSK connectors
---

# MSK Connect

## Example IAM Policy

Configure kPow with an IAM policy similar to the one below:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "KafkaConnect",
      "Effect": "Allow",
      "Action": [
        "kafkaconnect:DeleteConnector",
        "kafkaconnect:ListConnectors",
        "kafkaconnect:ListCustomPlugins",
        "kafkaconnect:ListWorkerConfigurations"
      ],
      "Resource": "arn:${Partition}:kafkaconnect:${Region}:${Account}:*"
    },
    {
      "Sid": "Connector",
      "Effect": "Allow",
      "Action": [
        "kafkaconnect:DescribeConnector"
      ],
      "Resource": "arn:${Partition}:kafkaconnect:${Region}:${Account}:connector/*/*"
    },
    {
      "Sid": "CustomPlugin",
      "Effect": "Allow",
      "Action": [
        "kafkaconnect:DescribeCustomPlugin"
      ],
      "Resource": "arn:${Partition}:kafkaconnect:${Region}:${Account}:custom-plugin/*/*"
    },
    {
      "Sid": "WorkerConfiguration",
      "Effect": "Allow",
      "Action": [
        "kafkaconnect:DescribeWorkerConfiguration"
      ],
      "Resource": "arn:${Partition}:kafkaconnect:${Region}:${Account}:worker-configuration/*/*"
    }
  ]
}
```

You can learn more about Kafka Connect IAM actions and resources at the [official Amazon documentation](https://docs.aws.amazon.com/service-authorization/latest/reference/list\_amazonmanagedstreamingforkafkaconnect.html).

## kPow Configuration

Specify the AWS region your MSK connectors/cluster belong to:

```
CONNECT_AWS_REGION=us-east-1
```
