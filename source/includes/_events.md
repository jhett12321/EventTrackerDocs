# Event Subscription/Payload Summary
## Service Events (No Subscriptions/Filtering - Messages are always sent)
### ConnectionStateChange

> ConnectionStateChange - Example Response

```json
{
    "service" : "ps2_events",
    "version" : "1.0.3",
    "websocket_event" : "connectionStateChange",
    "online" : "true"
}
```

Sent upon successful connection to the websocket service.

### ServiceStateChange

> ServiceStateChange - Example Response

```json
{
  "payload":
  {
    "online":"0",
    "world_id":"13"
  },
  "event_type":"ServiceStateChange"
}
```

Sent upon connection to indicate the status of worlds (servers), and when servers go offline, or census experiences difficulties.

## Custom Events

### PopulationChange

> PopulationChange - Subscription Options

```json
{
  "action": "subscribe",
  "event": "PopulationChange",
  "all": "false",
  "population_types": ["total", "world", "zone", "outfit", "zone_outfit"],
  "outfits": ["37524301022235903"],
  "zones": ["8"],
  "worlds": ["13"]
}
```

> PopulationChange - Example Response

```json
{
  "payload":
  {
	"population_type":"zone_outfit",
	"population_total":"1",
	"outfit_id":"37524301022235903",
	"zone_id":"8",
	"world_id":"13"
  },
  "event_type":"PopulationChange"
}
```

Called every time population changes.

Use the "population_type" filter to get online world, zone and outfit population.

<aside class="notice">
The "total" population type will give total population for an environment. Combine these environment values to get total population across all platforms.
</aside>

## Extended Standard Events

### AchievementEarned

> AchievementEarned - Subscription Options

