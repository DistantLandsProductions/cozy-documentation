---
icon: temperature-list
---

# Temperature

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/Temperature.cs" class="button secondary" data-icon="code">View on GitHub</a>

The `Temperature` struct represents temperature values within COZY. Regardless of how a temperature value is constructed or retrieved, its **internal storage is always stored in Fahrenheit**.

## Localization

Temperature formatting and unit defaults adapt dynamically based on global settings:

* Global Preference: When calling `GetTemperature()` or `ToString()` without explicit parameters, the struct retrieves the active unit from `CozyPreferences.TemperatureUnit`.
* Explicit Conversions: You can specify a `TemperatureUnit` (`Fahrenheit`, `Celsius`, or `Kelvin`) when retrieving values or formatting strings.

## Usage Examples

<details>

<summary>Initialization &#x26; Implicit Conversions</summary>

You can create a `Temperature` object by passing a raw value (defaults to Fahrenheit), specifying an explicit unit, or using implicit float casting:

```csharp
using DistantLands.Cozy;

// Implicit assignment (defaults to Fahrenheit)
Temperature temp1 = 72.5f; 

// Explicit unit constructor
Temperature temp2 = new Temperature(20f, TemperatureUnit.Celsius);

// Implicit conversion back to float (returns internal Fahrenheit value)
float fahrenheitValue = temp1; 
```

</details>

<details>

<summary>Conversions &#x26; Formatting</summary>

```csharp
Temperature temp = new Temperature(100f, TemperatureUnit.Celsius);

// Get converted float values
float celsius = temp.GetTemperature(TemperatureUnit.Celsius); // 100.0f
float kelvin = temp.GetTemperature(TemperatureUnit.Kelvin);   // 373.15f

// Convert to localized strings
string formatted = temp.ToString(TemperatureUnit.Celsius); // "100.0°C"
```

</details>

<details>

<summary>Parsing Strings</summary>

Strings containing numbers and optional unit designations can be converted into `Temperature` structs:

```csharp
Temperature t1 = Temperature.Parse("25.5 °C");
Temperature t2 = Temperature.Parse("300K");
Temperature t3 = Temperature.Parse("72"); // Uses CozyPreferences.TemperatureUnit
```

</details>

<details>

<summary>Interpolation &#x26; Arithmetic Operations</summary>

```csharp
Temperature start = 32f; // 32°F
Temperature end = 212f;  // 212°F

// Interpolate half-way between 32°F and 212°F
Temperature mid = Temperature.Lerp(start, end, 0.5f); // 122°F

// Modify temperatures using TemperatureDelta
TemperatureDelta boost = new TemperatureDelta(10f, TemperatureUnit.Celsius);
start.Add(boost);
```

</details>

## API

### Properties

<table><thead><tr><th width="128.66668701171875">Property</th><th width="118.33331298828125">Type<select><option value="2vj2nBWFhPyx" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Normalized</code></td><td><span data-option="2vj2nBWFhPyx">float</span></td><td>Returns a <code>0.0</code>–<code>1.0</code> clamped float representation mapped between -30°F and 120°F.</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="cKW72RPdHkeC" label="Constructor" color="blue"></option><option value="D6ubP05jV5tf" label="float" color="blue"></option><option value="J0rMksSdZPhK" label="string" color="blue"></option><option value="78o8Gt79yD8f" label="Temperature" color="blue"></option><option value="GNBuTBLFDe47" label="int" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Temperature(float, TemperatureUnit)</code></td><td><span data-option="cKW72RPdHkeC">Constructor</span></td><td>Constructs a new <code>Temperature</code> instance converted from the provided unit into internal Fahrenheit.</td></tr><tr><td><code>Temperature(float)</code></td><td><span data-option="cKW72RPdHkeC">Constructor</span></td><td>Constructs a new <code>Temperature</code> instance assuming raw Fahrenheit input.</td></tr><tr><td><code>GetTemperature(TemperatureUnit)</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Gets the temperature value converted to the requested unit.</td></tr><tr><td><code>GetTemperature()</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Gets the temperature converted to <code>CozyPreferences.TemperatureUnit</code>.</td></tr><tr><td><code>ToString()</code></td><td><span data-option="J0rMksSdZPhK">string</span></td><td>Formats the temperature as a string formatted according to <code>CozyPreferences.TemperatureUnit</code>.</td></tr><tr><td><code>ToString(TemperatureUnit)</code></td><td><span data-option="J0rMksSdZPhK">string</span></td><td>Formats the temperature value with its symbol (e.g., <code>"20.0°C"</code>, <code>"293.15K"</code>, <code>"68.0°F"</code>).</td></tr><tr><td><code>Parse(string)</code></td><td><span data-option="78o8Gt79yD8f">Temperature</span></td><td>Parses temperature strings (e.g., <code>"72f"</code>, <code>"20.5 celsius"</code>) into a <code>Temperature</code> struct.</td></tr><tr><td><code>Lerp(Temperature, Temperature, float)</code></td><td><span data-option="78o8Gt79yD8f">Temperature</span></td><td>Linearly interpolates between two <code>Temperature</code> values.</td></tr><tr><td><code>Lerp(Temperature, float)</code></td><td><span data-option="78o8Gt79yD8f">Temperature</span></td><td>Linearly interpolates this instance toward another target <code>Temperature</code>.</td></tr><tr><td><code>Add(TemperatureDelta)</code></td><td><span data-option="78o8Gt79yD8f">Temperature</span></td><td>Mutates this instance by adding a <code>TemperatureDelta</code>.</td></tr><tr><td><code>Subtract(TemperatureDelta)</code></td><td><span data-option="78o8Gt79yD8f">Temperature</span></td><td>Mutates this instance by subtracting a <code>TemperatureDelta</code>.</td></tr><tr><td><code>CompareTo(Temperature)</code></td><td><span data-option="GNBuTBLFDe47">int</span></td><td>Compares the internal value to another <code>Temperature</code> instance.</td></tr><tr><td><code>ConvertToUnit(float, TemperatureUnit)</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Utility method that converts a Fahrenheit value into the target <code>TemperatureUnit</code>.</td></tr><tr><td><code>ConvertFromUnit(float, TemperatureUnit)</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Utility method that converts a value from a specified <code>TemperatureUnit</code> into Fahrenheit.</td></tr></tbody></table>

### Static Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="cKW72RPdHkeC" label="Constructor" color="blue"></option><option value="D6ubP05jV5tf" label="float" color="blue"></option><option value="J0rMksSdZPhK" label="string" color="blue"></option><option value="78o8Gt79yD8f" label="Temperature" color="blue"></option><option value="GNBuTBLFDe47" label="int" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>ConvertToUnit(float, TemperatureUnit)</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Utility method that converts a Fahrenheit value into the target <code>TemperatureUnit</code>.</td></tr><tr><td><code>ConvertFromUnit(float, TemperatureUnit)</code></td><td><span data-option="D6ubP05jV5tf">float</span></td><td>Utility method that converts a value from a specified <code>TemperatureUnit</code> into Fahrenheit.</td></tr></tbody></table>

## Temperature Delta

The temperature delta struct represents a change in temperature. It can also be converted to other localizations, but will not offset them.&#x20;

> 0°C is 32°F, but a change of 0°C is the same as a change of 0°F!

When adjusting temperature, always be sure to use temperature delta instead of temperature!
