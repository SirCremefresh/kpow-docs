---
description: Secure kPow with RBAC
---

# Role Based Access Control

Role Based Access Control \(RBAC\) integrates with [**User Authentication**](../user-authentication/overview.md), leveraging roles that you have assigned to users in the credentials system of your choice. 

RBAC configuration is defined in a YAML file and configured with an environment variable:

```text
RBAC_CONFIGURATION_FILE=/path/to/rbac-config.yaml
```

RBAC provides **fine-grained control** of user actions on specific resources determined by a user's roles.

## Authorized Roles

kPow will restrict UI access to users who have **at least one role** defined in the RBAC configuration.

You may override this behaviour by providing a **specific list of `authorized_roles`** in your config.

```yaml
## Allow all users access to the UI ("*" is a role held by everyone)
authorized_roles:
  - "*"
  
## Or, allow users with specific roles access to the UI
authorized_roles:
  - "kafka-user"
  - "kafka-admin"
  - "ops-support"
```

## Policies

An RBAC Policy contains:

* **Resource**: The resource that this policy controls access to
* **Effect**: Whether to **deny** or **allow** access to the **Resource**
* **Actions**: A list of actions that this policy **Effects**

Then either:

* **Role:** The user role that this policy applies to
* **Roles:** The list of user roles that this policy applies to

### Example Configuration

The following configuration applies controls to three roles and **permits all authenticated users access**.

```yaml
authorized_roles:
  - "*"
  
policies:
  - resource: ["cluster", "N9xnGujkR32eYxHICeaHuQ"] 
    effect:   "Allow" 
    actions:  ["TOPIC_INSPECT", "TOPIC_PRODUCE", "TOPIC_EDIT"] 
    role:     "kafka-admin"
  - resource: ["cluster", "N9xnGujkR32eYxHICeaHuQ", "topic", "tx_audit"]
    effect:   "Deny"
    actions:  ["TOPIC_PRODUCE", "TOPIC_EDIT"]
    role:     "kafka-admin"
  - resource: ["cluster", "*"]
    effect:   "Allow" 
    actions:  ["GROUP_EDIT"] 
    roles:    ["kafka-admin","kafka-user"] 
```

**`kafka-admin`** is allowed to inspect, produce, and edit all topics **in a specific cluster**, then explicitly denied produce and edit actions to **one specific topic in that same cluster**. 

{% hint style="info" %}
**Note:** Where multiple policies apply to one resource, **Deny** effects take precedence.
{% endhint %}

**`kafka-admin`** and **`kafka-user`** are then permitted group edit permissions on all clusters.

All remaining actions are **implicitly denied** actions to all users on all resources.

## Resources

