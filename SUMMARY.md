# Table of contents

* [kPow User Guide](README.md)

## About

* [Introduction](about/introduction.md)
* [Our Team](about/our-team.md)
* [Releases](about/releases.md)
* [Trials and Licenses](about/trials-and-licenses.md)
* [Support](about/support.md)
* [Data Collection](about/data-collection.md)

## Installation

* [Quick Start](installation/quick-start.md)
* [System Requirements](installation/system-requirements.md)
* [Deployment Notes](installation/deployment-notes.md)
* [Minimum ACL Permissions](installation/minimum-acl-permissions.md)
* [Application Logs](installation/application-logs.md)
* [OpenShift](installation/openshift.md)
* [AWS Marketplace](installation/aws-marketplace.md)
* [Troubleshooting](installation/troubleshooting.md)

## Configuration <a href="#config" id="config"></a>

* [Environment Variables](config/environment-variables.md)
* [Kafka Cluster](config/kafka-cluster.md)
* [Schema Registry](config/schema-registry.md)
* [Kafka Connect](config/kafka-connect/README.md)
  * [Confluent Managed Connect](config/kafka-connect/confluent-managed-connect.md)
* [Multi-Cluster Management](config/multi-cluster.md)
* [Azure Event Hubs](config/azure-event-hubs.md)
* [Confluent Cloud](config/confluent-cloud.md)
* [Redpanda](config/redpanda.md)
* [MSK](config/msk.md)

## User Authentication <a href="#authentication" id="authentication"></a>

* [Overview](authentication/overview.md)
* [LdapLoginModule](authentication/ldap.md)
* [PropertyFileLoginModule](authentication/file.md)
* [JDBCLoginModule](authentication/db.md)
* [OpenID/OAuth 2.0](authentication/openid/README.md)
  * [GitHub](authentication/openid/github.md)
  * [Okta](authentication/openid/okta.md)
* [SAML](authentication/saml/README.md)
  * [Okta integration](authentication/saml/okta-integration.md)
  * [AWS SSO integration](authentication/saml/aws-sso-integration.md)
  * [Azure AD integration](authentication/saml/azure-ad-integration.md)
  * [Keycloak Integration](authentication/saml/keycloak-integration.md)

## User Authorization <a href="#authorization" id="authorization"></a>

* [Overview](authorization/overview.md)
* [Simple Access Control](authorization/simple-access-control.md)
* [Role Based Access Control](authorization/role-based-access-control.md)
* [Multi-Tenancy](authorization/tenants.md)
* [Administration](authorization/administration/README.md)
  * [Temporary Policies](authorization/administration/temporary-policies.md)
  * [Staged Mutations](authorization/administration/staged-mutations.md)

## Features

* [Kafka Streams](features/kafka-streams.md)
* [Data Governance (Audit Log)](features/data-governance.md)
* [Data Policies](features/data-policies.md)
* [HTTPS Connections](features/https-connections.md)
* [Live Mode](features/live-mode.md)
* [Data Inspect](features/data-inspect/README.md)
  * [Streaming Search](features/data-inspect/streaming-search.md)
  * [kJQ Filters](features/data-inspect/kjq-filters.md)
  * [Serdes](features/data-inspect/serdes.md)
* [Data Produce](features/data-produce.md)
* [Prometheus Integration](features/prometheus/README.md)
  * [Metrics Glossary](features/prometheus/metrics-glossary.md)
* [Slack Integration](features/slack-integration.md)

## Kafka Management <a href="#mutations" id="mutations"></a>

* [Topics](mutations/topic-actions.md)
* [Groups](mutations/group-actions.md)
* [Brokers](mutations/broker-actions.md)
* [ACLs](mutations/acl-actions.md)
* [Connect](mutations/connect-actions.md)
* [Schema Registry](mutations/schema-actions.md)
