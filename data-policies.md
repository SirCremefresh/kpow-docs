---
description: Declarative Redaction of Sensitive Data
---

# Data Policies

kPow supports configurable redaction of Data Inspection results with Data Policies.

Data policies are defined in a YAML file and configured with an environment variable:

```text
DATA_POLICY_CONFIGURATION_FILE=/path/to/masking/config.yml
```

Data policies are a declarative way to define how redactions are applied.

kPow supports redactions on **both the key and value** attributes of records and supports redaction of scalar types \(eg: strings\) or structured data types \(eg: maps, collections\).

Structured data redaction currently supports AVRO, JSON, Transit, and EDN serdes.

**Note:** If data masking policies are configured the ability to inspect with String serdes is restricted.

## Data Policies

The YAML configuration defines policies, each policy contains:

* `name`: the unique name of the data policy
* `resources`: the resources governed by the policy
* `category`: the category for this policy
* `redaction`: the redaction function to be applied
* `type`: the type of data \(either `scalar` or `non-scalar`\)
* `fields`: the fields to redact for `non-scalar` data

### Example YAML

```text
policies:
  - name: Credit Card
    category: PII
    resources:
      - [ cluster, '*' ]
    redaction: ShowLast4
    type: non-scalar
    fields: [ credit_card, creditcard, pan ]
```

### Resource

Resources are defined through a [taxonomy](https://en.wikipedia.org/wiki/Taxonomy_%28biology%29) that describes the hierarchy of objects in kPow:

```text
[DOMAIN_TYPE, DOMAIN_ID, OBJECT_TYPE?, OBJECT_ID? OBJECT_RESOURCE?]
```

Where:

* `DOMAIN_TYPE`: always `cluster` for data policies
* `DOMAIN_ID`: the ID of the cluster or `*` for all clusters.
* `OBJECT_TYPE`: always `topic` for data policies
* `OBJECT_ID`: the name of the topic, wildcard not supported
* `OBJECT_RESOURCE`: either `key` or `value`

**Specifying a topic, key, or value is optional.**

### Example Resources

| `["cluster", "*"]` | All clusters and topics  |
| :--- | :--- |
| `["cluster", "N9xnGujkR32eYxHICeaHuQ"]` | All topics for a specific cluster |
| `["cluster", "*", "topic", "MyTopic"]` | Specific topic on all clusters \(key and value\) |
| `["cluster", "*", "topic", "MyTopic", "key"]` | Specific topic on all clusters \(key only\)  |
| `["cluster", "*", "topic", "MyTopic", "value"]` | Specific topic on all clusters \(value only\) |

###  Redaction Functions

Supported redaction functions include:

| Redaction | Description | Example Data | Example Result |
| :--- | :--- | :--- | :--- |
| Full | Fully redact the matched value | John Smith | \*\*\*\*\*\*\*\*\*\*\*\* |
| SHAHash | Apply a SHA512 hash to the value | John Smith | ed014a19bb67a85f9d... |
| ShowEmailHost | Only show the email host | [johnsmith@corp.org](mailto:johnsmith@corp.org) | \*\*\*\*\*\*\*\*\*@corp.org |
| ShowEmailPart | Show the email host and the first character of the email | [johnsmith@corp.org](mailto:johnsmith@corp.org) | j\*\*\*\*\*\*\*\*@corp.org |
| ShowFirst | Only show the first character | John Smith | J\*\*\*\*\*\*\*\*\* |
| ShowFirst2 | Only show the first two characters | John Smith | Jo\*\*\*\*\*\*\*\* |
| ShowFirst4 | Only show the first four characters | John Smith | John\*\*\*\*\*\* |
| ShowFirst6 | Only show the first six characters | John Smith | John S\*\*\*\* |
| ShowLast | Only show the last character | John Smith | \*\*\*\*\*\*\*\*\*h |
| ShowLast2 | Only show the last two characters | John Smith | \*\*\*\*\*\*\*\*th |
| ShowLast4 | Only show the last four characters | John Smith | \*\*\*\*\*\*mith |
| ShowLast6 | Only show the last six characters | John Smith | \*\*\*\* Smith |

###  Nested Redaction

kPow supports redaction of nested data structures, for example if we apply the Credit Card policy to a topic with the following JSON message:

```text
{ 
  "user_details": { 
    "email_address": "a@user.com",
    "payment_options": [
      { "credit_card": "376953644924215" } 
    ] 
  } 
}
```

The data would be masked accordingly when displayed in Data Inspect search results: 

```text
{ 
  "user_details": { 
    "email_address": "a@user.com",
    "payment_options": [
      { "credit_card": "***********4215" } 
    ] 
  } 
}
```

kPow is **conservative** when applying data policies. Given a field where the selected redaction function cannot apply, the fallback is to use the **Full** redaction policy, e.g:

```text
{ 
  "user_details": { 
    "email_address": "a@user.com",
    "payment_options": [
      { 
        "credit_card": {
          "pan": "376953644924215",
          "expiry": "10/10/2010"
        } 
      } 
    ] 
  } 
}
```

Applying the same Credit Card policy to this data incurs a **Full** redaction at the credit\_card field as kPow does not know how to apply the configured "ShowLast4" redactor to a structured value \(in this case a map with "pan" and "expiry" fields\).

The result is effectively truncated:

```text
{ 
  "user_details": { 
    "email_address": "a@user.com",
    "payment_options": [
      { "credit_card": "***************" } 
    ] 
  } 
}
```

### Data Policy Sandbox

You can test your data policies from within kPow using the Data Policies sandbox.

Inside kPow, navigate to **Admin -&gt; Data Policies**:

[![dp-sandbox.png](https://support.operatr.io/hc/article_attachments/900003409283/dp-sandbox.png)](https://github.com/operatr-io/operatr/blob/60fc2e0ce5684f29718755c8871c56f9171a6a05/docs/data-policies-sandbox.png)

The Data Policies admin UI also gives a read-only view into your defined policies, with the ability to test each policy within the sandbox.

[![dp-policies.png](https://support.operatr.io/hc/article_attachments/900003409303/dp-policies.png)](https://github.com/operatr-io/operatr/blob/60fc2e0ce5684f29718755c8871c56f9171a6a05/docs/data-policies-table.png)  


