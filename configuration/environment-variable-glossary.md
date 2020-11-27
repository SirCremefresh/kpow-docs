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
      <td style="text-align:left">PORT</td>
      <td style="text-align:left">3000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The kPow server port (will serve HTTPS traffic if so configured)</td>
    </tr>
    <tr>
      <td style="text-align:left">ENABLE_GZIP</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Whether to enable gzip compression for kPow&apos;s static resources (JSON,
        CSS etc)</td>
    </tr>
    <tr>
      <td style="text-align:left">NUM_PARTITIONS</td>
      <td style="text-align:left">12</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The number of partitions for kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left">REPLICATION_FACTOR</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The replication factor of kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left">REQUEST_TIMEOUT_MS</td>
      <td style="text-align:left">30000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The request.timeout.ms settting for kPow&apos;s internal consumer groups</td>
    </tr>
    <tr>
      <td style="text-align:left">MAX_PRODUCE_REQUEST_SIZE</td>
      <td style="text-align:left">1000000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The max.produce.request.size setting for kPow&apos;s internal producers</td>
    </tr>
    <tr>
      <td style="text-align:left">SNAPSHOT_PARALLELISM</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The level of parallelism configured for when kPow captures telemetry for
        snapshots. Increase OPEARTR internal parallelism for larger clusters</td>
    </tr>
    <tr>
      <td style="text-align:left">SNAPSHOT_DEBUG</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Add additional logging messages to help debug snapshotting</td>
    </tr>
    <tr>
      <td style="text-align:left">PROMETHEUS_EGRESS</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Enable Prometheus endpoints for metrics and offsets egress. See: <a href="../features/prometheus.md">Promethus Integration</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PROMETHEUS_LABEL_ENV</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Include your ENVIRONMENT_NAME as &apos;env&apos; label on Prometheus metrics</td>
    </tr>
    <tr>
      <td style="text-align:left">CUSTOM_SERDES</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg: <code>io.operatr.SerdeOne,io.operatr.SerdeTwo</code>Comma separated
        names of custom serdes found on the classpath. See: <a href="../features/data-inspect/serdes.md#configuring-serdes">Custom Serdes</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DEFAULT_KEY_SERDES</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The default key serde to use when inspecting data, eg: <code>AVRO</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DEFAULT_VALUE_SERDES</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The default key value to use when inspecting data, eg: <code>JSON</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AVAILABLE_KEY_SERDES</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The list of key serdes to present when inspecting data, eg: <code>JSON,String,Transit / JSON</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AVAILABLE_VALUE_SERDES</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The list of key serdes to present when inspecting data, eg: <code>JSON,String,io.operatr.SerdeOne</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AUTH_PROVIDER_TYPE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>The OPENID provider configured for SSO, eg: <code>github</code>, <code>okta </code>
        </p>
        <p>See: <a href="../user-authentication/openid/">OpenID/Oauth 2.0</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AUTH_LANDING_URI</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The absolute URL to redirect to after successful OKTA login. Eg: https://staging.operatr.z-corp.com</td>
    </tr>
    <tr>
      <td style="text-align:left">OKTA_ORGANISATION</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The name of your Okta organisation, eg: my-corp</td>
    </tr>
    <tr>
      <td style="text-align:left">OPENID_AUTH_URI</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>For GitHub: <a href="https://github.com/login/oauth/authorize">https://github.com/login/oauth/authorize</a>
        </p>
        <p>For GitHub enterprise: [Server URL]/login/oauth/authorize</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">OPENID_API_URI</td>
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
      <td style="text-align:left">OPENID_TOKEN_URI</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>For GitHub: <a href="https://github.com/login/oauth/access_token">https://github.com/login/oauth/access_token</a>
        </p>
        <p>For GitHub enterprise: [Server URL]/login/oauth/access_token</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">OPENID_CLIENT_ID</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The &apos;Client ID&apos; found in your configured OpenID App</td>
    </tr>
    <tr>
      <td style="text-align:left">OPENID_CLIENT_SECRET</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The &apos;Client Secret&apos; found in your configured OpenID App</td>
    </tr>
    <tr>
      <td style="text-align:left">SAML_RELYING_PARTY_IDENTIFIER</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>You Operatr Application ID</p>
        <p>See: <a href="../user-authentication/saml/">SAML</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SAML_ACS_URL</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Assertion Consumer Service URL</td>
    </tr>
    <tr>
      <td style="text-align:left">SAML_METADATA_FILE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The SAML Metadata File from your provider</td>
    </tr>
    <tr>
      <td style="text-align:left">SAML_CERT</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SAML Certificate (Optional)</td>
    </tr>
    <tr>
      <td style="text-align:left">SAML_SESSION_S</td>
      <td style="text-align:left">3600</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The duration in seconds before re-authenticating SAML credentials</td>
    </tr>
    <tr>
      <td style="text-align:left">DEBUG_SAML</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Enable SAML debug logging in application logs</td>
    </tr>
    <tr>
      <td style="text-align:left">JETTY_AUTH_METHOD</td>
      <td style="text-align:left">form</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">JETTY_AUTH_TYPE</td>
      <td style="text-align:left">jaas</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">HASH_USER_FILE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">RIEMANN_HOST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Riemann host for metrics egress</td>
    </tr>
    <tr>
      <td style="text-align:left">RIEMANN_PORT</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The Riemann port for metrics egress</td>
    </tr>
    <tr>
      <td style="text-align:left">ENABLE_HTTPS</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">
        <p>Serve kPow content via HTTPS</p>
        <p>See: <a href="../features/https-connections.md">HTTPS Connections</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_KEYSTORE_LOCATION</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg: /ssl/https.keystore.jks</td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_KEYSTORE_TYPE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Type of SSL Keystore, eg JKS</td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_KEYSTORE_PASSWORD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SSL Keystore password</td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_TRUSTSTORE_LOCATION</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">eg, /ssl/https.truststore.jks</td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_TRUSTSTORE_TYPE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Type of SSL Truststore type, eg JKS</td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_TRUSTSTORE_PASSWORD</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">SSL Truststore password</td>
    </tr>
    <tr>
      <td style="text-align:left">RBAC_CONFIGURATION_FILE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The path to your Operatr RBAC Configuration (optional, expects SSO enabled)</td>
    </tr>
    <tr>
      <td style="text-align:left">LIVE_MODE_ENABLED</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">
        <p>Allow your users to switch to Live Mode</p>
        <p>See: <a href="../features/live-mode.md">Live Mode</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LIVE_MODE_PERIOD_MS</td>
      <td style="text-align:left">60000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Live Mode will prompt you to continue after this period</td>
    </tr>
    <tr>
      <td style="text-align:left">LIVE_MODE_INTERVAL_MS</td>
      <td style="text-align:left">3500</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The amount of time between Live Mode snapshots</td>
    </tr>
    <tr>
      <td style="text-align:left">LIVE_MODE_MAX_CONCURRENT_USERS</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The maximum number of concurrent Live Mode user sessions</td>
    </tr>
    <tr>
      <td style="text-align:left">SAMPLER_TIMEOUT_MS</td>
      <td style="text-align:left">7000</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The end-to-end timeout for a data inspect query</td>
    </tr>
    <tr>
      <td style="text-align:left">SAMPLER_CONSUMER_THREADS</td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">The level of parallelism for a data inspect query</td>
    </tr>
    <tr>
      <td style="text-align:left">DATA_POLICY_CONFIGURATION_FILE</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>The path to your kPow Data Policy Configuration.</p>
        <p>See: <a href="../features/data-policies.md">Data Policies</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SLACK_WEBHOOK_URL</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>Send Audit Log messages to Slack.</p>
        <p>See: <a href="../features/slack-integration.md">Slack Integration</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SLACK_WEBHOOK_AUDIT_LOG</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SHOW_SPLASH</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Turn off the initial page splash screen</td>
    </tr>
  </tbody>
</table>



