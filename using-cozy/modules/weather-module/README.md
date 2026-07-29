---
icon: clouds
tags:
  - module
  - tutorial
  - api
  - biome
---

# Weather Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyWeatherModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

## Overview

The weather module is the core engine that drives the changing weather in COZY. It takes static data from a [forecast-profile.md](../../profiles/forecast-profile.md "mention") and several [weather-profile.md](../../profiles/weather-profile.md "mention") to play weather FX, schedule new weather, and pass data to where it needs to go.

### Preview Weather

During edit mode, weather profiles can be previewed by selecting a weather profile at the top of the inspector

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### Forecasting

Forecasting is handled by the [forecast-profile.md](../../profiles/forecast-profile.md "mention"). This is covered in depth in the [forecasting.md](../../utilities/forecasting.md "mention") section.

### Initialization Behavior

The weather module has a few different modes that determine what happens when the game starts.

<table><thead><tr><th width="231.33331298828125">Name</th><th>Behavior</th></tr></thead><tbody><tr><td>Set Random Weather</td><td>Set a random weather profile when the game loads</td></tr><tr><td>Set Weather</td><td>Set a specific weather profile when the game loads</td></tr><tr><td>Set Forecast</td><td>Adds a list of weather profiles (one after another) to the forecast in sequence.</td></tr></tbody></table>

### Weather Change Mode

Set the scenario that will enact a weather change.

<table><thead><tr><th width="274.6666259765625">Name</th><th>Behavior</th></tr></thead><tbody><tr><td>Change when weather finishes</td><td>The weather will change when the current weather profile's timer is complete</td></tr><tr><td>Change daily</td><td>Change weather once a day at a specific time</td></tr><tr><td>Change via Scripting</td><td>Only change when the ProgressWeather() or SetWeather() method is called</td></tr></tbody></table>

### Next Weather Selection Mode

Selecting the next weather can be done through a variety of methods.

<table><thead><tr><th width="231.33331298828125">Name</th><th>Behavior</th></tr></thead><tbody><tr><td>Forecast</td><td>Use the forecast profile to determine an appropriate weather profile</td></tr><tr><td>Random</td><td>Select a random weather profile next</td></tr><tr><td>Weighted Random</td><td>Select a random weather profile based on their <a data-mention href="../../utilities/chance.md">chance.md</a></td></tr><tr><td>Change Via Scripting</td><td>Use the QueueWeather() function to add weather to the forecast directly.</td></tr></tbody></table>

## Usage Examples

<details>

<summary>Set the Current Weather </summary>

```csharp
// Sets the current weather
CozyWeather.Instance.Weather.SetWeather(yourProfile);
```

</details>

<details>

<summary>Get the Time Before Weather Changes</summary>

```csharp
// Get the time till the weather changes in MeridiemTimeDelta format
MeridiemTimeDelta timeTillWeatherChange = CozyWeather.Instance.Weather.WeatherTimer;
```

</details>

<details>

<summary>Get the Current Weather</summary>

```csharp
// Get the current weather profile
WeatherProfile currentWeather = CozyWeather.Instance.Weather.CurrentWeather;

// To get the current local weather (before biomes are applied), use the local parameter
WeatherProfile currentLocalWeather = CozyWeather.Instance.Weather.CurrentLocalWeather;
```

</details>

<details>

<summary>Listen for weather change events</summary>

```csharp
void OnWeatherChange(WeatherProfile oldProfile, WeatherProfile newProfile)
{
    Debug.Log($"Weather is changing from {oldProfile.name} to {newProfile.name}");
}

void OnEnable() 
{
    CozyWeather.Instance.Weather.OnWeatherChange += OnWeatherChange;
}

void OnDisable() 
{
    CozyWeather.Instance.Weather.OnWeatherChange -= OnWeatherChange;
}
```

</details>



## Widgets

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th><select><option value="OBED6ZmA2lxZ" label="Small" color="blue"></option><option value="FZGc4BhztoCa" label="Medium" color="blue"></option><option value="CC3yrvOgAGU1" label="Large" color="blue"></option></select></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h2>Current Weather</h2></td><td><span data-option="FZGc4BhztoCa">Medium</span></td><td>Select the current preview weather</td><td><a href="../../../.gitbook/assets/20260729-0051-22.3764269.gif">20260729-0051-22.3764269.gif</a></td></tr></tbody></table>

## Biome Integration

Biomes can also have a fully featured weather module.

## API

### Interfaces

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3><i class="fa-clouds">:clouds:</i></h3></td><td align="center">IWeatherModule</td><td><a href="iweathermodule.md">iweathermodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-forward-fast">:forward-fast:</i></h3></td><td align="center">ISkippable</td><td><a href="../extra-interfaces/iskippable.md">iskippable.md</a></td></tr></tbody></table>
