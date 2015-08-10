# Status Actions

These actions return information/data that might be useful if you are reconnecting and missed the original associated event.

## activeMetagameEvents

Returns all active metagame events/alerts (and their respective facilities) across all servers. Optionally, you can provide an array of world_id's to get metagame event information for only the specified servers.

<aside class="warning">
If a world does not contain any running metagame events, it WILL NOT appear in the worlds node.
</aside>

> Sent

```json
{
    "action": "activeMetagameEvents", "worlds": ["1002"]
}
```

> Response
> (Please note this has been truncated, the facilities and metagame_events arrays have much more than 1 element)

```json
{
    "action":"activeMetagameEvents",
    "worlds":
    {
        "1002":
        {
            "metagame_events":
            [
                {
                    "instance_id":"303",
                    "metagame_event_type_id":"4",
                    "facility_type_id":"0",
                    "category_id":"1",
                    "zone_id":"4",
                    "start_time":"1439216803",
                    "end_time":"1439224003",
                    "control_vs":"28",
                    "control_nc":"37",
                    "control_tr":"34",
                    "facilities":
                    [
                        {
                            "facility_id":"307010",
                            "facility_type_id":"6",
                            "owner":"2",
                            "zone_id":"4"
                        }
                    ]
                }
            ]
        }
    }
}
```

### Sent Payload

| Field  | JSON Type    | Description                                                                                                                                  |
|--------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| action | String       | The action we want to perform. In this case, activeMetagameEvents.                                                                           |
| worlds | String/Array | (Optional) A single or list of worlds that you want Metagame info for. Not specifying any worlds gets all metagame events across all worlds. |

### Response Payload

### root node

| Field | JSON Type | Description |
|------------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| action | String | An echo of the action that generated "worlds" |
| worlds | Object | The parent node containing all worlds which have metagame events (and were inside "worlds" if specified in the sent request) |

### metagame_events node

| Field | JSON Type | Description |
|------------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| instance_id | String | Represents the WORLD unique instance ID of this metagame event. This is not globally unique, and can clash with other servers/worlds. Use this to match up start/update/end metagame events that come through the "MetagameEvent" subscription. Matches the ["instance_id" found on Census](https://census.daybreakgames.com/get/ps2:v2/world_event/?type=METAGAME&c:limit=1) |
| metagame_event_type_id | String | Represents the type of this metagame. Matches the ["metagame_event_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/metagame_event/?c:limit=1000). |
| facility_type_id | String | Represents the facility type for facility metagame events. Returns "0" if metagame event is not facility type specific, otherwise returns the relating facility type. Matches the ["facility_type_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/facility_type/?c:limit=1000). |
| category_id | String | Represents the Magic "type" value given to metagame events by census. Matches the ["type" found on Census](http://census.daybreakgames.com/get/ps2:v2/metagame_event/?c:limit=1000). |
| zone_id | String | Represents the zone relating to this metagame event. Returns "0" if metagame event is global, otherwise returns the related zone. Matches the ["zone_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000). |
| start_time | String | Represents the epoch time (in seconds) when this metagame event started. |
| end_time | String | Represents the epoch time (in seconds) when the metagame event IS EXPECTED to end. |
| control_xx | String | Represents the rounded down territory control percentage from 0-100. |
| facilities | Array | Represents all facilities that contribute/have influence for this metagame event. |

### facilities node

| Field | JSON Type | Description |
|------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| facility_id | String | Represents the unique ID of this facility. Matches the ["region_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/region/?c:limit=1000). |
| facility_type_id | String | Represents the type of this facility (Bio-lab, Outpost, etc). Matches the ["facility_type_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/facility_type/?c:limit=1000) for this region. |
| owner | String | Represents the owner of this facility. Matches the ["faction_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/faction/?c:limit=1000) |
| zone_id | String | Represents the zone this facility is located in. Matches the ["zone_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000) |