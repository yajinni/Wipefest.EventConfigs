## Specification

An event config can have a fair few possible properties, but a small handful of them cover most use cases.
This page exists to document each property and what it can be used for.

* [Identifiers](#Identifiers)
  * [id](#id-string)
  * [name](#name-string)
* [Basic configuration](#Basic-configuration) (covers 95% of use cases)
  * [tags](#tags-string)
  * [show](#show-boolean)
  * [eventType](#eventType-string)
  * [friendly](#friendly-boolean)
  * [filter](#filter-Filter)
    * [type](#filter.type-string)
    * [types](#filter.types-string)
    * [ability](#filter.ability-FilterAbility)
      * [id](#filter.ability.id-number)
      * [ids](#filter.ability.ids-number)
* Further configuration (to cover 99% of use cases)
  * difficulties
  * filter
    * actor
      * id
      * name
    * first
    * firstPerInstance
    * index
    * minimum
    * range
    * rangePerActor
    * stack
    * query
  * target
  * showTarget
  * includePetTargets
  * source
  * showSource
  * title
* Rare configuration
  * timestamp
  * timestamps
  * titles
  * collapsed
  * icon
  * style

### Identifiers

#### id (*string*)

* [x] Required

A **2-character** string that must be unique within the event config group (boss / specialization).

Should be URL friendly (convention is for upper case letters and digits).

#### name: (*string*)

* [x] Required

A friendly name for the event. This is used in the left-hand filter menu.

If multiple event configs have the same name **and** tags,
their events will be combined into the same "row" in the left-hand filter menu
(so they are filtered on/off at the same time).
This is mostly just used for stacking tank debuffs as the "debuff" and "debuffstack" events usually want to be combined.

### Basic Configuration

#### tags (*string[]*)

* [x] Required

These tags help to organise the filters in the left-hand filter menu.
The first tag will be the main heading. for that filter group,
and the second tag will be the subheading.

For bosses, the first tag is typically "boss" / "player" / "raid" / "spawn",
and the second tag is typically "ability" / "buff" / "debuff" / "damage" / "interrupt".

#### show (*boolean*)

* Default: *false*

This property determines whether, on initial page load,
the event is shown (*true*) or filtered (*false*).

Be careful not to have too many events defaulting to be shown,
as the timeline can easily get cluttered with lots of frequent events
that the user isn't necessarily concerned about.

#### eventType (*string*)

* [x] Required

**eventType** mostly determines what the event title says.
For example, an *ability* event typically reads "X cast Y on Z",
but a *debuff* event might read "X applied Y to Z".

Valid values:

* ability
* debuff*
* debuffstack*
* removedebuff*
* damage
* interrupt
* phase
* spawn
* title

**debuff* / *debuffstack* / *removedebuff* events can also be used for buffs.

#### friendly (*boolean*)

* Default: *depends on the source/target of the event and the eventType*

**friendly** determines which side of the timeline the event title will appear.
Events on the left should be events that the raid had *some* control over,
and should have a **friendly** value of *true*.
Events on the right should be events that the raid didn't have *much* control over,
and should have a **friendly** value of *false*.

**friendly** also determines the phrasing of the event title.
For example, a friendly *debuff* event might read "X gains Y from Z",
and an unfriendly *debuff* event might read "Z applied Y to X".

If the default value of **friendly** is not correct, then simply override it by setting this property.

#### filter (*Filter*)

The **filter** determines which *Warcraft Logs* events are used to create *Wipefest* events.
Most of the time, one *Warcraft Logs* event will become one *Wipefest* event,
but there are also **filter** properties that will allow you to collapse several
*Warcraft Logs* events into a single *Wipefest* event.

##### > filter.type (*string*)

* [x] Required (Unless **filter.types** is specified)

**filter.type** refers to the *Warcraft Logs* type of the event.
These types are listed under *Built-in Identifiers* on [this page](https://www.warcraftlogs.com/help/pins),
but the main ones you will need to use are:

* begincast
* cast
* damage
* absorbed
* applybuff
* applydebuff
* applybuffstack
* applydebuffstack
* removebuff
* removedebuff
* interrupt

##### > filter.types (*string[]*)

* [x] Required (Unless **filter.type** is specified)

You can specify that you want to filter to multiple *Warcraft Logs* types
using the **filter.types** array instead of **filter.type**.

For example, a *Wipefest* *damage* **eventType** will often filter to both
*damage* and *absorb* *Warcraft Logs* types,
so as to include events where a player was hit but absorbed all of the damage:

```json
{
  "id": "AI",
  "name": "Alone in the Darkness",
  "tags": [ "player", "damage" ],
  "show": true,
  "eventType": "damage",
  "friendly": true,
  "showSource": false,
  "filter": {
    "types": [ "damage", "absorb" ],
    "ability": {
      "id": 243963
    }
  }
}
```

##### > filter.ability (*FilterAbility*)

As well as the *type* of the *Warcraft Logs* event,
*Wipefest* needs to know what *ability* to filter to.

###### > > filter.ability.id (*number*)

* [x] Required (Unless **filter.ability.ids** is specified)

**filter.ability.id** is the numeric *World of Warcraft* spell ID for that ability.
This is the same ID that is used in *Weak Auras*, *Warcraft Logs*, *WoWDB*, *Wowhead* etc.

###### > > filter.ability.ids (*number[]*)

* [x] Required (Unless **filter.ability.id** is specified)

To filter to multiple abilities, specify their ids in the **filter.ability.ids** array,
instead of using **filter.ability.id**.