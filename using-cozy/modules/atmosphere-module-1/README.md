---
description: Implements IWindModule
icon: image
tags:
  - module
  - tutorial
  - api
  - biome
---

# Wind Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyWindModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

## Overview

The Wind Module sends COZY's current information to various wind systems.

* [Wind Zone](https://docs.unity3d.com/6000.5/Documentation/Manual/class-WindZone.html)
* [Zephyr](https://assetstore.unity.com/packages/tools/particles-effects/zephyr-dynamic-wind-system-348514?aid=1011luj9X)
* Generic Shaders

## Usage Examples

<details>

<summary>Access Current Wind Direction</summary>

```csharp
// Get the atmosphere module
CozyWindModule windModule = CozyWeather.Instance.Wind;

// Get specific values
Vector3 dir = windModule.WindDirection;
```

</details>

<details>

<summary>Send COZY Wind Information to a Shader</summary>

In the shaders section of the Wind module UI, add a new global shader property

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

Then, set a property name based on your shader's global variables and assign a type.&#x20;

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

COZY will then update the global variable of that name based on the wind value at runtime.

</details>

## Widgets

<table data-view="cards"><thead><tr><th></th><th><select><option value="OBED6ZmA2lxZ" label="Small" color="blue"></option><option value="FZGc4BhztoCa" label="Medium" color="blue"></option><option value="CC3yrvOgAGU1" label="Large" color="blue"></option></select></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h3>Wind Direction</h3></td><td><span data-option="OBED6ZmA2lxZ">Small</span></td><td>Tells the heading of the wind along with the +/- offset</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (34).png">image (34).png</a></td></tr></tbody></table>

## Biome Integration

The Wind Module fully supports COZY's biome system. Each biome can define its own wind settings (heading, etc.) and are blended between based on the biome weight

## API

### Interfaces

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3>IWindModule</h3></td><td align="center">The standard interface for wind management</td><td><a href="../atmosphere-module/iatmospheremodule.md">iatmospheremodule.md</a></td></tr></tbody></table>
