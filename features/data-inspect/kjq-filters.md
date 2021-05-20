---
description: An introduction to filtering queries with kJQ
---

# kJQ Filters

## Overview

[**JQ**](https://stedolan.github.io/jq/) is a popular, practical language described as 'like sed for JSON data'. Data inspect supports JQ-like filters on Kafka topics. We call this kJQ!

kPow implements a subset of JQ allowing you to search [**JSON**, **Avro**, **Transit**, **EDN**, **String**, and **Custom Serdes**](serdes.md) with complex queries on structured data.

## Language

In simple terms kJQ supports multiple comma-separated _filters,_ one optional _reduction,_ one optional _negation,_ in that order.

kJQ filters can be applied to keys, values, and headers. kPow will scan **tens of thousands of messages a second** to find matching data.

kJQ is **not whitespace sensitive.**

### kJQ Grammar

A kJQ filter is a limited version of [a basic JQ filter](https://stedolan.github.io/jq/manual/v1.4/#Basicfilters)

A _filter_ consists of a _selector_ optionally followed by either a _comparator_ or a _function._

A _selector_ is a JQ dot notation Object Index or **zero-based** Array Index.

e.g. `.foo.bar, .[1], .foo[1].bar`

A _comparator_ is an _operator_ followed by a _selector_ or a _scalar._

Valid operators: `==`, `!=`, `<`, `<=`, `>`, `>=`

e.g. `>= 10`, `!= false`, `== "text"`, `< .foo.baz`

A _function_ is a _pipe_ followed by a _function-name_ with _text_ parameter.

Valid function names: `startswith`, `endswith`, `contains`

e.g**:** `| startswith("text")`, `| endswith("text")`, `| contains("text")`

### kJQ Query Evaluation

Multiple comma-separated kJQ filters are evaluated **in isolation** and then combined into a single query predicate with a _reduction._

Strict filter isolation means the behaviour of kJQ is slightly different from JQ, particularly regarding _pipe_ precedence.

The default _reduction_ is **all**, which is a logical **and** of your filters. You can explicitly set a query reduction to **any**, or **all**, which is a logical **or** of your filters.

e.g. `| any | all`

### kJQ Query Negation

A kJQ query predicate can be negated, this is the logical negation of the combined predicate.

e.g. `| not`

## Examples

### Truthy Filter

```text
.foo
```

Matches where the selector is not null \(eg `{"foo": true}` or `{"foo": 1}` will match, `{"bar": true}` will not match\)

###  Scalar Comparator Filter

```text
.foo.bar > 10
```

Matches where the selector &gt; 10 \(eg, `{"foo": {"bar": 11}}` will match, `{"foo": {"bar": 8}}` will not\)

### Selector Comparator Filter

```text
.foo.bar == .foo.zoo
```

Matches where both selectors are equal \(eg `{"foo": {"bar": 10, "zoo": 10}}` will match, `{"foo": {"bar": 10, "zoo": 7}}` will not\)

### Function Filter

```text
.foo.baz[0] | contains("IDDQD")
```

Matches where the selector contains text \(eg `{"foo": {"baz": ["IDDQDXXXXX"]}}` will match, `{"foo": {"baz": ["XXXXX"]}}` will not\)

### Negated Filter

```text
.[0].foo | contains("IDDQD") | not
```

Matches where the selector does not contain text

### Quoted and Clojure Selectors / Scalars

```text
.foo/bar.baz > 10,
.foo."field!" == :some-keyword
```

kJQ understands quoted and Clojure data

### Multiple Filters + \(Default\) All

```text
.foo.bar > 10,
.foo.bar == .foo.zoo,
.foo.baz[0] | contains("IDDQD")
```

Matches where **every** filter is true \(default\). \(eg `{"foo": {"bar": 12, "zoo": 12, "baz": ["IDDQDXXXXX"]}}` will match\)

### Multiple Filters + Explicit All

```text
.foo.bar > 10,
.foo.bar == .foo.zoo,
.foo.baz[0] | contains("IDDQD")
| all
```

Matches where **every** filter is true.

### Multiple Filters + Any

```text
.foo.bar == .foo.zoo,
.foo.baz[0] | contains("IDDQD")
| any
```

Matches where **any** filter is true. \(eg, `{"foo: {"baz": ["IDDQDXXX"]}}` will match\)  


**Multiple Filters + Any + Negated**

```text
.foo.bar > 10,
.foo.bar == .foo.zoo,
.foo.baz[0] | contains("IDDQD")
| any
| not
```

Matches where **any filter is false**  


