# Subscription Actions

> Sending a message to the server.

```javascript
//The API is ready to receive messages.
var message =
{
	"action": "subscribe",
	"event": "BattleRank",
	"battle_ranks": ["100"]
};
ws.send(JSON.stringify(message));

console.log("Now listening for Battle Rank 100 events.");
```

These actions are used to manage your event PUSH subscriptions. You will receive a JSON formatted confirmation message with your current subscriptions, and events will be sent to you as they happen.

## subscribe

> Sent

```json
{
    "action": "subscribe",
    "event": "BattleRank",
    "battle_ranks": ["11"]
}
```

> Response

```json
{
    "subscriptions":
    {
        "BattleRank":
        {
            "characters":[],
            "outfits":[],
            "factions":[],
            "battle_ranks":["11"],
            "zones":[],
            "worlds":{},
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        }
    },
    "action":"subscribe"
}
```

This is the probably the most common action. Use it to add filtered events to your subscription.

<aside class="notice">
"field_xx" represents any combination of fields for an event. For more information on the filter system, see the  <a href="#filters">Filter Section</a>.
</aside>

<aside class="notice">
Subscriptions are additive, but please note that each event DOES NOT share the same filter list for each event. (i.e. specifying worlds for 1 event will not set worlds for all other subscriptions.)
</aside>

**Sent Payload**

| Field    | JSON Type    | Description                                                     |
|----------|--------------|-----------------------------------------------------------------|
| action   | String       | The action we want to perform. In this case, subscribe.         |
| event    | String       | The event that contains the fields we want to unsubscribe from. |
| field_xx | String/Array | The field, and associated value/s to add to the subscription.   |

**Response Payload**

| Field         | JSON Type | Description                                                                                 |
|---------------|-----------|---------------------------------------------------------------------------------------------|
| subscriptions | Object    | Contains a mapped list of your current subscriptions, and their respective filtered fields. |
| action        | String    | An echo of the action that modified "subscriptions".                                        |

## unsubscribe

> Sent

```json
{
    "action": "subscribe",
    "event": "BattleRank",
    "battle_ranks": ["11","12"]
}
```

> Response

```json
{
    "subscriptions":
    {
        "BattleRank":
        {
            "characters":[],
            "outfits":[],
            "factions":[],
            "battle_ranks":["11","12"],
            "zones":[],
            "worlds":{},
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        }
    },
    "action":"subscribe"
}
```

> Sent

```json
{
    "action": "unsubscribe",
    "event": "BattleRank",
    "battle_ranks": ["11"]
}
```

> Response

```json
{
    "subscriptions":
    {
        "BattleRank":
        {
            "characters":[],
            "outfits":[],
            "factions":[],
            "battle_ranks":["12"],
            "zones":[],
            "worlds":{},
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        }
    },
    "action":"subscribe"
}
```

Allows you to remove entries from an existing subscription.

**Sent Payload**

| Field    | JSON Type    | Description                                                        |
|----------|--------------|--------------------------------------------------------------------|
| action   | String       | The action we want to perform. In this case, unsubscribe.          |
| event    | String       | The event that contains the fields we want to unsubscribe from.    |
| field_xx | String/Array | The field, and associated value/s to remove from the subscription. |

**Response Payload**

| Field         | JSON Type | Description                                                                                 |
|---------------|-----------|---------------------------------------------------------------------------------------------|
| subscriptions | Object    | Contains a mapped list of your current subscriptions, and their respective filtered fields. |
| action        | String    | An echo of the action that modified "subscriptions".                                        |


##unsubscribeAll

> Sent

```json
{
    "action": "subscribe",
    "event": "BattleRank",
    "battle_ranks": ["11"]
}
```

> Sent

```json
{
    "action": "subscribe",
    "event": "Combat",
    "vehicles": ["7"]
}
```

> Response

```json
{
    "subscriptions":
    {
        "BattleRank":
        {
            "characters":[],
            "outfits":[],
            "factions":[],
            "battle_ranks":["11"],
            "zones":[],
            "worlds":{ },
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        },
        "Combat":{
            "characters":[],
            "outfits":[],
            "factions":[],
            "loadouts":[],
            "vehicles":["7"],
            "weapons":[],
            "headshots":[],
            "zones":[],
            "worlds":{},
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        }
    },
    "action":"subscribe"
}
```

> Sent

```json
{
    "action": "unsubscribeAll",
    "event": "Combat"
}
```

> Response

```json
{
    "subscriptions":
    {
        "BattleRank":
        {
            "characters":[],
            "outfits":[],
            "factions":[],
            "battle_ranks":["11"],
            "zones":[],
            "worlds":{},
            "useAND":[],
            "all":"false",
            "environments":[],
            "show":[],
            "hide":[]
        }
    },
    "action":"unsubscribeAll"
}
```

Allows you to clear all subscribed events, both globally and on an event level.

**Sent Payload**

| Field  | JSON Type | Description                                                                                                            |
|--------|-----------|------------------------------------------------------------------------------------------------------------------------|
| action | String    | The action we want to perform. In this case, unsubscribeAll.                                                           |
| event  | String    | (Optional) The event that you wish to remove all subscriptions from. Not specifying an event clears all subscriptions. |

**Response Payload**

| Field         | JSON Type | Description                                                                                 |
|---------------|-----------|---------------------------------------------------------------------------------------------|
| subscriptions | Object    | Contains a mapped list of your current subscriptions, and their respective filtered fields. |
| action        | String    | An echo of the action that modified "subscriptions".                                        |