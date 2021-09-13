---
description: An introduction to filtering queries with kJQ
---

# kJQ Filters

## Overview

[**JQ**](https://stedolan.github.io/jq/) is a popular, practical language described as 'like sed for JSON data'. 

Data Inspect supports JQ-like filters on Kafka topics. We call this kJQ!

![Sample KJQ Query](../../.gitbook/assets/kjq.png)

kJQ is **fast**, easily scanning tens of thousands of messages from a Kafka topic each second.

The kJQ input field provides context highlighting, auto-completion, command memory \(press **up-arrow** to view previous filters\) and fast-execution \(press **shift-enter** to execute the search\).

Normally your kJQ filters will start with **.key .value or .header** but you can search on any field returned with a Kafka record, including topic, offset, etc.

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

Multiple kJQ filters can be joined with a logical **AND** or **OR**, just like normal JQ.

kJQ also supports standard explicit logical operator precedence with parenthesis.

e.g. `(.key.id or .key.currency == "GBP) and .value.tx.discount | to-double < 20.20`

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

Matches where the selector &gt; 10 

E.g. `{"foo": {"bar": 11}}` will match, `{"foo": {"bar": 8}}` will not

### Selector Comparator Filter

```text
.foo.bar == .foo.zoo
```

Matches where both selectors are equal.

E.g. `{"foo": {"bar": 10, "zoo": 10}}` will match, `{"foo": {"bar": 10, "zoo": 7}}` will not

### Function Filter

```text
.foo.baz[0] | contains("IDDQD")
```

Matches where the selector contains text

E.g. `{"foo": {"baz": ["IDDQDXXXXX"]}}` will match, `{"foo": {"baz": ["XXXXX"]}}` will not.

### Negated Filter

```text
.[0].foo | contains("IDDQD") | not
```

Matches where the selector does not contain text.

### Quoted and Clojure Selectors / Scalars

```text
.foo/bar.baz > 10,
.foo."field!" == :some-keyword
```

kJQ understands quoted and Clojure data

### Multiple Filters \(And\)

```text
.foo.bar > 10 and
.foo.bar == .foo.zoo and
.foo.baz[0] | contains("IDDQD")
```

Matches where **every** filter is true.

### Multiple Filters \(Or\)

```text
.foo.bar == .foo.zoo or
.foo.baz[0] | contains("IDDQD")
```

Matches where **any** filter is true.

### Multiple Filters \(Mixed\)

Combine multiple filters with **and**, **or, and explicit precedence.**

```text
(.key.currency == "GBP" and
 .value.tx.price | to-double < 16.50 and
 .value.tx.pan | endswith("8649")) or 
(.key.currency == "GBP" and 
 .value.tx.discount == "3.98")
```

