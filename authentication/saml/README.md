---
description: Integration guides for SAML and OpenID
---

# SAML

kPow can integrate with your SAML IdP of choice.

We have integration guides for common providers:

* [Okta](okta-integration.md)
* [AWS SSO](aws-sso-integration.md)
* [Azure AD](azure-ad-integration.md)

## Generic configuration

* `AUTH_PROVIDER_TYPE=saml`
* `SAML_RELYING_PARTY_IDENTIFIER=` the **Audience URI (SP Entity ID)**
*   `SAML_ACS_URL=` the **Single sign-on URL,** e.g.

    ```
    https://kpow.corp.com/saml
    ```
*   `SAML_METADATA_FILE=` the path to the **IDP metadata** file, e.g.

    ```
    /var/saml/saml-idp-metadata.xml
    ```
*   `SAML_CERT=` the path to the SAML certificate. \
    Note: This is optional, as it is most commonly bundled inside the IDP metdata XML

    ```
    /var/saml/saml-cert.pem
    ```

### SAML and Path-Proxied kPow

{% hint style="success" %}
Set **`AUTH_LANDING_URI`**` ``` when running kPow at a proxied path.
{% endhint %}

Often our users configure kPow behind a [reverse proxy at a specific path](../../installation/deployment-notes.md#custom-path-configuration), e.g.

`https://tools.your-corp/kafka/kpow`

When kPow is proxied to a specific host/path we need to set the `AUTH_LANDING_URI` to that same path so the post-login redirect process can work properly, e.g.

`AUTH_LANDING_URI=https://tools.your-corp/kafka/kpow`

### Debugging SAML

Start kPow with the environment variable `DEBUG_SAML=true` to debug SAML configurations.

This will log the `SAMLResponse` payload from your IdP. You can use a tool like [samltool.com](https://www.samltool.com/decode.php) to inspect and verify your IdP is correctly forwarding your configured claims/attributes.

kPow provides an endpoint for inspecting the state of the currently authenticated user. `kpow_host/me` returns a JSON payload like:

```
{"provider": "saml", 
 "email": "user@corp.com",
 "name": "User",
 "roles": ["admin"]}
```
