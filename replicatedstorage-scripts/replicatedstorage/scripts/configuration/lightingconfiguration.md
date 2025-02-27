---
description: Configuration
icon: gear-code
---

# LightingConfiguration

## It is part of [lighting-system.md](../../../../systems/systems/environment/lighting-system.md "mention")

### Location:

`ReplicatedStorage/Scripts/Configuration/LightingConfiguration`

### Configuration Description:

Configuration contains sections that mainly represent [time-dependent gradients ](#user-content-fn-1)[^1]

Sections that it currently contains and their formats:

* hueGradient - Format: _`[{time: number, color: Color3.fromRBG},]`_&#x20;
* shadowHueGradient - Format: _`[{time: number, color: Color3.fromRBG},]`_
* environmentDiffuseGradient - Format: _`[{time: number, value: number},]`_
* environmentSpecularGradient - Format: _`[{time: number, value: number},]`_
* shadowSoftnessGradient - Format: _`[{time: number, value: number},]`_
* sunraySpreadGradient - Format: _`[{time: number, value: number},]`_

[^1]: A time-dependent gradient is a function-based gradient where the output value changes over time. It acts as a graph with time as the x-axis (abscissa), allowing smooth transitions or animations based on elapsed time.
