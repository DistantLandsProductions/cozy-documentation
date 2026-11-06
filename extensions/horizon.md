---
tags:
  - extension
  - module
  - atmosphere
  - rendering
  - api
---

# Horizon

Horizon adds stylized layered background effects for COZY atmospheres. Instead of only rendering the sky dome, it creates a horizon plane that can contain layered silhouettes, terrain, clouds, sprites, and other atmospheric scenery.

This module is a good fit for wide, low-lying scenic features such as mountain ridges, floating islands, distant city skylines, forests, or foggy atmospheric layers. It is especially useful when you want a more painterly or stylized background than a standard skybox alone can provide.

## What it does

The Horizon module stores a list of layer references and resolves them into an active set that is rendered in the atmospheric scene. Each layer defines:

- the layer type (`Cubemap`, `Ribbon`, `Sprite`, or `TextureSheet`)
- placement in front of or behind clouds
- color, alpha, scale, tiling, angle, and orientation
- a unique distance key used for ordering

The module works with either static or animated layers and can be layered with weather and biome conditions.

## Typical use cases

### Stylized world background

Use Horizon for distant mountain silhouettes, prairies, floating islands, ruins, or city skylines that sit on the weather horizon.

### Environment storytelling

A low-lying fog bank, warm desert dunes, or a dark forest line can be added behind clouds and foreground atmosphere to create stronger environmental identity.

### Cinematic atmosphere layering

Because Horizon layers are independent from the weather profile, you can keep the main weather changes while making the background feel unique to the biome or moment.

## Core API

### `CozyHorizonModule`

```csharp
public class CozyHorizonModule : CozyBiomeModule<CozyHorizonModule>
```

Key members:

- `CozyHorizonProfile Profile`
- `SortedList<int, HorizonLayerInstance> ActiveLayers`
- `override void InitializeModule()`
- `override void OnCozyUpdateLoop()`
- `override void ApplyBiome(CozyHorizonModule biome, float weight)`

### `CozyHorizonProfile`

```csharp
public class CozyHorizonProfile : CozyProfile
```

The profile contains the layered setup for the horizon renderer.

Important members:

- `List<HorizonLayerReference> layers`
- `enum LayerType { Cubemap, Ribbon, Sprite, TextureSheet }`
- `enum PlacementLocation { behindClouds, inFrontOfClouds }`

### `HorizonLayerReference`

A layer reference describes how one horizon element is rendered:

```csharp
public class HorizonLayerReference
{
    public LayerType layerType = LayerType.Ribbon;
    public PlacementLocation placementLocation = PlacementLocation.inFrontOfClouds;
    public Texture texture;
    public Color color = Color.white;
    public float fogAmount = 1;
    public float placementHeight = 0f;
    public float verticalScale = 0.5f;
    public float tiling = 2;
    public float angle;
    public float alpha = 1;
    public float rows = 1;
    public float columns = 1;
    public float framerate = 10;
    public float pitch = 0;
    public float yaw = 0;
    public float roll = 0;
    public float size = 1;
    public int distance;
}
```

This is the core config object. The `distance` field gives the layer a unique render order so overlapping layers can be sorted deterministically.

### `HorizonFeature`

```csharp
public class HorizonFeature : ScriptableRendererFeature
```

This is the renderer integration that performs the actual render pass for the horizon layers. It is the bridge between the profile data and the Unity render pipeline.

## Example usage

```csharp
var horizon = weather.GetModule<CozyHorizonModule>();
if (horizon != null)
{
    horizon.Profile = horizonProfile;
}
```

Typical setup steps:

1. Create a `CozyHorizonProfile` asset.
2. Add one or more `HorizonLayerReference` entries.
3. Choose a layer type and placement location.
4. Set the texture, size, scale, and ordering.
5. Assign the profile to the Horizon module.

## Notes

- Horizon is best for atmospheric scenery rather than gameplay geometry.
- Layers can be placed before or after cloud rendering, depending on your compositing goal.
- Use `distance` to keep layers from fighting for render order when multiple layers share similar visuals.
