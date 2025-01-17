---
description: Secure kPow with Github SSO (OAuth2) and RBAC
---

# GitHub

{% hint style="warning" %}
Configure RBAC and set the organisation field to restrict access to your organisation.
{% endhint %}

## User Authentication

### Create a Github OAuth2 Application

1. Login to [GitHub](https://github.com/) and navigate to the organisation you wish to integrate with kPow.
2. Navigate to **Settings > Developer Settings > OAuth Apps > New Oath Application**
3. Fill out the **Register a new OAuth application** form:
   * **Application Name**: The name of your kPow instance, e.g. 'kPow Staging'.
   * **Homepage URL**: The absolute URL to your kPow instance, e.g.\
     `https://kpow.stage.mycorp.com`
   * **Authorization callback URL**: The absolute URL for authorization callback, e.g.\
     `https://kpow.stage.mycorp.com/oauth2/github/callback`
4. Open your freshly created OAuth App and make note of the **Client ID** and **Client Secret**.

### Integrate kPow with Github OAuth2

Set the following environment variables and start kPow:

* `AUTH_PROVIDER_TYPE=github`
*   `OPENID_AUTH_URI=` The URI to authorize Github users, e.g.

    ```
    https://github.com/login/oauth/authorize, or
    [Github Enterprise Host]/login/oauth/authorize
    ```
*   `OPENID_TOKEN_URI=` The URI to retrieve an OAuth token, e.g.

    ```
    https://github.com/login/oauth/access_token, or
    [Github Enterprise Host]/login/oauth/access_token
    ```
*   `GITHUB_API_ENDPOINT=` The URI to perform user actions, e.g.

    ```
    https://api.github.com/, or
    [Github Enterprise Host]/api/v3/
    ```
* `OPENID_CLIENT_ID=` the **Client ID** found in the OAuth Apps page (required)
* `OPENID_CLIENT_SECRET=` the **Client Secret** found in the OAuth Apps page (required)
*   `AUTH_LANDING_URI=` The absolute kPow URI, e.g.

    ```
    https://kpow.stage.mycorp.org
    ```

kPow will now authenticate users with Github via OAuth2.

## User Authorization

See the guide to [Role Based Access Control](../../authorization/role-based-access-control.md) for full configuration details.

### Integrate Github SSO and RBAC

When RBAC is enabled kPow will request `orgs:read` scope to view a user's roles.

![](<../../.gitbook/assets/Screen Shot 2020-08-07 at 12.03.11 pm.png>)

### Default Github Roles

Github Organisation roles are restricted to `admin` or `member` so they are the two default roles you can configure with kPow RBAC when using Github SSO.&#x20;

kPow makes a request to the [GitHub API](https://developer.github.com/v3/orgs/members/#get-organization-membership-for-a-user) for user membership state and role information by querying  `GET /orgs/:org/memberships/:username`. Specify the `github` key inside your `rbac-config.yaml` to define the Github Organisation to query for role information, and optional role\_field to use.

### Using Github Teams for Roles

{% hint style="info" %}
**Note**: Github Teams configuration requires extra OAuth scopes: `user` and `repo`&#x20;
{% endhint %}

kPow can use the [teams](https://docs.github.com/en/rest/reference/teams) associated with the authenticated user as roles in kPow. You can do this by specifying a custom `roles_field` in the RBAC yaml:

```
# Specifically restrict Auth to a single Github Organization
# Specify that a user's teams field should be used to identify roles
github:
  org: operatr-io
  role_field: teams
```

Once enabled, kPow will use the [list teams API call](https://docs.github.com/en/rest/reference/teams#list-teams-for-the-authenticated-user) to query for roles.&#x20;

### Configuration

This sample configuration specifies:

* Who may access kPow
* Which users are kPow admins
* What RBAC policies are in place
* Access is restricted to one Github organisation
* Github Teams are used as user-roles for RBAC

See: [Role Based Access Control](../../authorization/role-based-access-control.md) for more information.

```
# Allow all users who can authenticate access to kPow
authorized_roles:
  - "*"
  
# Specify that users with 'admin' role are kPow Admins  
admin_roles:
  - "admin"
  
# Define some RBAC policies
policies:
  - resource: ["cluster", "N9xnGujkR32eYxHICeaHuQ"]
    effect:   "Allow"
    actions:  ["TOPIC_INSPECT", "TOPIC_PRODUCE"]
    role:     "admin"

# Specifically restrict Auth to a single Github Organization
# Specify that a user's teams field should be used to identify roles
github:
  org: operatr-io
  role_field: teams
```
