---
icon: droplet
---

# Humidity

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/Humidity.cs" class="button secondary" data-icon="code">View on GitHub</a>

The `Humidity` struct stores a percentage chance for a rain-based weather profile. It is commonly used to set minimum and maximum constraints that factor into the chance effector for weather profiles. Its value is internally clamped between 0 and 100.

## Usage Examples

<details>

<summary>Initialization & Implicit Conversions</summary>

```csharp
using DistantLands.Cozy;

// Implicit assignment (clamped 0-100)
Humidity h1 = 55.5f; 

// Implicit conversion back to float
float rawValue = h1; 
```

</details>

<details>

<summary>Formatting</summary>

```csharp
Humidity h = new Humidity(80f);

// Convert to formatted string
string formatted = h.ToString(); // "80%"

```

</details>

<details>

<summary>Chance Mapping</summary>

```csharp
Humidity h = new Humidity(75f);

// Maps the 0-100 scale to a 0.0-1.0 chance axis multiplier
float chance = h.MapToChanceAxis(); // 0.75f

// Updates the humidity based on a 0.0-1.0 float
h.UnmapToChanceAxis(0.5f); // Sets humidity to 50%

```

</details>

<details>

<summary>Parsing Strings</summary>

```csharp
Humidity h1 = Humidity.Parse("99.9");
Humidity h2 = Humidity.Parse("50%"); // Extracts numeric value

```

</details>

<details>

<summary>Interpolation & Arithmetic Operations</summary>

```csharp
Humidity start = 10f;
Humidity end = 90f;

// Interpolate half-way
Humidity mid = Humidity.Lerp(start, end, 0.5f); // 50

// Modify humidity using HumidityDelta
HumidityDelta rainSystem = new HumidityDelta(20f);
start.Add(rainSystem);

```

</details>

## API

### Properties

<table><thead><tr><th width="128.66668701171875">Property</th><th width="118.33331298828125">Type<select><option value="id_float" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Normalized</code></td><td><span data-option="id_float">float</span></td><td>Returns a <code>0.0</code>–<code>1.0</code> clamped float representation mapped between 0 and 100.</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="Humidity" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Humidity(float)</code></td><td><span data-option="id_ctor">Constructor</span></td><td>Constructs a new <code>Humidity</code> instance clamped between 0 and 100.</td></tr><tr><td><code>GetHumidity()</code></td><td><span data-option="id_float">float</span></td><td>Gets the humidity value as a float.</td></tr><tr><td><code>ToString()</code></td><td><span data-option="id_str">string</span></td><td>Formats the humidity as a rounded string with a percentage symbol (e.g., <code>"50%"</code>).</td></tr><tr><td><code>Parse(string)</code></td><td><span data-option="id_self">Humidity</span></td><td>Parses numeric strings into a <code>Humidity</code> struct.</td></tr><tr><td><code>Lerp(Humidity, float)</code></td><td><span data-option="id_self">Humidity</span></td><td>Linearly interpolates this instance toward another target <code>Humidity</code>.</td></tr><tr><td><code>Add(HumidityDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by adding a <code>HumidityDelta</code>.</td></tr><tr><td><code>Subtract(HumidityDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by subtracting a <code>HumidityDelta</code>.</td></tr><tr><td><code>MapToChanceAxis()</code></td><td><span data-option="id_float">float</span></td><td>Converts the 0-100 percentage into a 0.0-1.0 float representation for chance generation.</td></tr><tr><td><code>UnmapToChanceAxis(float)</code></td><td><span data-option="id_void">void</span></td><td>Sets the humidity percentage based on a 0.0-1.0 chance float input.</td></tr></tbody></table>

### Static Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="Humidity" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Lerp(Humidity, Humidity, float)</code></td><td><span data-option="id_self">Humidity</span></td><td>Linearly interpolates between two <code>Humidity</code> values.</td></tr></tbody></table>

## Humidity Delta

The `HumidityDelta` struct represents a change in humidity.

When adjusting values over time or applying modifiers, always be sure to use the `HumidityDelta` variant instead of `Humidity` to maintain correct unit and localization offsets.
