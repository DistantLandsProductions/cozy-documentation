---
icon: calendar-days
---

# Climate Data & Ranges

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/ClimateRanges.cs" class="button secondary" data-icon="code">View on GitHub</a>

The climate data structs—`ClimateRanges`, `DailyRange<T, D>`, `ClimateSnapshot`, and `Season`—handle the complex, time-based variations of climate properties. They manage everything from small daily fluctuations (like temperature drops at night) to large-scale seasonal shifts.

## Usage Examples

<details>

<summary>Evaluating Daily Variation</summary>

```csharp
using DistantLands.Cozy;
using UnityEngine;

// Assuming you have a populated DailyRange and a current date
DailyRange<Temperature, TemperatureDelta> tempRange = currentSeason.climateInformation.temperature;
MeridiemDate currentDate = myWeatherSphere.currentDate;
int seed = 12345;

// Calculate how much the temperature varies at this specific date and time
float currentVariation = tempRange.GetVariation(currentDate, seed);
```

</details>

<details>

<summary>Accessing a Climate Snapshot</summary>

```csharp
// Snapshots hold the exact current values for the climate at a specific moment
ClimateSnapshot currentClimate = new ClimateSnapshot 
{
    temperature = 25f,
    humidity = 50f,
    season = SeasonName.Summer
};

// Use the snapshot to drive gameplay mechanics
if (currentClimate.season == SeasonName.Summer && currentClimate.temperature > 30f)
{
    Debug.Log("It's a hot summer day!");
}
```

</details>

## API

### `DailyRange<T, D>` Fields

<table><thead><tr><th width="180">Field</th><th width="150">Type<select><option value="id_t" label="T" color="blue"></option><option value="id_d" label="D" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_curve" label="AnimationCurve" color="blue"></option><option value="id_vartype" label="VariationType" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>high</code></td><td><span data-option="id_t">T</span></td><td>The maximum (high) value for the property during this range.</td></tr><tr><td><code>low</code></td><td><span data-option="id_t">T</span></td><td>The minimum (low) value for the property during this range.</td></tr><tr><td><code>variationAmplitude</code></td><td><span data-option="id_d">D</span></td><td>The amplitude of the variation applied to the value.</td></tr><tr><td><code>diurnalCurve</code></td><td><span data-option="id_curve">AnimationCurve</span></td><td>Modulates the value throughout the day. X-axis is time (0-1), Y-axis lerps between the low and high.</td></tr><tr><td><code>variationPeriod</code></td><td><span data-option="id_float">float</span></td><td>The period or frequency over which the variation occurs.</td></tr><tr><td><code>variationType</code></td><td><span data-option="id_vartype">VariationType</span></td><td>Determines the algorithm used for calculation (<code>Sine</code>, <code>Noise</code>, or <code>None</code>).</td></tr></tbody></table>

### `DailyRange<T, D>` Methods

<table><thead><tr><th width="241.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_float" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>GetVariation(MeridiemDate, int)</code></td><td><span data-option="id_float">float</span></td><td>Calculates the variation modifier based on the date, the chosen <code>VariationType</code>, and the system seed.</td></tr></tbody></table>


### `ClimateRanges` Fields

<table><thead><tr><th width="180">Field</th><th width="150">Type<select><option value="id_daily" label="DailyRange" color="blue"></option><option value="id_precip" label="PrecipitationChance" color="blue"></option><option value="id_season" label="SeasonName" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>temperature</code></td><td><span data-option="id_daily">DailyRange</span></td><td>Sets the daily range for temperature this season.</td></tr><tr><td><code>humidity</code></td><td><span data-option="id_daily">DailyRange</span></td><td>Sets the daily range for humidity this season.</td></tr><tr><td><code>pressure</code></td><td><span data-option="id_daily">DailyRange</span></td><td>Sets the daily range for pressure this season.</td></tr><tr><td><code>uvIndex</code></td><td><span data-option="id_daily">DailyRange</span></td><td>Sets the daily range for the UV index this season.</td></tr><tr><td><code>airQuality</code></td><td><span data-option="id_daily">DailyRange</span></td><td>Sets the daily range for the air quality this season.</td></tr><tr><td><code>stratiformRainChance</code></td><td><span data-option="id_precip">PrecipitationChance</span></td><td>Chance for lighter, longer storms. Used in seasonal calculation mode.</td></tr><tr><td><code>convectiveRainChance</code></td><td><span data-option="id_precip">PrecipitationChance</span></td><td>Chance for heavier, faster storms. Used in seasonal calculation mode.</td></tr><tr><td><code>season</code></td><td><span data-option="id_season">SeasonName</span></td><td>The name of the season for this climate range.</td></tr></tbody></table>


### `ClimateSnapshot` Fields

<table><thead><tr><th width="180">Field</th><th width="150">Type<select><option value="id_prop" label="ClimateProperty" color="blue"></option><option value="id_precip" label="PrecipitationChance" color="blue"></option><option value="id_season" label="SeasonName" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>temperature</code></td><td><span data-option="id_prop">Temperature</span></td><td>The current temperature based on this snapshot.</td></tr><tr><td><code>humidity</code></td><td><span data-option="id_prop">Humidity</span></td><td>The current humidity based on this snapshot.</td></tr><tr><td><code>pressure</code></td><td><span data-option="id_prop">Pressure</span></td><td>The current pressure based on this snapshot.</td></tr><tr><td><code>uvIndex</code></td><td><span data-option="id_prop">UVIndex</span></td><td>The current UV index based on this snapshot.</td></tr><tr><td><code>airQuality</code></td><td><span data-option="id_prop">AirQuality</span></td><td>The current air quality based on this snapshot.</td></tr><tr><td><code>stratiformRainChance</code></td><td><span data-option="id_precip">PrecipitationChance</span></td><td>The current stratiform rain chance based on this snapshot.</td></tr><tr><td><code>convectiveRainChance</code></td><td><span data-option="id_precip">PrecipitationChance</span></td><td>The current convective rain chance based on this snapshot.</td></tr><tr><td><code>season</code></td><td><span data-option="id_season">SeasonName</span></td><td>The current season associated with this snapshot.</td></tr></tbody></table>

### `Season` Fields

<table><thead><tr><th width="180">Field</th><th width="150">Type<select><option value="id_date" label="MeridiemDate" color="blue"></option><option value="id_ranges" label="ClimateRanges" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>startDay</code></td><td><span data-option="id_date">MeridiemDate</span></td><td>Sets the starting day for the season in the year.</td></tr><tr><td><code>climateInformation</code></td><td><span data-option="id_ranges">ClimateRanges</span></td><td>The specific ranges and rules for the climate during this season.</td></tr></tbody></table>

## Enumerations

### `SeasonName`
Specifies the four standard seasons:
*   `Spring`
*   `Summer`
*   `Fall`
*   `Winter`

### `VariationType` (Inside `DailyRange`)
Defines the mathematical curve applied to the climate data's variation:
*   `Sine`: A smooth wave, useful for predictable, cyclical patterns (like temperature peaks in the afternoon).
*   `Noise`: Uses Perlin noise for unpredictable, chaotic variation.
*   `None`: Disables variation.
