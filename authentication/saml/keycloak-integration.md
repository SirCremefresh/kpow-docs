---
description: >-
  This integration configures SAML as the authentication mechanism, with
  Keycloak as the identity provider (IdP) and kPow as the service provider.
---

# Keycloak Integration

## Create a Keycloak application

1. Log in to your Keycloak account as an Administrator.
2. Go to **Clients** in the left menu, and click **Create**.
3.  Input the following details to the Add Client form:

    * For **Client ID**, enter a name for your App (eg "kpow"). Take note of this Client ID for the last step in LogonLabs.
    * For **Client Protocol**, select **saml**.
    * Click **Save**.



![](<../../.gitbook/assets/Screen Shot 2022-04-29 at 9.33.50 am.png>)

4\. While editing the application configure the following:

* Set **Sign Assertions** to **ON**.
* Set **Client Signature Required** to **OFF**.
* For **Valid Redirect URIs**, enter: "https://kpow.mycorp.io/saml" (where kpow.mycorp.io is the URL of where kPow is hosted)

![](<../../.gitbook/assets/Screen Shot 2022-04-29 at 9.36.29 am.png>)

6\. Go to "Realm Settings" in the main left menu and click **SAML 2.0 Identity Provider Metadata.** Download the XML file and keep for the next step.

![](<../../.gitbook/assets/Screen Shot 2022-04-29 at 9.38.55 am.png>)

## Configure kPow

Set the following environment variables and start kPow:

* `SAML_RELYING_PARTY_IDENTIFIER=kpow` this is the **Client ID** set in step 1
* `AUTH_PROVIDER_TYPE=saml`
*   `SAML_ACS_URL=` the **Valid Redirect URI** from before, **** e.g.

    ```
    https://kpow.corp.com/saml
    ```
*   `SAML_METADATA_FILE=` the path to the **SAML 2.0 Identity Provider Metadata** file from step 6, e.g.

    ```
    /var/saml/saml-idp-metadata.xml
    ```

kPow will now authenticate users with Keycloak (SAML).\


## User Authorization

1. Navigate to kPow's SAML client in Keycloak and go to the **Mappers** tab and click **Add Builtin**&#x20;
2. Select the built in mappers for **role list** and click **Add Selected**&#x20;

![](<../../.gitbook/assets/Screen Shot 2022-04-29 at 9.45.49 am.png>)

3\. Within your [RBAC yaml configuration](../../authorization/role-based-access-control.md#saml-integration-generic) add the following line:

```
saml:
  role_field: "Role"
```



