---
description: Common kPow Installation Issues and Resolutions.
---

# Troubleshooting

## UI Connection Issues

kPow populates the UI with data retrieved from the back-end service via websockets.

If your browser is unable to make a websocket connection to the kPow service you will see the error:

```text
Connection lost. Retrying in 5 seconds.
```

The most common cause of this error is a reverse-proxy between your machine and the kPow back-end service that has not been configured to allow websocket traffic. Firewalls may also block this traffic.

See our guide to [configuring a reverse-proxy to allow websocket traffic](../deployment-notes.md#reverse-proxies-load-balancers).

