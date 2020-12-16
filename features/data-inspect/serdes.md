---
description: Configuration of serdes for data inspect
---

# Serdes

By default, kPow ships with the following serdes available from data inspect:

* JSON
* AVRO
* String
* EDN
* Double
* Float
* Integer
* Long
* Short
* Transit / JSON
* Transit / JSON-Verbose
* Transit / Msgpack

## AVRO

kPow integrates with Confluent [Schema Registry](https://docs.confluent.io/platform/current/schema-registry/index.html) and allows for AVRO serdes to be used in data inspect

See the [Schema Registry](https://app.gitbook.com/@operatr-io/s/kpow/~/drafts/-MN6L_-tcDmaE5R2dq-T/configuration/schema-registry) page for documentation on how to configure Confluent Schema Registry with kPow.

Once configured, from within the data inspect UI you will now be able to select the schema and subject strategy when searching for records by key:

![](../../.gitbook/assets/screen-shot-2020-11-27-at-1.20.34-pm.png)

## Configuring Serdes

kPow offers some configuration on how serdes are presented in the UI.

#### Default Serdes

Set `DEFAULT_KEY_SERDES` or `DEFAULT_VALUE_SERDES` to specify which serdes should be selected from the dropdown by default when using data inspect. 

#### Available Serdes

To restrict the serdes available to your users set `AVAILABLE_KEY_SERDES` or `AVAILABLE_VALUE_SERDES`  
  
Eg: `AVAILABLE_VALUE_SERDES=JSON,AVRO` to only ever show JSON or AVRO serdes from within kPow's UI

## Custom Serdes

{% hint style="info" %}
kPow can be configured with any [`org.apache.kafka.common.serialization.Serde`](https://kafka.apache.org/0102/javadoc/org/apache/kafka/common/serialization/Serde.html)
{% endhint %}

#### Setup

1. Provide your custom serdes on the kPow classpath \(see [How to add a Jar to the Classpath](https://docs.oracle.com/javase/tutorial/deployment/jar/downman.html)\).
2. Configure kPow with the `CUSTOM_SERDES` environment variable:

```text
# CUSTOM_SERDES accepts a comma-separated list of serdes classes

CUSTOM_SERDES=org.corp.XMLSerde,org.corp.MyCustomSerde
```

#### Configuration

Include a YAML configuration file in your jar to configure custom serdes further \(Optional\).

**E.g.** `org.corp.XMLSerde` can be configured with `org/corp/XMLSerde.yml`

The following fields are available to configure your serdes:

* `name` - the display name to use in kPow's Data Inspect UI.
* `format` - `json`, `clojure` or `string` \(default\)
* `isKey` -  **true** for key data only, **false** for value data only, **leave unset** for both key/value data.
* `config` - a map of config values passed into the serdes `configure` method 

`Config` is converted to String/String and passed to your Serdes/configure method.   
`Config` values starting with $ are resolved as environment variables. \(e.g. $SOME\_ENV below\)

**E.g.** Single Serdes Configuration \(json format, available to key and value fields\).

```text
name: PROTO
format: json
config:
  bootstrap: "some-value"
  limit: 22
  display: another-value
  abc: $SOME_ENV
```

**E.g.** Multi Serdes Configuration \(json format, separate configured serdes for key and value fields\)

```text
serdes:
  - name: "PROTO 1"
    format: "json"
    isKey: true
    config:
      bootstrap: "some-value"
      limit: 22
      display: another-value
      abc: $SOME_ENV
  - name: "PROTO 2"
    format: "json"
    isKey: false
    config:
      bootstrap: "some-value"
      limit: "100"
      display: another-value
      abc: $ANOTHER_ENV
```

{% hint style="warning" %}
Serdes default to String format and are available to keys and values where no config provided
{% endhint %}

#### Custom Serdes + Data Policies

[Data policies](../data-policies.md) apply to custom serdes whose format is specified as either `json` or `clojure`

#### Custom Serdes + kJQ

kJQ filters are available to custom serdes whose format is specified as either `json` or `clojure`