Resources are defined within a [taxonomy](https://en.wikipedia.org/wiki/Taxonomy_%28biology%29) that describes the hierarchy of objects in Operatr:

```text
[DOMAIN_TYPE, DOMAIN_ID, OBJECT_TYPE?, OBJECT_ID?]
```

Where:

* **Domain Type**: The top-level resource, either **cluster**, **schema**, or **connect**
* **Domain ID:** Unique identifier of the domain, **\*** for all/wildcard
* **Object Type:** Either either **topic, group, connector, subject,** or **broker**
* **Object ID:** Unique identified of the object. Wildcard not supported

Specifying the object is optional, if not provided the resource includes all objects within a domain.

### Example Resources

```text
["cluster", "*"] - all clusters and all objects
["cluster", "*", "topic"] - all topics on all clusters
["cluster", "N9xnGujkR32eYxHICeaHuQ"] - all objects in a cluster
["cluster", "*", "topic", "tx-events"] - named topic in all clusters
```

### Resource IDs

Operatr logs the IDs of all top-level resources at startup:

```text
 Connected to [2] Kafka clusters:
 * g10tMLohRLKthriTt0749g (Local):
   - kafka connect: http://kafka:8083 (g10tMLohRLKthriTt0749g)
   - schema registry not configured
 * lkc-lo019 (Confluent Cloud):
   - kafka connect not configured
   - schema registry: https://xxx.us-east-2.aws.confluent.cloud (a2f06a916672d71d675f) (Confluent Cloud)
```

In the example above we have four **domain** resources:

* Two Kafka Clusters \(`g10tMLohRLKthriTt0749g`, `lkc-lo0o9`\)
* One Kafka Connect \(`g10tMLohRLKthriTt0749g`\)
* One Schema Registry \(`a2f06a916672d71d675f`\)

#### Resource ID Definitions

* `Kafka Cluster` - the ID of the Kafka cluster as returned by a broker
* `Kafka Connect` - the ID of the Kafka cluster associated with the Kafka Connect installation
* `Schema Registry` - a SHA256 hash of the Schema Registry endpoint

## Effects

Specify `Allow` or `Deny` to indicate whether the policy allows or denies access to a resource.

Where no matching policy exists the effect is an **implicit deny.**

## Actions

Operatr supports this list of user actions:

* `TOPIC_CREATE` - create new topics
* `TOPIC_DELETE` - delete topics
* `TOPIC_INSPECT` - view full message data \(key and value\)
* `TOPIC_PRODUCE` - edit topic configuration and delete topics
* `TOPIC_EDIT` - edit topic configuration and delete topics
* `GROUP_EDIT` - reset group offsets and delete consumer groups
* `SCHEMA_EDIT` - edit and delete schema subjects
* `SCHEMA_CREATE` - create new schemas
* `BROKER_EDIT` - edit broker configuration
* `CONNECT_CREATE` - create new connectors
* `CONNECT_EDIT` - edit, delete, pause, and restart connectors
* `ACL_EDIT` - create, edit, and delete ACLs

## Roles

Define a user role to which you would like to allow or deny access.

Can be a wildcard \(**\***\) to specify the policy is for all roles.

### Role Evaluation

To determine if a user has access to an action on a resource we gather the policies for all roles assigned to that user and evaluate them with the following logic:

![rbac\_evaluation\_logic.png](https://support.operatr.io/hc/article_attachments/900002827323/rbac_evaluation_logic.png)

## User Access Governance

Operatr captures all user actions in an audit log, this log is retained in an internal topic called `__oprtr_audit_log` with recent actions being shown in the Operatr UI.

The audit log captures requests and responses related to each user action, as well as the metadata associated with the request.

### Example Audit Record

Consider a request to create a new Kafka topic named `tx-events`.

Operatr has been configured with Github SSO and the following RBAC policy:

```text
policies:
  - resource: ["cluster", "Enpl9Kw4QK6pwK0LaRVssQ"]
    effect:   "Allow"
    actions:  ["TOPIC_INSPECT", "TOPIC_EDIT", "TOPIC_PRODUCE"]
    role:     "*"
```

The request to create Kafka topic `tx-events` will result in the following record on the `__oprtr_audit_log` topic:

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

## Role Mapping

Operatr integrates with a number of OpenID and SAML SSO providers. In order to configure RBAC, you must ensure that authenticated users contain role information.

### Github SSO

Refer to the [Github SSO and RBAC](https://support.operatr.io/hc/en-us/articles/900002019643) guide for details on configuring Github SSO.

#### Integration

When RBAC is enabled Operatr will request `orgs:read` scope to view the roles associated with an authenticated user.

![Screen\_Shot\_2020-08-07\_at\_12.03.11\_pm.png](https://support.operatr.io/hc/article_attachments/900002845523/Screen_Shot_2020-08-07_at_12.03.11_pm.png)

Github Organisation roles are restricted to `admin` or `member` so they are the two roles you can configure with Operatr RBAC when using Github SSO. 

When authenticating a user Operatr makes a request to the [GitHub API](https://developer.github.com/v3/orgs/members/#get-organization-membership-for-a-user) for user membership state and role information by querying  `GET /orgs/:org/memberships/:username`.

Specify the `github` key inside your `rbac-config.yaml` to define the Github Organisation to query for role information.

#### Configuration

In this example we grant `admin` users of the `operatr-io` Github Organisation actions `TOPIC_INSPECT` and `TOPIC_PRODUCE` for cluster `N9xnGujkR32eYxHICeaHuQ`.

```text
policies:
  - resource: ["cluster", "N9xnGujkR32eYxHICeaHuQ"]
    effect:   "Allow"
    actions:  ["TOPIC_INSPECT", "TOPIC_PRODUCE"]
    role:     "admin"

github:
  org: operatr-io
```

### Okta SSO \(OpenID\)

Refer to the [Okta SSO and RBAC](https://support.operatr.io/hc/en-us/articles/900002022006) guide for details on configuring Okta SSO.

#### Integration

When RBAC is enabled Operatr will request `groups` scope to view the groups associated with an authenticated user. Operatr considers Okta groups as roles in your RBAC configuration.

You will need to configure a relevant [group claim filter](https://developer.okta.com/docs/guides/customize-tokens-returned-from-okta/create-groups-claim/) for the Operatr OpenID integration:

### ![rbac-okta-group-filter.png](https://support.operatr.io/hc/article_attachments/900002891246/rbac-okta-group-filter.png)

### AWS SSO

Refer to the [AWS SSO and RBAC](https://support.operatr.io/hc/en-us/articles/900002022026) guide for details on configuring AWS SSO.

#### Integration

Edit the Operatr application within the AWS SSO dashboard and navigate to "Attribute Mappings".

Add the following `Roles` mapping to `${user:groups}`:

![aws-sso-attribute-mapping.png](https://support.operatr.io/hc/article_attachments/900002862383/aws-sso-attribute-mapping.png)

In this case, we are using a user's assigned groups as their role for Operatr RBAC configuration.

Each of the `Roles` in this example will have the value of the GUID of the AWS SSO group. You can find the GUID from the AWS console in the URL params:

![aws-sso-guid.png](https://support.operatr.io/hc/article_attachments/900002891266/aws-sso-guid.png)

**Note**: If you are using Active Directory or an external IdP as your identity source for AWS SSO you can use a [supported directory attribute](https://docs.aws.amazon.com/singlesignon/latest/userguide/attributemappingsconcept.html?icmpid=docs_sso_console) like `{dir:....}` that maps to your roles in your Active Directory deployment. For more info visit the [AWS documentation](https://docs.aws.amazon.com/singlesignon/latest/userguide/mapssoattributestocdattributes.html).

### Azure AD SSO

Refer to the [Azure AD SSO and RBAC](https://support.operatr.io/hc/en-us/articles/900002019783) guide for details on configuring AWS SSO.

#### Integration

Follow this [guide](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-enterprise-app-role-management) to populate `user.assignedroles`, then setup attribute claims within your Enterprise Application configuration like so:

![azure-attribute-claims.png](https://support.operatr.io/hc/article_attachments/900002862603/azure-attribute-claims.png)

**Note:** The default role `User` does not get passed as an assigned role in the SAMLResponse.

### SAML

Operatr can integrate with your SAML IdP as a service provider.

Roles are defined in a `Roles` attribute in the SAMLResponse from your IdP.

You can also provide an `Email` attribute which will be used as metadata in the audit log records.

#### Debugging SAML

Start Operatr with the environment variable `DEBUG_SAML=true` to debug SAML configurations.

This will log the `SAMLResponse` payload from your IdP. You can use a tool like [samltool.com](https://www.samltool.com/decode.php) to inspect and verify your IdP is correctly forwarding your configured claims/attributes.

Operatr provides an endpoint for inspecting the state of the currently authenticated user. `operatr_host/me` returns a JSON payload like:

```text
{"provider": "saml", 
 "email": "user@corp.com",
 "name": "User",
 "roles": ["admin"]}
```

