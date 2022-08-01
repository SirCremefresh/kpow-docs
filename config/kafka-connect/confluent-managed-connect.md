---
description: Integrate Confluent's Managed Connect with kPow
---

# Confluent Managed Connect

## Configuration

### Generate an API key

You will need the Confluent CLI tools [installed and configured](https://docs.confluent.io/confluent-cli/current/install.html) to generate an API key for Connect.

* Log in to your account:\
  `confluent login`
* Create an API key for the `cloud` resource:\
  `confluent api-key create --resource cloud`

### Environment ID + Cluster ID

Next, you will need to locate your Confluent Cloud Environment ID + Cluster ID.&#x20;

You can discover this via the CLI using:

`confluent environments list`\
\
Or you can log in to the Confluent Cloud dashboard, select your cluster and find the IDs in the URL bar:

![](<../../.gitbook/assets/Screen Shot 2022-06-28 at 10.14.59 am.png>)&#x20;

### Configure kPow

With your API key generated, configure kPow with the following environment variables:

```
CONNECT_REST_URL=https://api.confluent.cloud/connect/v1/environments/${ENVIRONMENT_ID}/clusters/${CLUSTER_ID}
CONNECT_AUTH=BASIC
CONNECT_BASIC_AUTH_USER=${API_KEY}
CONNECT_BASIC_AUTH_PASS=${API_SECRET}
```
