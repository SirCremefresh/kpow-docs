---
description: Troubleshoot the kPow UI and Reverse Proxies
---

# Websocket Connections

## kPow and Websockets

kPow populates the UI with data retrieved from the back-end kPow service via websockets.

In order to use the kPow UI your browser must be able to open a websocket connection to the kPow service. If there is a reverse proxy or firewall between your machine and the kPow service it must be configured to allow websocket traffic.

See the [Nginx example of required configuration to support websocket traffic.](http://nginx.org/en/docs/http/websocket.html)

