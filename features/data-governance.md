# Data Governance

kPow **captures all user actions in an audit log.**

The audit log is retained in an internal topic, **`__oprtr_audit_log`** and displayed in the kPow UI.

kPow provides [**Slack Integration** ](slack-integration.md)to have user actions sent to the slack channel of your choosing.

The audit log captures requests and responses related to each user action, as well as the metadata associated with the request.

### Sample Audit Record

Consider a request to create a new Kafka topic named `tx-events`.

kPow has been configured with Github SSO and the following RBAC policy.

```yaml
policies:
  - resource: ["cluster", "Enpl9Kw4QK6pwK0LaRVssQ"]
    effect:   "Allow"
    actions:  ["TOPIC_INSPECT", "TOPIC_EDIT", "TOPIC_PRODUCE"]
    role:     "*"
```

The request to create Kafka topic `tx-events` will result in the following audit record.

```text
{:data
 {:user
  {:provider :github,
   :email "john@mycorp.org",
   :name "John Smith",
   :login "JohnSmithGithub",
   :id "e69002ee-467d-4d6f-8236-054c58b2a00c"},
  :event
  [:mutation/create-topic
   {:topic-name "MyNewTopic",
    :replication-factor "1",
    :partitions "1",
    :config-items {},
    :request/ctx {:cluster-id "Enpl9Kw4QK6pwK0LaRVssQ"}}],
  :rbac
  {:success? true,
   :action "TOPIC_CREATE",
   :policies
   ({:resource [:cluster "*"],
     :role "*",
     :effect "Allow",
     :actions
     #{"TOPIC_INSPECT" "TOPIC_EDIT" "TOPIC_PRODUCE"}})}},
 :ctx {:cluster-id "Enpl9Kw4QK6pwK0LaRVssQ"}, 
 :type :mutation/request}
```

The audit log record contains the following details:

* The contents of the request itself \(topic create request\)
* Metadata about the user who made the request \(John Smith\)
* Authorization results:
  * Whether the user was authorized to perform the request
  * The matching policies that were evaluated against the request
  * The action required to perform the mutation \(`TOPIC_CREATE`\)

