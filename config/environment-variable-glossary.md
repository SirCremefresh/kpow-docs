---
description: A glossary of all configuration options available to kPow
---

# Environment Variable Glossary

## Kafka

* See [Kafka Cluster](kafka-cluster.md) for Kafka environment variable reference
* See [Kafka Connect](kafka-connect.md) for Connect environment variable reference
* See [Schema Registry](schema-registry.md) for Schema registry environment variable reference

## Web Server 

### PORT

| Env Var | Type | Default | Description               |
| ------- | ---- | ------- | ------------------------- |
| PORT    | long | 3000    | The kPow web server port  |

**Note: **will serve HTTPS traffic if so configured.

### HTTP_FORWARDED

| Env Var        | Type | Default | Description                                      |
| -------------- | ---- | ------- | ------------------------------------------------ |
| HTTP_FORWARDED | bool | false   | Set when kPow is running behind a reverse proxy. |

**Note**: see [Deployment notes](../installation/deployment-notes.md) for reverse proxy examples. 

### ENABLE_GZIP

| Env Var     | Type | Default | Description                                                                    |
| ----------- | ---- | ------- | ------------------------------------------------------------------------------ |
| ENABLE_GZIP | bool | true    | Whether to enable gzip compression for kPow's static resources (JSON, CSS etc) |

### ENABLE_HTTPS

| Env Var      | Default | Type | Description                  |
| ------------ | ------- | ---- | ---------------------------- |
| ENABLE_HTTPS | false   | bool | Serve kPow content via HTTPS |

**Note: **see [HTTPS connections](../features/https-connections.md) for more details about configuration. 

### **HTTPS_SNI_HOST_CHECK**

| Env Var                  | Default | Type | Description                                                                              |
| ------------------------ | ------- | ---- | ---------------------------------------------------------------------------------------- |
| **HTTPS_SNI_HOST_CHECK** | false   | bool | When SSL configured, whether the certificate sent to the client matches the Host header. |

### **HTTPS_KEYSTORE_LOCATION**

| Env Var                     | Default | Type   | Description                 |
| --------------------------- | ------- | ------ | --------------------------- |
| **HTTPS_KEYSTORE_LOCATION** |         | string | eg: /ssl/https.keystore.jks |

### **HTTPS_KEYSTORE_TYPE**

| Env Var                 | Default | Type   |                              |
| ----------------------- | ------- | ------ | ---------------------------- |
| **HTTPS_KEYSTORE_TYPE** |         | string | Type of SSL Keystore, eg JKS |

### **HTTPS_KEYSTORE_PASSWORD**

| Env Var                     | Default | Type   | Description           |
| --------------------------- | ------- | ------ | --------------------- |
| **HTTPS_KEYSTORE_PASSWORD** |         | string | SSL Keystore password |

### **HTTPS_TRUSTSTORE_LOCATION**

| Env Var                       | Default | Type   | Description                   |
| ----------------------------- | ------- | ------ | ----------------------------- |
| **HTTPS_TRUSTSTORE_LOCATION** |         | string | eg, /ssl/https.truststore.jks |

### **HTTPS_TRUSTSTORE_TYPE**

| Env Var                   | Default | Type   | Description                         |
| ------------------------- | ------- | ------ | ----------------------------------- |
| **HTTPS_TRUSTSTORE_TYPE** |         | string | Type of SSL Truststore type, eg JKS |

### **HTTPS_TRUSTSTORE_PASSWORD**

| Env Var                       | Default | Type   | Description             |
| ----------------------------- | ------- | ------ | ----------------------- |
| **HTTPS_TRUSTSTORE_PASSWORD** |         | string | SSL Truststore password |

## Authentication

### AUTH_PROVIDER_TYPE

| Env Var                | Default | Type | Description                                                          |
| ---------------------- | ------- | ---- | -------------------------------------------------------------------- |
| **AUTH_PROVIDER_TYPE** |         | enum | The OPENID provider configured for SSO, eg: `github`, `jetty`,`okta` |

Note: see [User Authentication](../authentication/overview.md) for more details

### OKTA_ORGANISATION

| Env Var               | Default | Type   | Description                                     |
| --------------------- | ------- | ------ | ----------------------------------------------- |
| **OKTA_ORGANISATION** |         | string | The name of your Okta organisation, eg: my-corp |

