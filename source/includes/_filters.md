# Introduction to Filters
All events can be filtered through the subscription system. Each event inherits all global filters, and implements multiple filters of their own. Use these filters to refine the events and data you receive.

> To specify a filter for an event, the general format is as follows.

```json
{
  "action":"subscribe",
  "event":"event_name",
  "filter_1":["item1","item2"],
  "filter_2":["item1"]
}
```

> filter_x represents any combination of filters under the "Filter Options" for each event. For example, to subscribe to Combat events for a specific Outfit:

```json
{
  "action":"subscribe",
  "event":"Combat",
  "outfits":["37510026483763654"]
}
```

# Global Filters and Subscription Options
## all
*"all": "true"*

Disables all event-specific filters for the specified event, therefore receiving all events for the given event type. As David from SOE describes it, "it's like drinking from a firehose of events"

## environments
*"environments": ["pc","ps4_us"]*

Only includes events from the selected platforms/environments. Valid values are “pc”, “ps4_us”, and “ps4_eu”.

## show
*"show": ["timestamp","facility_id"]*

Only include the provided fields from the event within the message.

## hide
*"hide": ["facility_id", "world_id"]*

Includes all fields except the provided fields from the event within the message.
NOTE: Overrides fields in **show**. If a field is in both **hide** and **show**, it will be **hidden** from the event's messages.

## useAND
*"useAND": ["property1", "property2"]*

By default, the server checks each property with an OR statement. This setting allows you to mark properties that have both an attacker and victim type as AND.

> VehicleCombat example: Getting air vehicle vs air vehicle combat
> Sent
```json
// This subscription would return all air vehicle kills where the attacking vehicle, OR the victim's vehicle were an air vehicle. So if an aircraft destroyed a tank, the event would still be sent to the client.
{
  "action":"subscribe",
  "event":"VehicleCombat",
  "vehicles":[ "7","8","9","10","11"]
}
```

> Sent
```json
//This subscription would return all air vehicle kills where the attacking vehicle, AND the victim's vehicle were an air vehicle. So if an aircraft destroyed a tank, the event would NOT be sent to the client.
{
  "action":"subscribe",
  "event":"VehicleCombat",
  "vehicles":["7","8","9","10","11"],
  "useAND":["vehicles"]
}
```