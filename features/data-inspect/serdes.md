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

## Configuring serdes

kPow offers some configuration on how serdes are presented in the UI.

#### Default serdes

Set `DEFAULT_KEY_SERDES` or `DEFAULT_VALUE_SERDES` to specify which Serdes should be selected from the dropdown by default when using data inspect. 

#### Available serdes

To filter out serdes from the dropdown list in data inspect set `AVAILABLE_KEY_SERDES` or `AVAILABLE_VALUE_SERDES`  
  
Eg: `AVAILABLE_VALUE_SERDES=JSON,AVRO` to only ever show JSON or AVRO serdes from within kPow's UI

## Custom serdes

kPow allows you to use any serde that implements the [`org.apache.kafka.common.serialization.Serde`](https://kafka.apache.org/0102/javadoc/org/apache/kafka/common/serialization/Serde.html) interface.

Custom serdes integrate with all other data inspect features including [Data policies](../data-policies.md)

#### Classpath setup

kPow expects the custom serde class to live on the classpath.

Once the serdes have been added to kPow's classpath, set the following environment variable:

```text
CUSTOM_SERDES=org.corp.XMLSerde,org.corp.MyCustomSerde2
```

`CUSTOM_SERDES` expects a comma separated list of serdes found on the classpath.

#### YML config setup

A custom YML file can optionally be included on the classpath to further customise serde use with kPow.

For example: for the class `org.corp.XMLSerde` - kPow would expect the configuration for this serde to be present at `org/corp/XMLSerde.yml`on the classpath. 

An example of a custom serde YML file looks like:

```text
name: XML
format: json
field: key
config:
  bootstrap: "some-value"
  limit: 22
  display: another-value
  abc: $SOME_ENV
```

A serde defintion contains:

* `name` - the name of the serde to be presented in kPow's UI
* `format` - the format of the serde \(either `json`, `clojure` or `string`\) - set to `json` if the format is a structured data format.
* `field` - the field that relates to this serde \(either `key`, `value` or `any`\)
* `config` - a map of config values passed into the serde's `configure` method 

**Note**: If no YML file is found on the classpath for the serde, the configuration will default to:

```text
field: any
format: string
```

#### Custom Serdes + Data Policies

[Data policies](../data-policies.md) will work out of the box with custom serdes if the format specified is set to either `json` or `clojure`

