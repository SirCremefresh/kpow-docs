---
description: Secure the kPow UI with HTTPS
---

# HTTPS Connections

## Overview

kPow supports SSL termination at the instance without a reverse proxy.

Once configured all content is served via HTTPS, meaning you must update any configured integrations including Prometheus scrapers, SSO providers (e.g. `OPENID_LANDING_URI` and callback-urls within the provider) as **https://**.

## Configuration

kPow is powered by **Jetty** which uses Java KeyStores (JKS) to manage certificates.

Refer to the **** [**Jetty documentation**](https://www.eclipse.org/jetty/documentation/jetty-10/operations-guide/index.html#og-keystore) for instructions on using the JDK keytool or OpenSSL to create and import certificates (e.g. a `.pem` file) into a KeyStore.

Set the following environment variable and start kPow with SSL connections.

* `ENABLE_HTTPS=true` Once set kPow will serve HTTPS traffic on the configured UI `PORT`
*   `HTTPS_KEYSTORE=` The location of your KeyStore, e.g.

    ```
    /var/certs/keystore.jks
    ```
* `HTTPS_KEYSTORE_TYPE=` The type of KeyStore (eg, `PKCS12`).
* `HTTPS_KEYSTORE_PASSWORD=` The password of the KeyStore.
*   `HTTPS_TRUSTSTORE=` - (optional) The location of your Truststore e.g.

    ```
    /var/certs/truststore.jks
    ```
* `HTTPS_TRUSTSTORE_TYPE=` (optional) The type of TrustStore.
* `HTTPS_TRUSTSTORE_PASSWORD=` (optional) The password of the TrustStore.
