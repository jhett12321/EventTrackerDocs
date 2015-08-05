---
title: Planetside 2 Extended Census API Documentation

language_tabs:
  - javascript

toc_footers:
  - <a href='mailto:api@blackfeatherproductions.com'>Sign Up for a API Key</a>

includes:
  - errors

search: true
---

# Welcome!
Welcome to the Extended Planetside 2 Census API Documentation! Here, you will find

## API Status/Downtime Notices

<aside class="notice">
API Service is operating normally.
</aside>

## API Keys & API Support/Requests
For those interested in writing applications using the API, please email <a href='mailto:api@blackfeatherproductions.com'>api@blackfeatherproductions.com</a> with information regarding your application, to receive your API Key. If you are experiencing issues with the service, or have a feature/improvement request, please remember to provide your API key when contacting us. You will typically receive a response within 48 hours.

## Connecting to the API/Authetication
The Extended Census Websocket uses API keys for authentication and access (which you can get from above). The API key "example" can also be used for experimenting with the API, although use of this key may be limited in the future.

<aside class="notice">
Always use your API key in production applications. Do not use "example".
</aside>

1: Open a websocket connection to: ws://push.api.blackfeatherproductions.com/?apikey=example

```javascript
    // Open Websocket Connection
    var apiKey = "example";
    var url = "ws://push.api.blackfeatherproductions.com/?apikey=" + apiKey;
    ws = new WebSocket(url);
```

2: You will receive some messages confirming your websocket connection, and the status of Census websocket feeds.

```javascript
    // Set event handlers.
    ws.onopen = function(evt)
    {
        console.log("Websocket Connection Established!");
    };
    ws.onmessage = function(evt)
    {
        // All messages sent by the API are JSON. Parse it so we can work with it.
        var data = JSON.parse(evt.data);
        if(data.websocket_event != undefined && data.websocket_event == "connectionStateChange")
        {
            // We are now connected. Do stuff.
        }
    };
    ws.onclose = function(evt)
    {
        console.log("Websocket Connection Closed.");
    };
    ws.onerror = function(evt)
    {
        console.log("Websocket Error: " + evt.data);
    };
```

> Connection Message

```json
{
    "service":"ps2_events",
    "version":"1.4.5",
    "websocket_event":"connectionStateChange",
    "online":"true"
}
```

3: You will also receive several ServiceStateChange messages detailing the status of census websocket feeds. More on this in the Service Events section.

> ServiceState Messages.

```json
{
    "payload":
    {
        "online":"1",
        "world_id":"2002"
    },
    "event_type":"ServiceStateChange"
}
```

4: Send messages to the server using the actions, events and filters listed below as a guideline.