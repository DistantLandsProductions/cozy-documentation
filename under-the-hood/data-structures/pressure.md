---
icon: gauge
---

# Pressure

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/Pressure.cs" class="button secondary" data-icon="code">View on GitHub</a>

The `Pressure` struct represents atmospheric pressure values within COZY. Regardless of how a pressure value is constructed or retrieved, its **internal storage is always stored in inHg (Inches of Mercury)**.

## Localization

Pressure formatting and unit defaults adapt dynamically based on global settings:

* Global Preference: When calling `GetPressure()` or `ToString()` without explicit parameters, the struct retrieves the active unit from `CozyPreferences.PressureUnit`.
* Explicit Conversions: You can specify a `PressureUnit` (`inHg`, `hPa`, or `Atmosphere`) when retrieving values or formatting strings.

## Usage Examples

<details>

<summary>Initialization & Implicit Conversions</summary>

```csharp
using DistantLands.Cozy;

// Implicit assignment (defaults to inHg)
Pressure p1 = 29.92f; 

// Explicit unit constructor
Pressure p2 = new Pressure(1013f, PressureUnit.hPa);

// Implicit conversion back to float (returns internal inHg value)
float rawValue = p1; 
```

</details>

<details>

<summary>Conversions & Formatting</summary>

```csharp
Pressure p = new Pressure(1f, PressureUnit.Atmosphere);

// Get converted float values
float hpa = p.GetPressure(PressureUnit.hPa); // 1013.25f
float inhg = p.GetPressure(PressureUnit.inHg); // 29.92f

// Convert to localized strings
string formatted = p.ToString(PressureUnit.hPa); // "1013.25 hPa"

```

</details>

<details>

<summary>Parsing Strings</summary>

```csharp
Pressure p1 = Pressure.Parse("1013.25 hPa");
Pressure p2 = Pressure.Parse("1 atm");
Pressure p3 = Pressure.Parse("29.92"); // Uses CozyPreferences.PressureUnit

```

</details>

<details>

<summary>Interpolation & Arithmetic Operations</summary>

```csharp
Pressure start = new Pressure(1000f, PressureUnit.hPa);
Pressure end = new Pressure(1020f, PressureUnit.hPa);

// Interpolate half-way
Pressure mid = Pressure.Lerp(start, end, 0.5f);

// Modify pressure using PressureDelta
PressureDelta drop = new PressureDelta(-5f, PressureUnit.hPa);
start.Add(drop);

```

</details>

## API

### Properties

<table><thead><tr><th width="128.66668701171875">Property</th><th width="118.33331298828125">Type<select><option value="id_float" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Normalized</code></td><td><span data-option="id_float">float</span></td><td>Returns a <code>0.0</code>–<code>1.0</code> clamped float representation mapped between 28.5 and 31.0 inHg.</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="Pressure" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Pressure(float, PressureUnit)</code></td><td><span data-option="id_ctor">Constructor</span></td><td>Constructs a new <code>Pressure</code> instance converted from the provided unit into internal inHg.</td></tr><tr><td><code>GetPressure(PressureUnit)</code></td><td><span data-option="id_float">float</span></td><td>Gets the pressure value converted to the requested unit.</td></tr><tr><td><code>GetPressure()</code></td><td><span data-option="id_float">float</span></td><td>Gets the pressure converted to <code>CozyPreferences.PressureUnit</code>.</td></tr><tr><td><code>ToString()</code></td><td><span data-option="id_str">string</span></td><td>Formats the pressure as a string formatted according to <code>CozyPreferences.PressureUnit</code>.</td></tr><tr><td><code>ToString(PressureUnit)</code></td><td><span data-option="id_str">string</span></td><td>Formats the pressure value with its symbol (e.g., <code>"1013.25 hPa"</code>).</td></tr><tr><td><code>Parse(string)</code></td><td><span data-option="id_self">Pressure</span></td><td>Parses pressure strings (e.g., <code>"1013 hPa"</code>) into a <code>Pressure</code> struct.</td></tr><tr><td><code>Lerp(Pressure, float)</code></td><td><span data-option="id_self">Pressure</span></td><td>Linearly interpolates this instance toward another target <code>Pressure</code>.</td></tr><tr><td><code>Add(PressureDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by adding a <code>PressureDelta</code>.</td></tr><tr><td><code>Subtract(PressureDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by subtracting a <code>PressureDelta</code>.</td></tr></tbody></table>

### Static Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="Pressure" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Lerp(Pressure, Pressure, float)</code></td><td><span data-option="id_self">Pressure</span></td><td>Linearly interpolates between two <code>Pressure</code> values.</td></tr><tr><td><code>ConvertToUnit(float, PressureUnit)</code></td><td><span data-option="id_float">float</span></td><td>Utility method that converts an inHg value into the target <code>PressureUnit</code>.</td></tr><tr><td><code>ConvertFromUnit(float, PressureUnit)</code></td><td><span data-option="id_float">float</span></td><td>Utility method that converts a value from a specified <code>PressureUnit</code> into inHg.</td></tr></tbody></table>

## Pressure Delta

The `PressureDelta` struct represents a change in pressure.

When adjusting values over time or applying modifiers, always be sure to use the `PressureDelta` variant instead of `Pressure` to maintain correct unit and localization offsets.
