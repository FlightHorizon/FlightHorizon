# Lighting System

Lighting System is system that is responsible for managing global Lighting withing the game environment.

## Current functions are:

* Change Sun/Moon position based on Global time
* Change Hues, Shadow Softness and other lighting settings with [time-dependent gradients](#user-content-fn-1)[^1].

## Configuration

### Location:

`ReplicatedStorage/Scripts/Configuration/LightingConfiguration`

### Configuration Description:

Configuration contains sections that mainly represent [time-dependent gradients ](#user-content-fn-1)[^1]

Sections that it currently contains and their formats:

* **hueGradient** - Format: _`{time: number, color: Color3.fromRBG}`_
* **shadowHueGradient** - Format: _`{time: number, color: Color3.fromRBG}`_
* **environmentDiffuseGradient** - Format: _`{time: number, value: number}`_
* **environmentSpecularGradient** - Format: _`{time: number, value: number}`_
* **shadowSoftnessGradient** - Format: _`{time: number, value: number}`_
* **sunraySpreadGradient** - Format: _`{time: number, value: number}`_

## Scripts

* [daycyclemanager.md](../../../server-scripts/serverscriptservice/environment/daycyclemanager.md "mention") - Location: ServerScriptService/Environment/DayCycleManager
* LightingManager - Location: ServerScriptService/Environment/LightingManager



[^1]: A time-dependent gradient is a function-based gradient where the output value changes over time. It acts as a graph with time as the x-axis (abscissa), allowing smooth transitions or animations based on elapsed time.