### AUTH_LANDING_URI

| Env Var              | Default | Type   | Description                                                                                         |
| -------------------- | ------- | ------ | --------------------------------------------------------------------------------------------------- |
| **AUTH_LANDING_URI** |         | string | The absolute URL to redirect to after successful OKTA login. Eg: https://staging.operatr.z-corp.com |

### **OPENID_AUTH_URI**

| Env Var             | Default | Type   | Description                                                                                                                                                                        |
| ------------------- | ------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **OPENID_AUTH_URI** |         | string | <p>For GitHub: <a href="https://github.com/login/oauth/authorize">https://github.com/login/oauth/authorize</a></p><p>For GitHub enterprise: [Server URL]/login/oauth/authorize</p> |

### OPENID_API_URI

| Env Var            | Default | Type   | Description                                                                                                                                          |
| ------------------ | ------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **OPENID_API_URI** |         | string | <p>For GitHub:</p><p><a href="https://api.github.com/user">https://api.github.com/user</a></p><p>For GitHub enterprise: [Server URL]/api/v3/user</p> |

### OPENID_TOKEN_URI

| Env Var              | Default | Type   | Description                                                                                                                                                                                 |
| -------------------- | ------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **OPENID_TOKEN_URI** |         | string | <p>For GitHub: <a href="https://github.com/login/oauth/access_token">https://github.com/login/oauth/access_token</a></p><p>For GitHub enterprise: [Server URL]/login/oauth/access_token</p> |

### OPENID_CLIENT_ID

| Env Var              | Default | Type   | Description                                         |
| -------------------- | ------- | ------ | --------------------------------------------------- |
| **OPENID_CLIENT_ID** |         | string | The 'Client ID' found in your configured OpenID App |

### OPENID_CLIENT_SECRET

| Env Var                  | Default | Type   | Description                                             |
| ------------------------ | ------- | ------ | ------------------------------------------------------- |
| **OPENID_CLIENT_SECRET** |         | string | The 'Client Secret' found in your configured OpenID App |

### **SAML_RELYING_PARTY_IDENTIFIER**

| Env Var                           | Default | Type   | Description                |
| --------------------------------- | ------- | ------ | -------------------------- |
| **SAML_RELYING_PARTY_IDENTIFIER** |         | string | You Operatr Application ID |

### SAML_ACS_URL

| Env Var          | Default | Type   | Description                        |
| ---------------- | ------- | ------ | ---------------------------------- |
| **SAML_ACS_URL** |         | string | The Assertion Consumer Service URL |

### **SAML_METADATA_FILE**

| Env Var                | Default | Type   | Description                               |
| ---------------------- | ------- | ------ | ----------------------------------------- |
| **SAML_METADATA_FILE** |         | string | The SAML Metadata File from your provider |

### SAML_CERT

| Env Var       | Default | Type   | Description                 |
| ------------- | ------- | ------ | --------------------------- |
| **SAML_CERT** |         | string | SAML Certificate (Optional) |

### **SAML_SESSION_S**

| Env Var            | Default | Type | Description                                                       |
| ------------------ | ------- | ---- | ----------------------------------------------------------------- |
| **SAML_SESSION_S** | 3600    | long | The duration in seconds before re-authenticating SAML credentials |

### DEBUG_SAML

| Env Var        | Default | Type | Description                                   |
| -------------- | ------- | ---- | --------------------------------------------- |
| **DEBUG_SAML** | false   | bool | Enable SAML debug logging in application logs |

### **JETTY_AUTH_METHOD**

| Env Var               | Default | Type | Description                                                                                                                                                         |
| --------------------- | ------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **JETTY_AUTH_METHOD** | form    | enum | <p>Configure if using <a href="../authentication/overview.md#jetty-authentication">Jetty authentication</a></p><p>Either: <code>form</code>or<code>basic</code></p> |

## Authorization

### **RBAC_CONFIGURATION_FILE**

| Env Var                     | Default | Type   | Description                                                                 |
| --------------------------- | ------- | ------ | --------------------------------------------------------------------------- |
| **RBAC_CONFIGURATION_FILE** |         | string | The path to your Operatr RBAC Configuration (optional, expects SSO enabled) |

