# Status Actions

These actions return information/data that might be useful if you are reconnecting and missed the original associated event.

## activeMetagameEvents (previously activeAlerts)

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
> (Please note this has been truncated, the facilities and metagame_events arrays have more than 1 element)

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
| worlds | String/Array | (Optional) A single or list of world ID's ([PC](http://census.daybreakgames.com/get/ps2:v2/world/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/world/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/world/?c:limit=1000)) that you want Metagame info for. Not specifying any worlds gets all metagame events across all worlds. |

### Response Payload

### root node

| Field | JSON Type | Description |
|------------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| action | String | An echo of the action that generated "worlds" |
| worlds | Object | The parent node containing all worlds valid for the sent request. JSON keys/properties match the "world_id" found on Census ([PC](http://census.daybreakgames.com/get/ps2:v2/world/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/world/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/world/?c:limit=1000)). |

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
| control_xx | String | Represents the rounded down territory control percentage from 0-100 for faction "xx". "control_vs", "control_nc" and "control_tr" represent each factions territory control. |
| facilities | Array | Represents all facilities that contribute/have influence for this metagame event. |

### facilities node

| Field | JSON Type | Description |
|------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| facility_id | String | Represents the unique ID of this facility. Matches the ["region_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/region/?c:limit=1000). |
| facility_type_id | String | Represents the type of this facility (Bio-lab, Outpost, etc). Matches the ["facility_type_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/facility_type/?c:limit=1000) for this region. |
| owner | String | Represents the owner of this facility. Matches the ["faction_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/faction/?c:limit=1000) |
| zone_id | String | Represents the zone this facility is located in. Matches the ["zone_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000) |

## worldStatus (Previously zoneStatus/facilityStatus)

Returns zone (territory control, lock) and facility information (ownership) for the given world/zones.

> Sent

```json
{
    "action": "worldStatus", "worlds": ["25"], "zones": ["2"]
}
```

> Response
> (Please note this has been truncated, the worlds, zones and facilites arrays can contain more than 1 element, depending on the query.)

```json
{
    "action":"worldStatus",
    "worlds":
    {
        "25":
        {
            "zones":
            {
                "2":
                {
                    "locked":"0",
                    "locked_by":"0",
                    "control_vs":"28",
                    "control_nc":"27",
                    "control_tr":"44",
                    "facilities":
                    [
                        {
                            "facility_id":"4430",
                            "facility_type_id":"6",
                            "owner":"3",
                            "zone_id":"2"
                        }
                    ]
                }
            }
        }
    }
}
```

### Sent Payload

| Field | JSON Type | Description |
|--------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| action | String | The action we want to perform. In this case, worldStatus. |
| worlds | String/Array | (Optional) A single or list of world ID's ([PC](http://census.daybreakgames.com/get/ps2:v2/world/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/world/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/world/?c:limit=1000)) that you want zone/facility info for. Not specifying any worlds gets data from all worlds. |
| zones | String/Array | (Optional) A single or list of zone ID's ([PC](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/zone/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/zone/?c:limit=1000)) that you want zone/facility info for. Not specifying any zones gets data from all zones. |

### Response Payload

### root node

| Field | JSON Type | Description |
|--------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| action | String | An echo of the action that generated "worlds" |
| worlds | Object | The parent node containing all worlds valid for the sent request. JSON keys/properties match the "world_id" found on Census ([PC](http://census.daybreakgames.com/get/ps2:v2/world/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/world/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/world/?c:limit=1000)). |

### xx world ID node

| Field | JSON Type | Description |
|--------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| zones | Object | The parent node containing all zones valid for the sent request. JSON keys/properties match the "zone_id" found on Census ([PC](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000) [PS4-US](http://census.daybreakgames.com/get/ps2ps4us:v2/zone/?c:limit=1000) [PS4-EU](http://census.daybreakgames.com/get/ps2ps4eu:v2/zone/?c:limit=1000)). |

### zones node

| Field | JSON Type | Description |
|------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| locked | String | Represents whether this zone is locked. "0" indicates the zone is unlocked, "1" indicates the zone is locked. |
| locked_by | String | Represents the faction who locked this zone. If the zone is not locked, this returns "0". Matches the ["faction_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/faction/?c:limit=1000) |
| control_xx | String | Represents the rounded down territory control percentage from 0-100 for faction "xx". "control_vs", "control_nc" and "control_tr" represent each factions territory control. |
| facilities | Array | Represents all facilities inside this zone. |

### facilities node

| Field | JSON Type | Description |
|------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| facility_id | String | Represents the unique ID of this facility. Matches the ["region_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/region/?c:limit=1000). |
| facility_type_id | String | Represents the type of this facility (Bio-lab, Outpost, etc). Matches the ["facility_type_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/facility_type/?c:limit=1000) for this region. |
| owner | String | Represents the owner of this facility. Matches the ["faction_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/faction/?c:limit=1000) |
| zone_id | String | Represents the zone this facility is located in. Matches the ["zone_id" found on Census](http://census.daybreakgames.com/get/ps2:v2/zone/?c:limit=1000) |