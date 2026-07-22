---
description: Implements IAtmosphereModule
icon: image
tags:
  - module
  - tutorial
  - api
---

# Atmosphere Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyAtmosphereModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

The Atmosphere Module is the core system that manages all visual aspects of the sky, fog, clouds, and lighting in COZY. This module controls the most important aesthetic features of your weather system, including sky gradients, celestial bodies, cloud layers, and environmental lighting.

## Overview

The Atmosphere Module works by collecting parameters from atmosphere profiles and biomes, then propagating these values to Unity's shader system. The module handles:

- **Sky Rendering**: Gradient skies, two-tone skies, stars, constellations, galaxy, rainbows, light columns, and shooting stars
- **Celestial Bodies**: Sun and moon disk rendering with configurable appearance and orbital mechanics
- **Fog Systems**: Multiple fog types including gradient fog, volumetric fog, height-based fog, and two-tone fog
- **Cloud Layers**: Volumetric clouds and procedural cloud layers (cumulus, altocumulus, cirrus, cirrostratus)
- **Lighting**: Sun and moon light management, ambient lighting, lens flares, and shadow configuration

## Module Architecture

The Atmosphere Module operates in two main phases:

### 1. Parameter Aggregation (`PropagateVariables`)
The module collects atmosphere parameters from:
- Active atmosphere profile overrides
- Biome-specific atmosphere profiles (when applicable)
- Sky pitch and rotation preferences

### 2. Shader Variable Propagation (`PassShaderVariables`)
All collected parameters are passed to the rendering system through global shader variables, ensuring visual consistency across all rendered surfaces.

## Public Properties

| Name | Type | Description |
|------|------|-------------|
| `Parameters` | AtmosphereParameters | Read-only access to the current atmosphere parameters |
| `SunDirection` | Vector3 | The current direction vector pointing toward the sun |
| `MoonDirection` | Vector3 | The current direction vector pointing toward the moon |
| `SunLight` | Light | Reference to the sun light component |
| `MoonLight` | Light | Reference to the moon light component |
| `StrongestLight` | Light | Returns whichever light (sun or moon) is currently brightest |

## Public Methods

| Name | Parameters | Return Type | Description |
|------|------------|------------|-------------|
| `InitializeModule` | - | void | Sets up module references and initializes parameters |
| `PropagateVariables` | - | void | Collects and aggregates all atmosphere parameters |

## Public Events

| Name | Parameters | Description |
|------|------------|-------------|
| `RunBeforeBiomes` | CozyAtmosphereModule | Invoked before biome atmosphere profiles are applied |
| `RunAfterBiomes` | CozyAtmosphereModule | Invoked after biome atmosphere profiles are applied |

## Usage Examples

<details>

<summary>Access Current Atmosphere Parameters</summary>

```csharp
// Get the atmosphere module
CozyAtmosphereModule atmosphereModule = GetComponent<CozyWeather>().GetModule<CozyAtmosphereModule>();

// Access current parameters
AtmosphereParameters currentParams = atmosphereModule.Parameters;

// Get specific values
Color skyZenith = currentParams.skyGradientZenithColor;
float sunIntensity = currentParams.lightingSunLightIntensity;
```

</details>

<details>

<summary>Monitor Celestial Directions</summary>

```csharp
// Get the atmosphere module
CozyAtmosphereModule atmosphereModule = GetComponent<CozyWeather>().GetModule<CozyAtmosphereModule>();

// Get sun and moon positions
Vector3 sunDir = atmosphereModule.SunDirection;
Vector3 moonDir = atmosphereModule.MoonDirection;

// Calculate angle between sun and observer
float sunAngle = Vector3.Angle(Vector3.up, -sunDir);

// Determine if the sun is above the horizon
bool sunAboveHorizon = sunAngle < 90;
```

</details>

<details>

<summary>Respond to Atmosphere Changes</summary>

```csharp
CozyAtmosphereModule atmosphereModule = GetComponent<CozyWeather>().GetModule<CozyAtmosphereModule>();

// Subscribe to atmosphere events
atmosphereModule.RunBeforeBiomes += (module) =>
{
    Debug.Log("About to apply biome atmosphere settings");
};

atmosphereModule.RunAfterBiomes += (module) =>
{
    Debug.Log("Biome atmosphere settings applied");
    
    // Update custom lighting based on new atmosphere
    UpdateCustomLighting(module);
};
```

