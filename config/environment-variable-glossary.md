---
description: A glossary of all configuration options available to kPow
---

# Environment Variable Glossary

## Web Server 

### PORT

| Env Var | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| PORT | long | 3000 | The kPow web server port  |

**Note:** will serve HTTPS traffic if so configured.

### HTTP\_FORWARDED

| Env Var | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| HTTP\_FORWARDED | bool | false | Set when kPow is running behind a reverse proxy. |

**Note**: see [Deployment notes](../installation/deployment-notes.md) for reverse proxy examples. 

### ENABLE\_GZIP

| Env Var | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| ENABLE\_GZIP | bool | true | Whether to enable gzip compression for kPow's static resources \(JSON, CSS etc\) |

### ENABLE\_HTTPS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| ENABLE\_HTTPS | false | bool | Serve kPow content via HTTPS |

**Note:** see [HTTPS connections](../features/https-connections.md) for more details about configuration. 

### **HTTPS\_SNI\_HOST\_CHECK**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_SNI\_HOST\_CHECK** | false | bool | When SSL configured, whether the certificate sent to the client matches the Host header. |

### **HTTPS\_KEYSTORE\_LOCATION**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_KEYSTORE\_LOCATION** |  | string | eg: /ssl/https.keystore.jks |

### **HTTPS\_KEYSTORE\_TYPE**

| Env Var | Default | Type |  |
| :--- | :--- | :--- | :--- |
| **HTTPS\_KEYSTORE\_TYPE** |  | string | Type of SSL Keystore, eg JKS |

### **HTTPS\_KEYSTORE\_PASSWORD**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_KEYSTORE\_PASSWORD** |  | string | SSL Keystore password |

### **HTTPS\_TRUSTSTORE\_LOCATION**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_TRUSTSTORE\_LOCATION** |  | string | eg, /ssl/https.truststore.jks |

### **HTTPS\_TRUSTSTORE\_TYPE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_TRUSTSTORE\_TYPE** |  | string | Type of SSL Truststore type, eg JKS |

### **HTTPS\_TRUSTSTORE\_PASSWORD**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HTTPS\_TRUSTSTORE\_PASSWORD** |  | string | SSL Truststore password |

## Authentication

### AUTH\_PROVIDER\_TYPE

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **AUTH\_PROVIDER\_TYPE** |  | enum | The OPENID provider configured for SSO, eg: `github`, `jetty`,`okta` |

Note: see [User Authentication](../authentication/overview.md) for more details

### OKTA\_ORGANISATION

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **OKTA\_ORGANISATION** |  | string | The name of your Okta organisation, eg: my-corp |

### AUTH\_LANDING\_URI

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **AUTH\_LANDING\_URI** |  | string | The absolute URL to redirect to after successful OKTA login. Eg: https://staging.operatr.z-corp.com |

### **OPENID\_AUTH\_URI**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Env Var</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>OPENID_AUTH_URI</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>For GitHub: <a href="https://github.com/login/oauth/authorize">https://github.com/login/oauth/authorize</a>
        </p>
        <p>For GitHub enterprise: [Server URL]/login/oauth/authorize</p>
      </td>
    </tr>
  </tbody>
</table>

### OPENID\_API\_URI

<table>
  <thead>
    <tr>
      <th style="text-align:left">Env Var</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>OPENID_API_URI</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>For GitHub:</p>
        <p><a href="https://api.github.com/user">https://api.github.com/user</a>
        </p>
        <p>For GitHub enterprise: [Server URL]/api/v3/user</p>
      </td>
    </tr>
  </tbody>
</table>

### OPENID\_TOKEN\_URI

<table>
  <thead>
    <tr>
      <th style="text-align:left">Env Var</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>OPENID_TOKEN_URI</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>For GitHub: <a href="https://github.com/login/oauth/access_token">https://github.com/login/oauth/access_token</a>
        </p>
        <p>For GitHub enterprise: [Server URL]/login/oauth/access_token</p>
      </td>
    </tr>
  </tbody>
</table>

### OPENID\_CLIENT\_ID

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **OPENID\_CLIENT\_ID** |  | string | The 'Client ID' found in your configured OpenID App |

### OPENID\_CLIENT\_SECRET

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **OPENID\_CLIENT\_SECRET** |  | string | The 'Client Secret' found in your configured OpenID App |

### **SAML\_RELYING\_PARTY\_IDENTIFIER**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAML\_RELYING\_PARTY\_IDENTIFIER** |  | string | You Operatr Application ID |

### SAML\_ACS\_URL

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAML\_ACS\_URL** |  | string | The Assertion Consumer Service URL |

### **SAML\_METADATA\_FILE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAML\_METADATA\_FILE** |  | string | The SAML Metadata File from your provider |

### SAML\_CERT

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAML\_CERT** |  | string | SAML Certificate \(Optional\) |

### **SAML\_SESSION\_S**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAML\_SESSION\_S** | 3600 | long | The duration in seconds before re-authenticating SAML credentials |

### DEBUG\_SAML

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **DEBUG\_SAML** | false | bool | Enable SAML debug logging in application logs |

### **JETTY\_AUTH\_METHOD**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Env Var</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>JETTY_AUTH_METHOD</b>
      </td>
      <td style="text-align:left">form</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>Configure if using <a href="../authentication/overview.md#jetty-authentication">Jetty authentication</a>
        </p>
        <p>Either: <code>form</code>or<code>basic</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### **JETTY\_AUTH\_TYPE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **JETTY\_AUTH\_TYPE** | jaas | enum |  |

### HASH\_USER\_FILE

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **HASH\_USER\_FILE** |  | string |  |

## Authorization

