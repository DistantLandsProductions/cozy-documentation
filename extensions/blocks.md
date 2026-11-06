---
tags:
  - extension
  - module
  - atmosphere
  - api
---

# Blocks

Blocks is a time-based atmosphere override module for COZY. Instead of replacing the main atmosphere profile, it schedules a collection of block profiles that blend into the active weather state over time. This makes it ideal for scenes where the sky should slowly evolve from sunrise to daylight, dusk, overcast, or nighttime transitions without losing the underlying COZY atmosphere logic.

The module tracks time-of-day and chooses the appropriate block based on the current schedule. Each block stores one or more weighted `BlocksProfile` entries, and each selected profile can override specific atmosphere variables while leaving everything else to the main COZY atmosphere and biome configuration.

## What it does

At a high level, Blocks does the following:

- defines named daily time windows
- selects one profile for each time block based on conditions and weighted probability
- blends that profile into the current atmosphere over a transition period
- leaves any untouched atmosphere values under the main COZY system's control

This makes it useful for generative or scripted climates where you want different sky and fog conditions at different hours without managing a large number of full atmosphere profiles manually.

## Typical use cases

### Daily atmospheric transitions

Create a day block, evening block, and night block that progressively change fog, sky, lighting, and cloud parameters across the day.

### Biome-specific timed moods

A desert, tundra, or tropical biome can use timed atmosphere states to shift from bright noon to warm gold-hour haze or cool night fog.

### Story-driven environment changes

Inject unique time blocks for cinematic periods, weather events, seasonal transitions, or special scenes while keeping the base atmosphere profile intact.

## Core API

### `BlocksModule`

```csharp
public class BlocksModule : CozyBiomeModule<BlocksModule>
```

Key members:

- `BlocksCollectionProfile CollectionProfile`
- `BlocksProfile CurrentBlockProfile`
- `override Type[] ModuleRequirements`
- `public override void InitializeModule()`
- `public override void ApplyBiome(BlocksModule biome, float weight)`

### `BlocksCollectionProfile`

```csharp
public class BlocksCollectionProfile : CozyProfile
```

This profile defines the daily schedule. It contains a list of `BlockCollection` entries with:

- `blockName`
- `startTime`
- `transitionPercentage`
- `List<BlocksConditions> blocks`

The module evaluates the current time against the collection and chooses the active block.

### `BlockCollection`

```csharp
public struct BlockCollection
{
    public string blockName;
    public MeridiemTime startTime;
    public float transitionPercentage;
    public List<BlocksConditions> blocks;
}
```

Each `BlockCollection` references a set of profile conditions and chance weights; the selected override profile is resolved once per day and reused for that day's block.

### `BlocksProfile`

```csharp
public class BlocksProfile : CozyProfile
```

This is the specific override set for a block. It contains a list of generated `BlockOverride` objects and applies them to `AtmosphereParameters` while respecting the feature toggles on each override.

### `BlockOverride`

```csharp
public class BlockOverride
```

Generated override types extend this class and represent individual atmosphere variables such as sky gradients, fog settings, ambient light, or cloud properties. Each override can be toggled on or off and adds its value during the block blending pass.

### `TimeBlock`

```csharp
public struct TimeBlock
{
    public List<BlocksConditions> profileConditions;
    public MeridiemTime startTime;
    public MeridiemTime endTime;
    public string name;
}
```

This type is used to describe the scheduled block shape and timing at the data level.

## Example usage

```csharp
var blocks = weather.GetModule<BlocksModule>();
if (blocks != null)
{
    blocks.CollectionProfile = myBlocksCollection;
}
```

A common setup pattern is:

1. Create a `BlocksCollectionProfile` asset.
2. Add time blocks such as Dawn, Day, Dusk, and Night.
3. Add `BlocksProfile` entries with override values for each block.
4. Assign the collection to the Blocks module.

## Notes

- Blocks works as an overlay over the current atmosphere rather than replacing it.
- Any override not enabled in the active block remains under the control of the main atmosphere profile.
- Generated override types are built from COZY's atmosphere variable stack and should be regenerated whenever those variable definitions change.

