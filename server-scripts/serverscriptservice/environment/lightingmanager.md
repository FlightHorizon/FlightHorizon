---
description: Script
icon: scroll
---

# LightingManager

## Part of the  [lighting-system.md](../../../systems/systems/environment/lighting-system.md "mention")

## Location: _`ServerScriptService/Environment/LightingManager`_

## Services and Dependencies

* `RunService`
* `Lighting`
* [lightingconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/lightingconfiguration.md "mention")

## Configurable Variables

`none`

## Functions

* `LerpColor(color1:Color3.fromRGB, color2:Color3.fromRGB, t:float)`

Function for linear interpolation of colors.

```lua
return color1:Lerp(color2, t)
```



* `Lerp(val1:float, val2:float, t:floar)`

Function for linear interpolation numbers with floating point.

```lua
return val1 + (val2 - val1) * t
```



* `getCurrentColor(timeOfDay:float, gradient:table)`

Function for getting the hue from specified gradient based on the time of the day. (can be used for getting hue of sun, shadow, etc.) works similar to `interpolateValue()` function described below.



* `interpolateValue(timeOfDay:float, gradient:table)`

Function is used to interpolate values from gradient based on time. Gradient has multiple timestamps and values connected to them so regular `Lerp()` function will not be suitable for this task on its own. This function finds 2 neighbors where current `timeOfDay`is between them and with a `Lerp()` function interpolates them.



## Main logic

All those functions are being called in Heartbeat event of RunService service for live update of the lighting.

```lua
runService.Heartbeat:Connect(function(deltaTime: number)
	-- update light's hue based on time
	local currentTime = lightinService.ClockTime

	-- Get colors for light
	local hue = getCurrentColor(currentTime, config.hueGradient)
	lightinService.ColorShift_Top = hue
	lightinService.ColorShift_Bottom = hue
	
	-- shadow colors
	local shadowHue = getCurrentColor(currentTime, config.shadowHueGradient)
	lightinService.Ambient = shadowHue
	lightinService.OutdoorAmbient = shadowHue
	
	-- shadow softness
	local shadowSoftness = interpolateValue(currentTime, config.shadowSoftnessGradient)
	lightinService.ShadowSoftness = shadowSoftness
	
	-- ray spread
	local raySpread = interpolateValue(currentTime, config.sunraySpreadGradient)
	SunRays.Spread = raySpread
	
	-- environmental diffuse
	local diffuseValue = interpolateValue(currentTime, config.environmentDiffuseGradient)
	lightinService.EnvironmentDiffuseScale = diffuseValue
	
	-- specular light
	local specularValue = interpolateValue(currentTime, config.environmentSpecularGradient)
	lightinService.EnvironmentSpecularScale = specularValue
end)
```

