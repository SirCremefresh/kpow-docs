# MSK

## **AWS IAM Integration**

kPow supports [IAM Access Control for AWS MSK](https://docs.aws.amazon.com/msk/latest/developerguide/iam-access-control.html).

Simply set your kPow connection fields appropriately, e.g.

```
SSL_TRUSTSTORE_LOCATION=<PATH_TO_TRUST_STORE_FILE>
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=AWS_MSK_IAM
SASL_JAAS_CONFIG=software.amazon.msk.auth.iam.IAMLoginModule required;
SASL_CLIENT_CALLBACK_HANDLER_CLASS=software.amazon.msk.auth.iam.IAMClientCallbackHandler
```

See the AWS documentation for more information, including JAAS config for named profiles.

### Example IAM Policy for kPow

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kafka-cluster:*"
            ],
            "Resource": "arn:aws:kafka:<REGION>:cluster/<CLUSTER-NAME>/<GUID>"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kafka-cluster:*Topic*",
                "kafka-cluster:WriteData",
                "kafka-cluster:ReadData"
            ],
            "Resource": "arn:aws:kafka:<REGION>:topic/<CLUSTER-NAME>/<GUID>/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kafka-cluster:AlterGroup",
                "kafka-cluster:DescribeGroup"
            ],
            "Resource": "arn:aws:<REGION>:group/<CLUSTER-NAME>/<GUID>/*"
        }
    ]
}
```

## MSK Serverless

To configure kPow to run on an MSK Serverless cluster, the following configuration is recommended: &#x20;

```
CLUSTER_ID=your-msk-serverless-arn
KAFKA_VARIANT=MSK_SERVERLESS
NUM_PARTITIONS=1
SECURITY_PROTOCOL=SASL_SSL
SASL_MECHANISM=AWS_MSK_IAM
SASL_JAAS_CONFIG=software.amazon.msk.auth.iam.IAMLoginModule required;
SASL_CLIENT_CALLBACK_HANDLER_CLASS=software.amazon.msk.auth.iam.IAMClientCallbackHandler
```

`KAFKA_VARIANT` will create kPow's internal topics with the constrained [topic configuration properties](https://docs.aws.amazon.com/msk/latest/developerguide/serverless-config.html) and [limitations](https://docs.aws.amazon.com/msk/latest/developerguide/limits.html).&#x20;

`CLUSTER_ID` needs to be set to something unique as MSK's desribeCluster does not return an ID.

It is also recommended to set the environment variable `NUM_PARTITIONS=1` to overcome MSK's limitation on maximum number of partitions (120).

### Limitations

The following functionality will be impacted due MSK's own limitations:

* kPow's internal audit log topic will only have a retention of 1 day
* Broker disk metrics are not available in MSK serverless

## MSK Connect

See the [MSK Connect](msk.md#msk-connect) article
