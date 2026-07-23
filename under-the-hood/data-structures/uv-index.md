---
icon: sun
---

# UV Index

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Climate/UVIndex.cs" class="button secondary" data-icon="code">View on GitHub</a>

The `UVIndex` struct represents solar ultraviolet (UV) radiation levels within COZY. Its value is internally clamped between 0 and 15.

## Usage Examples

<details>

<summary>Initialization &#x26; Implicit Conversions</summary>

```csharp
using DistantLands.Cozy;

// Implicit assignment (clamped 0-15)
UVIndex uv1 = 5f; 

// Implicit conversion back to float
float rawValue = uv1; 
```

</details>

<details>

<summary>Formatting</summary>

```csharp
UVIndex uv = new UVIndex(11f);

// Convert to string
string formatted = uv.ToString(); // "11"

```

</details>

<details>

<summary>Parsing Strings</summary>

```csharp
UVIndex uv1 = UVIndex.Parse("8");
UVIndex uv2 = UVIndex.Parse("12.5");

```

</details>

<details>

<summary>Interpolation &#x26; Arithmetic Operations</summary>

```csharp
UVIndex start = 0f;
UVIndex end = 10f;

// Interpolate half-way
UVIndex mid = UVIndex.Lerp(start, end, 0.5f); // 5

// Modify UV index using UVIndexDelta
UVIndexDelta spike = new UVIndexDelta(2f);
start.Add(spike);

```

</details>

## API

### Properties

<table><thead><tr><th width="128.66668701171875">Property</th><th width="118.33331298828125">Type<select><option value="id_float" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Normalized</code></td><td><span data-option="id_float">float</span></td><td>Returns a <code>0.0</code>–<code>1.0</code> clamped float representation mapped between 0 and 15.</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="215.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="UVIndex" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>UVIndex(float)</code></td><td><span data-option="id_ctor">Constructor</span></td><td>Constructs a new <code>UVIndex</code> instance clamped between 0 and 15.</td></tr><tr><td><code>GetUVIndex()</code></td><td><span data-option="id_float">float</span></td><td>Gets the UV index value as a float.</td></tr><tr><td><code>ToString()</code></td><td><span data-option="id_str">string</span></td><td>Formats the UV Index as a rounded string value.</td></tr><tr><td><code>Parse(string)</code></td><td><span data-option="id_self">UVIndex</span></td><td>Parses numeric strings into a <code>UVIndex</code> struct.</td></tr><tr><td><code>Lerp(UVIndex, float)</code></td><td><span data-option="id_self">UVIndex</span></td><td>Linearly interpolates this instance toward another target <code>UVIndex</code>.</td></tr><tr><td><code>Add(UVIndexDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by adding a <code>UVIndexDelta</code>.</td></tr><tr><td><code>Subtract(UVIndexDelta)</code></td><td><span data-option="id_void">void</span></td><td>Mutates this instance by subtracting a <code>UVIndexDelta</code>.</td></tr></tbody></table>

### Static Methods

<table><thead><tr><th width="209.66668701171875">Method</th><th width="120.3333740234375">Return Type<select><option value="id_ctor" label="Constructor" color="blue"></option><option value="id_float" label="float" color="blue"></option><option value="id_str" label="string" color="blue"></option><option value="id_self" label="UVIndex" color="blue"></option><option value="id_void" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td><code>Lerp(UVIndex, UVIndex, float)</code></td><td><span data-option="id_self">UVIndex</span></td><td>Linearly interpolates between two <code>UVIndex</code> values.</td></tr></tbody></table>

## UVIndex Delta

The `UVIndexDelta` struct represents a change in uvindex.

When adjusting values over time or applying modifiers, always be sure to use the `UVIndexDelta` variant instead of `UVIndex` to maintain correct unit and localization offsets.
