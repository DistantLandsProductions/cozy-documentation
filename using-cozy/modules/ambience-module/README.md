---
icon: sun-dust
tags:
  - module
  - tutorial
  - api
  - biome
---

# Ambience Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyAmbienceModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

## Overview

The ambience module is a lightweight, secondary weather system designed to be used alongside the main weather module to add more variety to COZY.

### Not a Weather Module

The ambience module is _not_ a complete weather module, rather it is designed to operate alongside it. Here are some of the features that are not available in the Ambience module that are in the [weather-module](../weather-module/ "mention")

* Forecasting - ambience profiles are selected randomly based on the current weather and climate conditions
* Lateral Shifts - ambience profiles will never laterally shift to an adjacent profile
* Change Modes - ambience will only change when the previous profile completes

## Usage Examples

<details>

<summary>Change the Current Ambience</summary>

```csharp
// Get the ambience module
CozyAmbienceModule ambience = CozyWeather.Instance.Ambience;

ambience.SetAmbience(ambienceProfile);
```

</details>

<details>

<summary>Get the Current Ambience Profile</summary>

```csharp
// Get the ambience module
CozyAmbienceModule ambience = CozyWeather.Instance.Ambience;

// Get the current ambience profile
AmbienceProfile ambienceProfile = ambience.CurrentProfile
```

</details>

<details>

<summary>Listen for Ambience Change Events</summary>

```csharp
void OnChange(AmbienceProfile oldProfile, AmbienceProfile newProfile)
{
    Debug.Log($"Ambience is changing from {oldProfile.name} to {newProfile.name}");
}

void OnEnable() 
{
    CozyWeather.Instance.Ambience.OnAmbienceChange += OnChange;
}

void OnDisable() 
{
    CozyWeather.Instance.Ambience.OnAmbienceChange -= OnChange;
}
```

</details>

## Biome Integration

Biomes can also have a fully featured ambience module.

## API

### Interfaces

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3><i class="fa-sun-dust">:sun-dust:</i></h3></td><td align="center">IAmbienceModule</td><td><a href="../weather-module/iweathermodule.md">iweathermodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-forward-fast">:forward-fast:</i></h3></td><td align="center">ISkippable</td><td><a href="../extra-interfaces/iskippable.md">iskippable.md</a></td></tr></tbody></table>