```json
{
  "action": "subscribe",
  "event": "AchievementEarned",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "achievements": ["2", "6"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> AchievementEarned - Example Response

```json
{
  "payload":
  {
	"character_id":"5428196144902462561",
	"character_name":"StickyTapeProfit",
	"outfit_id":"37528083641406998",
	"faction_id":"1",
	"achievement_id":"90022",
	"timestamp":"1424785275",
	"zone_id":"2",
	"world_id":"1"
  },
  "event_type":"AchievementEarned"
}
```

"The given character has earned a new achievement (medal or ribbon)"

### BattleRank (Census: BattleRankUp)

> BattleRank - Subscription Options

```json
{
  "action": "subscribe",
  "event": "BattleRank",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "battle_ranks": ["90", "95"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> BattleRank - Example Response

```json
{
  "payload":
  {
	"character_id":"8258686574497087089",
	"character_name":"lchSeheDich",
	"outfit_id":"37517800549394039",
	"faction_id":"1",
	"battle_rank":"6",
	"timestamp":"1424785325",
	"zone_id":"6",
	"world_id":"13"
  },
  "event_type":"BattleRank"
}
```

"The given character has achieved a new battle rank."

### Combat (Census: Death)

> Combat - Subscription Options

```json
{
  "action": "subscribe",
  "event": "Combat",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "loadouts": ["5", "6"],
  "vehicles": ["7", "8"],
  "weapons": ["98"],
  "headshots": ["1"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> Combat - Example Response

```json
{
  "payload":
  {
	"attacker_character_id":"8258686574496803233",
	"attacker_character_name":"Neigler",
	"attacker_outfit_id":"0",
	"attacker_faction_id":"1",
	"attacker_loadout_id":"20",
	"victim_character_id":"8257461498430035057",
	"victim_character_name":"Carlwiecarl",
	"victim_outfit_id":"0",
	"victim_faction_id":"3",
	"victim_loadout_id":"12",
	"weapon_id":"86",
	"fire_mode_id":"127",
	"vehicle_id":"0",
	"is_headshot":"0",
	"timestamp":"1424785517",
	"zone_id":"2",
	"world_id":"10"
  },
  "event_type":"Combat"
}
```

"The given character has been killed."

### ContinentLock

> ContinentLock - Subscription Options

```json
{
  "action": "subscribe",
  "event": "ContinentLock",
  "all": "false",
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> ContinentLock - Example Response

```json
{
  "payload":
  {
	"vs_population":"33",
	"nc_population":"33",
	"tr_population":"33",
	"locked_by":"2",
	"metagame_event_id":"2",
	"timestamp":"1424785639"
	"zone_id":"6",
	"world_id":"17"
  },
  "event_type":"ContinentLock"
}
```

"A continent has been locked."

### ContinentUnlock

> ContinentUnlock - Subscription Options

```json
{
  "action": "subscribe",
  "event": "ContinentUnlock",
  "all": "false",
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> ContinentUnlock - Example Response

```json
{
  "payload":
  {
	"vs_population":"33",
	"nc_population":"33",
	"tr_population":"33",
	"unlocked_by":"2",
	"metagame_event_id":"2",
	"timestamp":"1424785639"
	"zone_id":"6",
	"world_id":"17"
  },
  "event_type":"ContinentUnlock"
}
```

"A continent has been unlocked."

### ExperienceEarned (Census: GainExperience)

> ExperienceEarned - Subscription Options

```json
{
  "action": "subscribe",
  "event": "ExperienceEarned",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "experience_types": ["7", "8"],
  "loadouts": ["5", "6"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> ExperienceEarned - Example Response

```json
{
  "payload":
  {
	"amount":"6",
	"character_id":"5428123302638686705",
	"character_name":"lNighterl",
	"outfit_id":"37509675644678161",
	"faction_id":"1",
	"experience_id":"93",
	"loadout_id":"19",
	"other_id":"174225795038838914",
	"timestamp":"1424785639",
	"zone_id":"8",
	"world_id":"13"
  },
  "event_type":"ExperienceEarned"
}
```

"A player has gained experience. Match experience_id with http://census.daybreakgames.com/get/ps2/experience to find out what they did. Field other_id may refer to another player, or a vehicle, etc."

### FacilityControl (Census: FacilityControl)

> FacilityControl - Subscription Options

```json
{
  "action": "subscribe",
  "event": "FacilityControl",
  "all": "false",
  "facilities": ["2222", "4519"],
  "facility_types": ["7", "8"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "captures": ["1"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> FacilityControl - Example Response

```json
{
  "payload":
  {
	"facility_id":"222060",
	"facility_type_id":"6",
	"outfit_id":"37509488620601614",
	"duration_held":"691",
	"new_faction_id":"1",
	"old_faction_id":"1",
	"is_capture":"1",
	"control_vs":"37",
	"control_nc":"25",
	"control_tr":"37",
	"timestamp":"1424785690",
	"zone_id":"6",
	"world_id":"17"
  },
  "event_type":"FacilityControl"
}
```

"A facility has changed hands."

### Login (Census: PlayerLogin, PlayerLogout)

> Login - Subscription Options

```json
{
  "action": "subscribe",
  "event": "Login",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "is_login": ["1"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> Login - Example Response

```json
{
  "payload":
  {
	"character_id":"8256737736841511857",
	"character_name":"KaBzZz",
	"outfit_id":"37509528949546300",
	"faction_id":"1",
	"is_login":"1",
	"timestamp":"1424785740",
	"world_id":"13"
  },
  "event_type":"Login"
}
```

"A character has logged in, or out of the game."

### MetagameEvent (Census: MetagameEvent)

> MetagameEvent - Subscription Options

```json
{
  "action": "subscribe",
  "event": "MetagameEvent",
  "all": "false",
  "metagames": ["111112222", "23333444323"],
  "metagame_types": ["3", "4"],
  "statuses": ["1", "0"],
  "dominations": ["1"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> MetagameEvent - Example Response

```json
{
  "payload":
  {
	"instance_id":"4278",
	"type_id":"1",
	"start_time":"1424779839",
	"end_time":"0",
	"timestamp":"1424785835",
	"status":"2",
	"control_vs":"63",
	"control_nc":"23",
	"control_tr":"13",
	"domination":"0",
	"zone_id":"2",
	"world_id":"1"
  },
  "event_type":"MetagameEvent"
}
```

"A metagame event (alert) has started or ended."

### PlayerFacilityControl (Census: PlayerFacilityCapture, PlayerFacilityDefend)

> PlayerFacilityControl - Subscription Options

```json
{
  "action": "subscribe",
  "event": "PlayerFacilityControl",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "facilities": ["2222", "4519"],
  "captures": ["1"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> PlayerFacilityControl - Example Response

```json
{
  "payload":
  {
    "character_id":"5428100110522400353",
    "character_name":"SYD2842",
    "outfit_id":"37524390589257254",
    "faction_id":"2",
    "facility_id":"222190",
    "is_capture":"0",
    "timestamp":"1429725298",
    "zone_id":"6",
    "world_id":"13"
  },
  "event_type":"PlayerFacilityControl"
}
```

"A player has taken part in the capture, or defense of a facility."

### VehicleDestroy (Census: VehicleDestroy)

> VehicleDestroy - Subscription Options

```json
{
  "action": "subscribe",
  "event": "VehicleDestroy",
  "all": "false",
  "characters": ["111112222", "23333444323"],
  "outfits": ["3333", "111111"],
  "factions": ["1", "2"],
  "loadouts": ["5", "6"],
  "vehicles": ["7", "8"],
  "weapons": ["98"],
  "facilities": ["4444"],
  "zones": ["2", "4"],
  "worlds": ["25"]
}
```

> VehicleDestroy - Example Response

```json
{
  "payload":
  {
    "character_id":"5428100110522400353",
    "character_name":"SYD2842",
    "outfit_id":"37524390589257254",
    "faction_id":"2",
    "facility_id":"222190",
    "is_capture":"0",
    "timestamp":"1429725298",
    "zone_id":"6",
    "world_id":"13"
  },
  "event_type":"PlayerFacilityControl"
}
```

"A vehicle has been destroyed."