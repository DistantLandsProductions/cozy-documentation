---
icon: temperature-low
tags:
  - module
  - tutorial
  - api
  - biome
---

# Climate Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyClimateModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

## Overview

The climate module is responsible for holding and changing the current [temperature.md](../../../under-the-hood/data-structures/climate/temperature.md "mention"), [humidity.md](../../../under-the-hood/data-structures/climate/humidity.md "mention"), [pressure.md](../../../under-the-hood/data-structures/climate/pressure.md "mention"), [uv-index.md](../../../under-the-hood/data-structures/climate/uv-index.md "mention"), and [air-quality.md](../../../under-the-hood/data-structures/climate/air-quality.md "mention").

### Precipitation Chance

You can either use a calculated or manually set precipitation chance. To learn more about how the rain chance is calculated see [precipitation-chance.md](../../../under-the-hood/data-structures/climate/precipitation-chance.md "mention").

### Seasons

The climate module sets the current information ([temperature.md](../../../under-the-hood/data-structures/climate/temperature.md "mention"), [humidity.md](../../../under-the-hood/data-structures/climate/humidity.md "mention"), [pressure.md](../../../under-the-hood/data-structures/climate/pressure.md "mention"), etc.) based on [season.md](../../../under-the-hood/data-structures/climate/season.md "mention")s that are setup on the module. These are designed to be static and interpolated between at runtime.

<figure><img src="../../../.gitbook/assets/image (31).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
COZY only supports 4 seasons
{% endhint %}

Each season lets you control 5 properties to set the climate during that season. Each property can be expanded to set several additional properties.

<figure><img src="../../../.gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

#### Average High/Low

Set the baseline for the average min and max for a value. These are _not_ hard limits and may be exceeded in certain situations.

#### Diurnal Curve

Set a curve that interpolates the value between the high and low values throughout the day. The x-axis represents the day percentage and the y-axis lerps between the low and high values (0 is low, 1 is high).

#### Variation Type/Amplitude/Period

Variation adds an offset to the property based on a curve. You can set the variation type to either sine or noise. The amplitude sets the +/- intensity of the variation and the period spreads out the variation.

## Usage Examples

<details>

<summary>Get Current Season</summary>

```csharp
// Grab the current season module. In this case, this is the Climate module
ISeasonModule seasonsModule = CozyWeather.Instance.Seasons;

SeasonName seasonName = seasonsModule.CurrentSeason;

// If you want to access the data of the current season, you need to pass the
// seasonName back into the climate module to get the info from the profile.
CozyWeather.Instance.GetModule(out ClimateModule climate);
Season season = climate.climateProfile.GetSeason(seasonName);
```

</details>

<details>

<summary>Get Snow/Rain Accumulation</summary>

COZY does not ship with a snow accumulation shader out of the box, but can be used as a manager for any third party accumulation system.

To get the current snow and rain accumulated, you can use this snippet

```csharp
// Grab the current precipitation accumulation module
IPrecipitationModule accumulation = CozyWeather.Instance.Precipitation;

Accumulation snowAmount = accumulation.AccumulatedSnow;
Accumulation rainAmount = accumulation.AccumulatedRain;
```

</details>



## Widgets

<table data-view="cards"><thead><tr><th></th><th><select><option value="OBED6ZmA2lxZ" label="Small" color="blue"></option><option value="FZGc4BhztoCa" label="Medium" color="blue"></option><option value="CC3yrvOgAGU1" label="Large" color="blue"></option></select></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h4>Current Temperature</h4></td><td><span data-option="FZGc4BhztoCa">Medium</span></td><td>Displays the current <a data-mention href="../../../under-the-hood/data-structures/climate/temperature.md">temperature.md</a> and the high and low today.</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (27).png">image (27).png</a></td></tr><tr><td><h3>Current Humidity</h3></td><td><span data-option="FZGc4BhztoCa">Medium</span></td><td>Displays the current <a data-mention href="../../../under-the-hood/data-structures/climate/humidity.md">humidity.md</a> and the high and low today.</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (28).png">image (28).png</a></td></tr><tr><td><h4>Precipitation Chance</h4></td><td><span data-option="FZGc4BhztoCa">Medium</span></td><td>Displays the current stratiform and convective <a data-mention href="../../../under-the-hood/data-structures/climate/precipitation-chance.md">precipitation-chance.md</a></td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (29).png">image (29).png</a></td></tr><tr><td><h3>Current Pressure</h3></td><td><span data-option="OBED6ZmA2lxZ">Small</span></td><td>Displays the current <a data-mention href="../../../under-the-hood/data-structures/climate/pressure.md">pressure.md</a> and the high and low today.</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (30).png">image (30).png</a></td></tr></tbody></table>

## Biome Integration

The Climate module supports local offset volumes that let you offset the global temperature, humidity, etc. by a set value.&#x20;

<figure><img src="../../../.gitbook/assets/image (26).png" alt="" width="563"><figcaption></figcaption></figure>

***

## API

### Properties

<table><thead><tr><th width="218.99993896484375">Name</th><th width="144.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="ZNAD0ac2Urqp" label="AtmosphereParameters" color="blue"></option><option value="ksE4BNxkLF9Y" label="Vector3" color="blue"></option><option value="0TudOX4NH3gX" label="Light" color="blue"></option><option value="3AkRONAIwfwI" label="ClimateSnapshot" color="blue"></option><option value="qHu98Nabm7Tt" label="MeridiemDate" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>HottestDayOfTheYear</td><td><span data-option="qHu98Nabm7Tt">MeridiemDate</span></td><td>Get the hottest day of the year</td></tr><tr><td>ColdestDayOfTheYear</td><td><span data-option="qHu98Nabm7Tt">MeridiemDate</span></td><td>Get the coldest day of the year</td></tr></tbody></table>

### Interfaces

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3><i class="fa-temperature-arrow-down">:temperature-arrow-down:</i></h3></td><td align="center">IClimateModule</td><td><a href="iclimatemodule.md">iclimatemodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-raindrops">:raindrops:</i></h3></td><td align="center">IPrecipitationModule</td><td><a href="iprecipitationmodule.md">iprecipitationmodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-calendar">:calendar:</i></h3></td><td align="center">ISeasonModule</td><td><a href="iseasonmodule.md">iseasonmodule.md</a></td></tr></tbody></table>
