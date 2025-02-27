---
icon: scroll
description: Script
---

# DayCycleManager

## Part of the  [lighting-system.md](../../../systems/systems/environment/lighting-system.md "mention")

## Location: _`ServerScriptService/Environment/DayCycleManager`_

## Services and Dependencies

* `RunService`
* `Lighting`

## Configurable Variables

* `dayLength` - Represents the day cycle length **in seconds.**

## Functions

* `UpdateTime(deltaTime:number)`

The function calculates the next `.ClockTime` value based on previous one and `dayLength` setting. Then it assigns it to the `Lighting` of the environment. Function is called in `RunService.HeartBeat` event  to repeatedly update the clock.
