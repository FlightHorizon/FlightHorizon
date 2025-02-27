---
icon: list
description: System
---

# Lighting System

Lighting System is system that is responsible for managing global Lighting within the game environment.

## Current functions are:

* Change Sun/Moon position based on Global time
* Change Hues, Shadow Softness and other lighting settings with [time-dependent gradients](#user-content-fn-1)[^1].

## Configuration

[lightingconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/lightingconfiguration.md "mention") - Location: `ReplicatedStorage/Scripts/Configuration/LightingConfiguration`

## Scripts and components

* [daycyclemanager.md](../../../server-scripts/serverscriptservice/environment/daycyclemanager.md "mention") - Location: `ServerScriptService/Environment/DayCycleManager`
* [lightingmanager.md](../../../server-scripts/serverscriptservice/environment/lightingmanager.md "mention") - Location: `ServerScriptService/Environment/LightingManager`

### Interactions and functions:

(Simple)

* **DayCycleManager**  - Uses the builtin `.ClockTime` value of the `Lighting` Service to change the positions of Sun and Moon. Has no other interactions and does not use any other dependencies.
* **LightingManager**  - Based on configuration and  `.ClockTime` event it determines the lighting settings like: hue, shadow softness, etc. and assigns them for `Lighting` of the game environment. The Configuration is required.



[^1]: A time-dependent gradient is a function-based gradient where the output value changes over time. It acts as a graph with time as the x-axis (abscissa), allowing smooth transitions or animations based on elapsed time.
