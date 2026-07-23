---
icon: wind
---

# AirQuality

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/AirQuality.cs" class="button secondary" data-icon="code">View on GitHub</a>

The `AirQuality` struct represents the Air Quality Index (AQI) within COZY. Its value is internally clamped between 0 and 500.

## Usage Examples

<details>

<summary>Initialization & Implicit Conversions</summary>

```csharp
using DistantLands.Cozy;

// Implicit assignment (clamped 0-500)
AirQuality aq = 45f; 

// Implicit conversion back to float
float rawValue = aq; 
```

</details>

<details>

<summary>Formatting</summary>

```csharp
AirQuality aq = new AirQuality(150f);

// Convert to formatted string
string formatted = aq.ToString(); // "150 AQI"

```

</details>

<details>

<summary>Parsing Strings</summary>

```csharp
AirQuality aq1 = AirQuality.Parse("50");
AirQuality aq2 = AirQuality.Parse("300 AQI"); // Extracts numeric value

```

</details>

<details>

<summary>Interpolation & Arithmetic Operations</summary>

```csharp
AirQuality start = 20f;
AirQuality end = 200f;

// Interpolate half-way
AirQuality mid = AirQuality.Lerp(start, end, 0.5f); // 110

// Modify AQI using AirQualityDelta
AirQualityDelta smog = new AirQualityDelta(50f);
start.Add(smog);

```

</details>

## API

### Properties

<table><thead><tr><th width="128.66668701171875">Property</th><th width="118.33331298828125">Type<select><option value="id_float" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Normalized</code></td><td><span data-option="id_float">float</span></td><td>Returns a <code>0.0</code>–<code>1.0</code> clamped float representation mapped between 0 and 500.</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="AirQuality" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>AirQuality(float)</code></td><td><span data-option="id_ctor">Constructor</span></td><td>Constructs a new <code>AirQuality</code> instance clamped between 0 and 500.</td></tr><tr><td><code>GetAirQuality()</code></td><td><span data-option="id_float">float</span></td><td>Gets the Air Quality index value as a float.</td></tr><tr><td><code>ToString()</code></td><td><span data-option="id_str">string</span></td><td>Formats the Air Quality value with the AQI suffix (e.g., <code>"45 AQI"</code>).</td></tr><tr><td><code>Parse(string)</code></td><td><span data-option="id_self">AirQuality</span></td><td>Parses numeric strings into an <code>AirQuality</code> struct.</td></tr><tr><td><code>Lerp(AirQuality, float)</code></td><td><span data-option="id_self">AirQuality</span></td><td>Linearly interpolates this instance toward another target <code>AirQuality</code>.</td></tr><tr><td><code>Add(AirQualityDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by adding an <code>AirQualityDelta</code>.</td></tr><tr><td><code>Subtract(AirQualityDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by subtracting an <code>AirQualityDelta</code>.</td></tr></tbody></table>

### Static Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="AirQuality" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Lerp(AirQuality, AirQuality, float)</code></td><td><span data-option="id_self">AirQuality</span></td><td>Linearly interpolates between two <code>AirQuality</code> values.</td></tr></tbody></table>

## AirQuality Delta

The `AirQualityDelta` struct represents a change in airquality.

When adjusting values over time or applying modifiers, always be sure to use the `AirQualityDelta` variant instead of `AirQuality` to maintain correct unit and localization offsets.
