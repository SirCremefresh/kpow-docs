---
description: A glossary of all configuration options available to kPow
---

# Environment Variable Glossary

<table>
  <thead>
    <tr>
      <th style="text-align:left">Env Var</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Comment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>PORT</b>
      </td>
      <td style="text-align:left">3000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The kPow server port (will serve HTTPS traffic if so configured)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>ENABLE_GZIP</b>
      </td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Whether to enable gzip compression for kPow&apos;s static resources (JSON,
        CSS etc)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>NUM_PARTITIONS</b>
      </td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The number of partitions for kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>REPLICATION_FACTOR</b>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The replication factor of kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>REQUEST_TIMEOUT_MS</b>
      </td>
      <td style="text-align:left">30000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The request.timeout.ms settting for kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>MAX_PRODUCE_REQUEST_SIZE</b>
      </td>
      <td style="text-align:left">1000000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The max.produce.request.size setting for kPow&apos;s internal producers</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SNAPSHOT_PARALLELISM</b>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The level of parallelism configured for when kPow captures telemetry for
        snapshots. Increase OPEARTR internal parallelism for larger clusters</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SNAPSHOT_DEBUG</b>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Add additional logging messages to help debug snapshotting</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>PROMETHEUS_EGRESS</b>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Enable Prometheus endpoints for metrics and offsets egress</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>PROMETHEUS_LABEL_ENV</b>
      </td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Include your ENVIRONMENT_NAME as &apos;env&apos; label on Prometheus metrics</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CUSTOM_SERDES</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg: <code>io.operatr.SerdeOne,io.operatr.SerdeTwo</code>Comma separated
        names of custom serdes found on the classpath</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DEFAULT_KEY_SERDES</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The default key serde to use when inspecting data, eg: <code>AVRO</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DEFAULT_VALUE_SERDES</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The default key value to use when inspecting data, eg: <code>JSON</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>AVAILABLE_KEY_SERDES</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The list of key serdes to present when inspecting data, eg: <code>JSON,String,Transit / JSON</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>AVAILABLE_VALUE_SERDES</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The list of key serdes to present when inspecting data, eg: <code>JSON,String,io.operatr.SerdeOne</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>AUTH_PROVIDER_TYPE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>The OPENID provider configured for SSO, eg: <code>github</code>, <code>jetty</code>,<code>okta</code>
        </p>
        <p>See: <a href="../user-authentication/overview.md">User Authentication</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>AUTH_LANDING_URI</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The absolute URL to redirect to after successful OKTA login. Eg: https://staging.operatr.z-corp.com</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>OKTA_ORGANISATION</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The name of your Okta organisation, eg: my-corp</td>
    </tr>
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
    <tr>
      <td style="text-align:left"><b>OPENID_CLIENT_ID</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The &apos;Client ID&apos; found in your configured OpenID App</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>OPENID_CLIENT_SECRET</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The &apos;Client Secret&apos; found in your configured OpenID App</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAML_RELYING_PARTY_IDENTIFIER</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">You Operatr Application ID</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAML_ACS_URL</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Assertion Consumer Service URL</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAML_METADATA_FILE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The SAML Metadata File from your provider</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAML_CERT</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SAML Certificate (Optional)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAML_SESSION_S</b>
      </td>
      <td style="text-align:left">3600</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The duration in seconds before re-authenticating SAML credentials</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DEBUG_SAML</b>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Enable SAML debug logging in application logs</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>JETTY_AUTH_METHOD</b>
      </td>
      <td style="text-align:left">form</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>Configure if using <a href="../user-authentication/overview.md#jetty-authentication">Jetty authentication</a>
        </p>
        <p>Either: <code>form</code>or<code>basic</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>JETTY_AUTH_TYPE</b>
      </td>
      <td style="text-align:left">jaas</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HASH_USER_FILE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>RIEMANN_HOST</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Riemann host for metrics egress</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>RIEMANN_PORT</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Riemann port for metrics egress</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>ENABLE_HTTPS</b>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Serve kPow content via HTTPS</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_KEYSTORE_LOCATION</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg: /ssl/https.keystore.jks</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_KEYSTORE_TYPE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Type of SSL Keystore, eg JKS</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_KEYSTORE_PASSWORD</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SSL Keystore password</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_TRUSTSTORE_LOCATION</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg, /ssl/https.truststore.jks</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_TRUSTSTORE_TYPE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Type of SSL Truststore type, eg JKS</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTTPS_TRUSTSTORE_PASSWORD</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SSL Truststore password</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>RBAC_CONFIGURATION_FILE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The path to your Operatr RBAC Configuration (optional, expects SSO enabled)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>LIVE_MODE_ENABLED</b>
      </td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Allow your users to switch to Live Mode</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>LIVE_MODE_PERIOD_MS</b>
      </td>
      <td style="text-align:left">60000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Live Mode will prompt you to continue after this period</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>LIVE_MODE_INTERVAL_MS</b>
      </td>
      <td style="text-align:left">3500</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The amount of time between Live Mode snapshots</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>LIVE_MODE_MAX_CONCURRENT_USERS</b>
      </td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The maximum number of concurrent Live Mode user sessions</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAMPLER_TIMEOUT_MS</b>
      </td>
      <td style="text-align:left">7000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The end-to-end timeout for a data inspect query</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAMPLER_CONSUMER_THREADS</b>
      </td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The level of parallelism for a data inspect query</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DATA_POLICY_CONFIGURATION_FILE</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The path to your kPow Data Policy Configuration</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SLACK_WEBHOOK_URL</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Send Audit Log messages to Slack</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SLACK_WEBHOOK_AUDIT_LOG</b>
      </td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CONNECT_TIMEOUT_MS</b>
      </td>
      <td style="text-align:left">5000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The timeout value in ms for all HTTP requests made to a Kafka Connect
        cluster</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SHOW_SPLASH</b>
      </td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Turn off the initial page splash scre</td>
    </tr>
  </tbody>
</table>

