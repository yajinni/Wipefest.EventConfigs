# Examples

These examples should help you understand the format of an event config.
Feel free to dive into the [specification](specification.md)
if you need more details about each property.

## Ability

Ability events are used to show that an actor has cast an ability,
and take the form:

```json
{
  "id": "DH",
  "name": "Divine Hymn",
  "tags": [ "priest", "holy" ],
  "show": true,
  "eventType": "ability",
  "filter": {
    "type": "cast",
    "ability": {
      "id": 64843
    }
  }
}
```

In English, this would read:

<pre>
The <b>ability</b> event "<b>Divine Hymn</b>" happens when a <b>cast</b> event has an ability id of <b>64843</b>.
</pre>

The *Warcraft Logs* query that this event config generates is:

<pre>
type = '<b>cast</b>' and ability.id = <b>64843</b>
</pre>

*Warcraft Logs* then returns [these events](https://www.warcraftlogs.com/reports/cJtAzp6k8G2fTCNm#fight=8&view=events&pins=2%24Off%24%23909049%24expression%24type%20%3D%20'cast'%20and%20ability.id%20%3D%2064843).

*Wipefest* adds these events to its timeline
and makes them filterable under the name **Divine Hymn**,
under the heading **priest** and subheading **holy**.

When the timeline initially loads, these events **will show** by default (`"show": true`).

### Multiple spells

You can filter to multiple spells using the **filter.ability.ids** property.

For example, on *High Antoran Command*,
*Felshield Emitter* has a different spell id on mythic than heroic.
We can use a single event config to cover both difficulties by specifying both spell ids:

```json
{
  "id": "FE",
  "name": "Felshield Emitter",
  "tags": [ "player", "ability" ],
  "show": false,
  "eventType": "ability",
  "friendly": true,
  "filter": {
    "type": "cast",
    "ability": {
      "ids": [ 244902, 255140 ]
    }
  }
}
```

The *Warcraft Logs* query that this event config generates is:

<pre>
type = '<b>cast</b>' and ability.id in (<b>244902</b>, <b>255140</b>)
</pre>

Note also the use of `"show": false` to indicate that we don't want these events
to be shown by default when the timeline initially loads.

We have also indicated `"friendly": true` to override the default
and force this event to appear on the left-hand side of the timeline,
because it is an event that the raid has some control over.

### showTarget

Often, the *target* of a cast is important information.
When this is the case,
we can format the event title as "*X casts Y on Z*"
by setting the **showTarget** property to *true*.

For example, we would not only want to know when *Guardian Spirit* is cast,
but who it is cast on:

```json
{
  "id": "GS",
  "name": "Guardian Spirit",
  "tags": [ "priest", "holy" ],
  "show": true,
  "showTarget": true,
  "eventType": "ability",
  "filter": {
    "type": "cast",
    "ability": {
      "id": 47788
    }
  }
}
```

Avoid using **showTarget** when it doesn't provide much meaningful information.

## Buff / Debuff

### Debuff

We often want to know when an actor gains a buff or debuff.
For this, we use the *debuff* **eventType**.

The main difference we see changing from *ability* **eventType** to *debuff* **eventType**
is the way that *Wipefest* formats the title of the event:

* *ability*: X casts Y
* *debuff*: X gains Y

This example brings back the events where players were feared by *Weight of Darkness*
on *Felhounds of Sargeras*:

```json
{
  "id": "0E",
  "name": "Weight of Darkness (Fear)",
  "tags": [ "player", "debuff" ],
  "show": true,
  "eventType": "debuff",
  "friendly": true,
  "filter": {
    "type": "applydebuff",
    "ability": {
      "id": 244071
    }
  }
}
```

In English, this would read:

<pre>
The <b>debuff</b> event "<b>Weight of Darkness (Fear)</b>" happens when an <b>applydebuff</b> event has an ability id of <b>244071</b>.
</pre>

The *Warcraft Logs* query that this event config generates is:

<pre>
type = '<b>applydebuff</b>' and ability.id = <b>244071</b>
</pre>

*Warcraft Logs* then returns [these events](https://www.warcraftlogs.com/reports/DvFYmpzcBGa46VxJ#fight=9&view=events&pins=2%24Off%24%23244F4B%24expression%24type%20%3D%20'applydebuff'%20and%20ability.id%20%3D%20244071).

*Wipefest* adds these events to its timeline
and makes them filterable under the name **Weight of Darkness (Fear)**,
under the heading **player** and subheading **debuff**.

When the timeline initially loads, these events **will show** by default (`"show": true`).

These events will load on the **left**-hand side of the timeline (`"friendly": true`),
because the raid has some control over whether players get feared or not.

### Buff

Buff events also take the title format "*X gains Y*",
so we also use the *debuff* **eventType** here.

The main difference is that the **filter.type** will be different
(*applybuff* instead of *applydebuff*).

This event config targets events where actors gain the *Spirit of Redemption* buff:

```json
{
  "id": "S1",
  "name": "Spirit of Redemption",
  "tags": [ "priest", "holy" ],
  "show": true,
  "eventType": "debuff",
  "friendly": true,
  "filter": {
    "type": "applybuff",
    "ability": {
      "id": 27827
    }
  }
}
```

### Remove buff / debuff

If we want the event title to be of the form "*X loses Y*",
we use the *removedebuff* **eventType**.

The **filter.type** will also change to *removebuff* / *removedebuff*.

This example targets events where actors *lose* the *Spirit of Redemption* buff:

```json
{
  "id": "S2",
  "name": "Spirit of Redemption (Removed)",
  "tags": [ "priest", "holy" ],
  "show": true,
  "eventType": "removedebuff",
  "friendly": true,
  "filter": {
    "type": "removebuff",
    "ability": {
      "id": 27827
    }
  }
}
```

The convention is to append "*(Removed)*" to the **name** of the event config
for *removedebuff* **eventTypes**.