### **RBAC\_CONFIGURATION\_FILE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **RBAC\_CONFIGURATION\_FILE** |  | string | The path to your Operatr RBAC Configuration \(optional, expects SSO enabled\) |

**Note:** see [Authorization](../authorization/role-based-access-control.md) for more details

## Kafka

## kPow

### **DATA\_POLICY\_CONFIGURATION\_FILE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **DATA\_POLICY\_CONFIGURATION\_FILE** |  | string | The path to your kPow Data Policy Configuration |

Note: see [Data Policies](../features/data-policies.md) for more information

### CONNECT\_TIMEOUT\_MS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **CONNECT\_TIMEOUT\_MS** | 5000 | long | The timeout value in ms for all HTTP requests made to a Kafka Connect cluster |

### CUSTOM\_SERDES

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **CUSTOM\_SERDES** |  | string | eg: `io.operatr.SerdeOne,io.operatr.SerdeTwo`Comma separated names of custom serdes found on the classpath |

**Note**: see [Custom serdes](../features/data-inspect/serdes.md#custom-serdes) for more information

### DEFAULT\_KEY\_SERDES

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **DEFAULT\_KEY\_SERDES** |  | string | The default key serde to use when inspecting data, eg: `AVRO` |

### DEFAULT\_VALUE\_SERDES

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **DEFAULT\_VALUE\_SERDES** |  | string | The default key value to use when inspecting data, eg: `JSON` |

### **AVAILABLE\_KEY\_SERDES**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **AVAILABLE\_KEY\_SERDES** |  | string | The list of key serdes to present when inspecting data, eg: `JSON,String,Transit / JSON` |

### **AVAILABLE\_VALUE\_SERDES**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **AVAILABLE\_VALUE\_SERDES** |  | string | The list of key serdes to present when inspecting data, eg: `JSON,String,io.operatr.SerdeOne` |

### NUM\_PARTITIONS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **NUM\_PARTITIONS** | 12 | long | The number of partitions for kPow's internal consumer groups |

### REPLICATION\_FACTOR

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **REPLICATION\_FACTOR** | 3 | long | The replication factor of kPow's internal consumer groups |

### REQUEST\_TIMEOUT\_MS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **REQUEST\_TIMEOUT\_MS** | 30000 | long | The request.timeout.ms settting for kPow's internal consumer groups |

### **MAX\_PRODUCE\_REQUEST\_SIZE**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **MAX\_PRODUCE\_REQUEST\_SIZE** | 1000000 | long | The max.produce.request.size setting for kPow's internal producers |

### **PROMETHEUS\_EGRESS**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **PROMETHEUS\_EGRESS** | false | bool | Enable Prometheus endpoints for metrics and offsets egress |

### **PROMETHEUS\_LABEL\_ENV**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **PROMETHEUS\_LABEL\_ENV** | true | bool | Include your ENVIRONMENT\_NAME as 'env' label on Prometheus metrics |

### SNAPSHOT\_PARALLELISM

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SNAPSHOT\_PARALLELISM** | 3 | long | The level of parallelism configured for when kPow captures telemetry for snapshots. Increase OPEARTR internal parallelism for larger clusters |

### SNAPSHOT\_DEBUG

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SNAPSHOT\_DEBUG** | false | bool | Add additional logging messages to help debug snapshotting |

### LIVE\_ MODE\_ENABLED

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **LIVE\_MODE\_ENABLED** | true | bool | Allow your users to switch to Live Mode |

**Note**: see [Live mode](../features/live-mode.md) for more details.

### **LIVE\_MODE\_PERIOD\_MS**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **LIVE\_MODE\_PERIOD\_MS** | 60000 | long | Live Mode will prompt you to continue after this period |

### **LIVE\_MODE\_INTERVAL\_MS**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **LIVE\_MODE\_INTERVAL\_MS** | 3500 | long | The amount of time between Live Mode snapshots |

### **LIVE\_MODE\_MAX\_CONCURRENT\_USERS**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **LIVE\_MODE\_MAX\_CONCURRENT\_USERS** | 2 | long | The maximum number of concurrent Live Mode user sessions |

### SAMPLER\_TIMEOUT\_MS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAMPLER\_TIMEOUT\_MS** | 7000 | long | The end-to-end timeout for a data inspect query |

### SAMPLER\_CONSUMER\_THREADS

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SAMPLER\_CONSUMER\_THREADS** | 6 | long | The level of parallelism for a data inspect query |

### **SLACK\_WEBHOOK\_URL**

| Env Var | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SLACK\_WEBHOOK\_URL** |  | string | Send Audit Log messages to Slack |

### **SLACK\_WEBHOOK\_URL**

| **Env Var** | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SLACK\_WEBHOOK\_VERBOSITY** | Mutations | enum | Possible values: All, Mutations, Queries |

### SHOW\_SPLASH

| **Env Var** | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **SHOW\_SPLASH** | true | bool | Turn off the initial page splash scre |

### **STREAMS\_ERROR\_STRATEGY**

| **Env Var** | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **STREAMS\_ERROR\_STRATEGY** | LOG\_EXCEPTION | enum | The strategy to use when kPow's internal Kafka Streams instance enters an ERROR state. Possible values: LOG\_EXCEPTION, LOG\_AND\_EXIT |

### **STREAMS\_TASK\_TIMEOUT\_MS**

| **Env Var** | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| **STREAMS\_TASK\_TIMEOUT\_MS** | 300000 | long | Configures kPow's internal streams `task.timeout.ms` value. See: [KIP-572](https://cwiki.apache.org/confluence/display/KAFKA/KIP-572%3A+Improve+timeouts+and+retries+in+Kafka+Streams) for more information |

