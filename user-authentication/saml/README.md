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
* `SAML_RELYING_PARTY_IDENTIFIER=` the **Audience URI \(SP Entity ID\)**
* `SAML_ACS_URL=` the **Single sign-on URL,** e.g.

  ```text
  https://kpow.corp.com/saml
  ```

* `SAML_METADATA_FILE=` the path to the **IDP metadata** file, e.g.

  ```text
  /var/saml/saml-idp-metadata.xml
  ```

* `SAML_CERT=` the path to the SAML certificate.   
  Note: This is optional, as it is most commonly bundled inside the IDP metdata XML

  ```text
  /var/saml/saml-cert.pem
  ```

### Debugging SAML

If you would like to debug SAML while setting up the integration, you can set the environment variable `DEBUG_SAML=true`

This will log the SAMLAssertion payload and other interactions which can be used to verify that kPow is correctly parsing your assertions.