</details>

<details>

<summary>Get the Strongest Light Source</summary>

```csharp
CozyAtmosphereModule atmosphereModule = GetComponent<CozyWeather>().GetModule<CozyAtmosphereModule>();

// Get whichever light is currently brightest
Light dominantLight = atmosphereModule.StrongestLight;

// This is useful for directing shadows or special effects
if (dominantLight == atmosphereModule.SunLight)
{
    Debug.Log("Sun is the primary light source");
}
else
{
    Debug.Log("Moon is the primary light source");
}
```

</details>

## Interfaces

The Atmosphere Module implements the `IAtmosphereModule` interface, providing a standard contract for atmosphere management across the COZY ecosystem.

## Sky Configuration

The module supports multiple sky rendering modes:

### Gradient Sky
A smooth gradient from zenith to horizon with optional ground color. Perfect for realistic atmospheric rendering.

**Key Parameters:**
- `skyGradientZenithColor` - Color at the top of the sky
- `skyGradientHorizonColor` - Color at the horizon
- `skyGradientGroundColor` - Color for the ground/below horizon
- `skyGradientZenithExponent` - Controls gradient falloff from zenith
- `skyGradientGroundExponent` - Controls gradient falloff to ground

### Two-Tone Sky
A stylized two-color sky split around the sun direction. Great for cartoon or stylized weather.

**Key Parameters:**
- `skyTwoToneSunSideColor` - Color on the sun side
- `skyTwoToneAntiSunSideColor` - Color opposite the sun
- `skyTwoToneOffset` - Adjusts the split position
- `skyTwoToneExponent` - Controls the transition smoothness

### Celestial Features
Stars, constellations, galaxy, rainbows, light columns, and shooting stars can all be independently configured and blended into your sky.

## Cloud Systems

### Volumetric Clouds
High-performance volumetric cloud rendering with ray marching, supporting multiple height layers and wind effects.

**Configuration:**
- Height and thickness
- Density and cohesion for shape control
- Lighting colors for lit and shaded areas
- Wind strength for animation
- LOD support for performance scaling

### Cloud Layers
Four procedural cloud layer types with unique characteristics:

1. **Cumulus** - Puffy fair-weather clouds
2. **Altocumulus** - Mid-level textured clouds
3. **Cirrus** - High, wispy clouds with wind effects
4. **Cirrostratus** - Thin, sheet-like clouds

Each layer supports independent configuration of height, density, lighting, wind, and erosion.

## Fog Systems

### Gradient Fog
Multi-color gradient fog with distance-based density variation.

### Volumetric Fog
Lit fog with ray marching and multiple cascade levels for advanced atmospheric effects.

### Height Fog
Fog density based on world height for realistic ground-hugging effects.

### Two-Tone Fog
Stylized fog split between sun-lit and shadowed areas.

## Lighting Management

The module automatically manages:

- **Sun Light**: Direction, intensity, color, and shadows based on time and atmosphere
- **Moon Light**: Similar to sun with moon phase influence
- **Ambient Lighting**: Sky, equator, and ground colors for global illumination
- **Lens Flares**: Automatic lens flare positioning and intensity

When `HandleSceneLighting` is enabled in preferences, the module updates Unity's global render settings automatically.

## Performance Considerations

- The Atmosphere Module uses shader global variables for efficiency
- Only changed parameters are propagated to shaders (delta detection)
- Cloud rendering supports LOD adjustments for performance scaling
- Volumetric effects can be configured with step count for quality/performance tradeoffs

## Biome Integration

The Atmosphere Module fully supports COZY's biome system. Each biome can define its own atmosphere profile with unique sky, fog, cloud, and lighting settings. The module smoothly blends between biome atmospheres based on active biome weights.

## Interfaces

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3><i class="icon icon-square"></i>IAtmosphereModule</h3></td><td align="center">The standard interface for atmosphere management</td><td><a href="iatmospheremodule.md">iatmospheremodule.md</a></td></tr></tbody></table>
