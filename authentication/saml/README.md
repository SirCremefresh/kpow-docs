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
*   `SAML_ACS_URL=` the **Single sign-on URL, **e.g.

    ```
    https://kpow.corp.com/saml
    ```
*   `SAML_METADATA_FILE=` the path to the **IDP metadata **file, e.g.

    ```
    /var/saml/saml-idp-metadata.xml
    ```
*   `SAML_CERT=` the path to the SAML certificate. \
    Note: This is optional, as it is most commonly bundled inside the IDP metdata XML

    ```
    /var/saml/saml-cert.pem
    ```

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