**Note: **see [Authorization](../authorization/role-based-access-control.md) for more details

## kPow

### **DATA_POLICY_CONFIGURATION_FILE**

| Env Var                            | Default | Type   | Description                                     |
| ---------------------------------- | ------- | ------ | ----------------------------------------------- |
| **DATA_POLICY_CONFIGURATION_FILE** |         | string | The path to your kPow Data Policy Configuration |

Note: see [Data Policies](../features/data-policies.md) for more information

### CONNECT_TIMEOUT_MS

| Env Var                | Default | Type | Description                                                                   |
| ---------------------- | ------- | ---- | ----------------------------------------------------------------------------- |
| **CONNECT_TIMEOUT_MS** | 5000    | long | The timeout value in ms for all HTTP requests made to a Kafka Connect cluster |

### CUSTOM_SERDES

| Env Var           | Default | Type   | Description                                                                                                |
| ----------------- | ------- | ------ | ---------------------------------------------------------------------------------------------------------- |
| **CUSTOM_SERDES** |         | string | eg: `io.operatr.SerdeOne,io.operatr.SerdeTwo`Comma separated names of custom serdes found on the classpath |

**Note**: see [Custom serdes](../features/data-inspect/serdes.md#custom-serdes) for more information

### DEFAULT_KEY_SERDES

| Env Var                | Default | Type   | Description                                                   |
| ---------------------- | ------- | ------ | ------------------------------------------------------------- |
| **DEFAULT_KEY_SERDES** |         | string | The default key serde to use when inspecting data, eg: `AVRO` |

### DEFAULT_VALUE_SERDES

| Env Var                  | Default | Type   | Description                                                   |
| ------------------------ | ------- | ------ | ------------------------------------------------------------- |
| **DEFAULT_VALUE_SERDES** |         | string | The default key value to use when inspecting data, eg: `JSON` |

### **AVAILABLE_KEY_SERDES**

| Env Var                  | Default | Type   | Description                                                                              |
| ------------------------ | ------- | ------ | ---------------------------------------------------------------------------------------- |
| **AVAILABLE_KEY_SERDES** |         | string | The list of key serdes to present when inspecting data, eg: `JSON,String,Transit / JSON` |

### **AVAILABLE_VALUE_SERDES**

| Env Var                    | Default | Type   | Description                                                                                   |
| -------------------------- | ------- | ------ | --------------------------------------------------------------------------------------------- |
| **AVAILABLE_VALUE_SERDES** |         | string | The list of key serdes to present when inspecting data, eg: `JSON,String,io.operatr.SerdeOne` |

### NUM_PARTITIONS

| Env Var            | Default | Type | Description                                                  |
| ------------------ | ------- | ---- | ------------------------------------------------------------ |
| **NUM_PARTITIONS** | 12      | long | The number of partitions for kPow's internal consumer groups |

### REPLICATION_FACTOR

| Env Var                | Default | Type | Description                                               |
| ---------------------- | ------- | ---- | --------------------------------------------------------- |
| **REPLICATION_FACTOR** | 3       | long | The replication factor of kPow's internal consumer groups |

### REQUEST_TIMEOUT_MS

| Env Var                | Default | Type | Description                                                         |
| ---------------------- | ------- | ---- | ------------------------------------------------------------------- |
| **REQUEST_TIMEOUT_MS** | 30000   | long | The request.timeout.ms settting for kPow's internal consumer groups |

### **MAX_PRODUCE_REQUEST_SIZE**

| Env Var                      | Default | Type | Description                                                        |
| ---------------------------- | ------- | ---- | ------------------------------------------------------------------ |
| **MAX_PRODUCE_REQUEST_SIZE** | 1000000 | long | The max.produce.request.size setting for kPow's internal producers |

### **PROMETHEUS_EGRESS**

| Env Var               | Default | Type | Description                                                |
| --------------------- | ------- | ---- | ---------------------------------------------------------- |
| **PROMETHEUS_EGRESS** | false   | bool | Enable Prometheus endpoints for metrics and offsets egress |

### **PROMETHEUS_LABEL_ENV**

| Env Var                  | Default | Type | Description                                                        |
| ------------------------ | ------- | ---- | ------------------------------------------------------------------ |
| **PROMETHEUS_LABEL_ENV** | true    | bool | Include your ENVIRONMENT_NAME as 'env' label on Prometheus metrics |

### SNAPSHOT_PARALLELISM

| Env Var                  | Default | Type | Description                                                                                                                                   |
| ------------------------ | ------- | ---- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **SNAPSHOT_PARALLELISM** | 3       | long | The level of parallelism configured for when kPow captures telemetry for snapshots. Increase OPEARTR internal parallelism for larger clusters |

### SNAPSHOT_DEBUG

| Env Var            | Default | Type | Description                                                |
| ------------------ | ------- | ---- | ---------------------------------------------------------- |
| **SNAPSHOT_DEBUG** | false   | bool | Add additional logging messages to help debug snapshotting |

### LIVE\_ MODE_ENABLED

| Env Var               | Default | Type | Description                             |
| --------------------- | ------- | ---- | --------------------------------------- |
| **LIVE_MODE_ENABLED** | true    | bool | Allow your users to switch to Live Mode |

**Note**: see [Live mode](../features/live-mode.md) for more details.

### **LIVE_MODE_PERIOD_MS**

| Env Var                 | Default | Type | Description                                             |
| ----------------------- | ------- | ---- | ------------------------------------------------------- |
| **LIVE_MODE_PERIOD_MS** | 60000   | long | Live Mode will prompt you to continue after this period |

### **LIVE_MODE_INTERVAL_MS**

| Env Var                   | Default | Type | Description                                    |
| ------------------------- | ------- | ---- | ---------------------------------------------- |
| **LIVE_MODE_INTERVAL_MS** | 3500    | long | The amount of time between Live Mode snapshots |

### **LIVE_MODE_MAX_CONCURRENT_USERS**

| Env Var                            | Default | Type | Description                                              |
| ---------------------------------- | ------- | ---- | -------------------------------------------------------- |
| **LIVE_MODE_MAX_CONCURRENT_USERS** | 2       | long | The maximum number of concurrent Live Mode user sessions |

### SAMPLER_TIMEOUT_MS

| Env Var                | Default | Type | Description                                     |
| ---------------------- | ------- | ---- | ----------------------------------------------- |
| **SAMPLER_TIMEOUT_MS** | 7000    | long | The end-to-end timeout for a data inspect query |

### SAMPLER_CONSUMER_THREADS

| Env Var                      | Default | Type | Description                                       |
| ---------------------------- | ------- | ---- | ------------------------------------------------- |
| **SAMPLER_CONSUMER_THREADS** | 6       | long | The level of parallelism for a data inspect query |

### **SLACK_WEBHOOK_URL**

| Env Var               | Default | Type   | Description                      |
| --------------------- | ------- | ------ | -------------------------------- |
| **SLACK_WEBHOOK_URL** |         | string | Send Audit Log messages to Slack |

### **SLACK_WEBHOOK_URL**

| **Env Var**                 | Default   | Type | Description                              |
| --------------------------- | --------- | ---- | ---------------------------------------- |
| **SLACK_WEBHOOK_VERBOSITY** | Mutations | enum | Possible values: All, Mutations, Queries |

### SHOW_SPLASH

| **Env Var**     | Default | Type | Description                           |
| --------------- | ------- | ---- | ------------------------------------- |
| **SHOW_SPLASH** | true    | bool | Turn off the initial page splash scre |

### **STREAMS_ERROR_STRATEGY**

| **Env Var**                | Default       | Type | Description                                                                                                                         |
| -------------------------- | ------------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **STREAMS_ERROR_STRATEGY** | LOG_EXCEPTION | enum | The strategy to use when kPow's internal Kafka Streams instance enters an ERROR state. Possible values: LOG_EXCEPTION, LOG_AND_EXIT |

### **STREAMS_TASK_TIMEOUT_MS**

| **Env Var**                 | Default | Type | Description                                                                                                                                                                                                 |
| --------------------------- | ------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **STREAMS_TASK_TIMEOUT_MS** | 300000  | long | Configures kPow's internal streams `task.timeout.ms` value. See: [KIP-572](https://cwiki.apache.org/confluence/display/KAFKA/KIP-572%3A+Improve+timeouts+and+retries+in+Kafka+Streams) for more information |
