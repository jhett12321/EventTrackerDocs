# Welcome!
<aside class="success">
All API Services are operating normally.
</aside>

<aside class="error">
<b>DEPRECATION NOTICE: Current Status Actions</b></br>
Support for all current status actions will be DROPPED in the upcoming 1.5 update.
</aside>

Welcome to the Extended Planetside 2 Census API Documentation! Here, you will find documented examples and JSON formats for the various feeds provided by the API service, and the additional subscription/filter features that you can use to customize the events you receive.

## API Keys & API Support/Requests
For those interested in writing applications using the API, please email <a href='mailto:api@blackfeatherproductions.com'>api@blackfeatherproductions.com</a> with information regarding your application, to receive your API Key. If you are experiencing issues with the service, or have a feature/improvement request, please remember to provide your API key when contacting us. You will typically receive a response within 48 hours.

## Connecting to the API/Authetication

> Connecting to the API

```javascript
// Open Websocket Connection
var apiKey = "example";
var url = "ws://push.api.blackfeatherproductions.com/?apikey=" + apiKey;
ws = new WebSocket(url);

// Set event handlers.
ws.onopen = function(evt)
{
	console.log("Websocket Connection Established!");
};
ws.onmessage = function(evt)
{
	// All messages sent by the API are JSON. Parse it so we can work with it.
	var data = JSON.parse(evt.data);
	if(data.websocket_event != undefined && data.websocket_event == "connectionStateChange" && data.online == "true")
	{
	    console.log("Websocket API Ready.");
		//The API is ready to receive messages.
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

> After connecting, you will receive a ConnectionStateChange message.

```json
{
    "service":"ps2_events",
    "version":"1.4.5",
    "websocket_event":"connectionStateChange",
    "online":"true"
}
```

> ... and a ServiceStateChange event for each world, indicating their online status.

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

The Extended Census Websocket uses API keys for authentication and access (which you can get via emailing us). The API key "example" can also be used for experimenting with the API, although use of this key may be limited in the future.

<aside class="notice">
Always use your API key in production applications. Do not use "example".
</aside>

1: Open a websocket connection to: ws://push.api.blackfeatherproductions.com/?apikey=example

2: You will receive some messages confirming your websocket connection, and the status of Census websocket feeds.

3: You will also receive several ServiceStateChange messages detailing the status of census websocket feeds. More on this in the Service Events section.

4: Send messages to the server using the actions, events and filters listed below as a guideline.