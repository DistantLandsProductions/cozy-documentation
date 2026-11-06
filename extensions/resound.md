---
tags:
  - extension
  - module
  - audio
  - api
---

# ReSound

ReSound is COZY's audio management extension for weather-driven music playback. It allows your weather state, ambience, and gameplay conditions to select a soundtrack, transition between tracks, and fade in or out without hard-coding transitions or manual playback logic into gameplay code.

The module can choose tracks based on the active COZY profile, current time, biome conditions, or temporary gameplay overrides. It also supports pooling, track priority, requested overrides, and smooth transitions so it can behave like a lightweight procedural DJ system for a weather scene.

## What it does

ReSound centralizes the logic for:

- creating and managing `ResoundTrack` assets
- selecting a track according to the active state machine profile
- handling override requests from gameplay or custom scripts
- blending between tracks using configurable transition types
- routing audio through a mixer group and a reusable audio source pool

This is useful anytime a scene needs music to react to weather mood, time-of-day, or active biome-driven events without writing custom audio scripts for each case.

## Typical use cases

### Weather-driven soundtrack

Change from calm ambient music during clear weather to tense or dramatic music during storms, sunset, or night transitions.

### Gameplay interruptions

Use `TrackOverrideHandle` to temporarily replace the normal track with a menu, cinematic, or event-specific soundtrack while preserving automatic restoration when the override ends.

### Biome and state machine transitions

Since the module inherits a state machine model, it can respond to profile changes and route track selection through COZY conditions and state transitions.

## Core API

### `CozyResoundModule`

```csharp
public class CozyResoundModule : CozyStateMachineModule<ResoundTrack>
```

Key members:

- `CozyResoundDJ DJ`
- `AudioMixerGroup MixerGroup`
- `float MasterVolume`
- `bool Playing`
- `ResoundTrack CurrentTrack`
- `bool TryGetPlayback(out float time, out float length)`
- `TrackOverrideHandle CreateTrackOverride(...)`
- `void ReleaseTrackOverride(long id)`

### `ResoundTrack`

```csharp
public class ResoundTrack : CozyProfile, IStateMachineProfile
```

Tracks contain the actual audio asset and metadata used by the module:

- `AudioClip Clip`
- `float Volume`
- `LoopMethod LoopMode`
- `MeridiemTimeDelta MinTime`
- `MeridiemTimeDelta MaxTime`
- `float Chance`
- `float GetChance(ConditionSnapshot conditions)`

### `LoopMethod`

```csharp
public enum LoopMethod
{
    PlayOnce,
    Loop
}
```

Controls whether the track plays once or loops in the active state machine.

### `SongTransitionType`

```csharp
public enum SongTransitionType
{
    Crossfade,
    FadeOutThenPlayInstant,
    FadeOutThenFadeIn,
    InstantCut,
    PlayAfterCurrentTrack
}
```

Used when moving from one track to another or when a gameplay override interrupts the base selection.

### `TrackOverrideHandle`

```csharp
public sealed class TrackOverrideHandle : IDisposable
```

This is a disposable request object for temporarily forcing a track override. It is useful for short-lived gameplay or cinematic music changes.

### `ResoundFX`

```csharp
public class ResoundFX : CozyFXProfile
```

This profile type allows a temporary music track to be attached to a COZY FX while the FX is active.

## Example usage

```csharp
var resound = weather.GetModule<CozyResoundModule>();
if (resound != null)
{
    resound.MasterVolume = 0.8f;
    resound.Playing = true;
}
```

Temporary override:

```csharp
using var overrideHandle = resound.CreateTrackOverride(
    track: myEventTrack,
    priority: 25,
    transitionOnStart: SongTransitionType.Crossfade,
    transitionOnEnd: SongTransitionType.FadeOutThenPlayInstant);
```

## Notes

- ReSound uses a pooled source system to keep playback efficient.
- It is designed to work as part of the weather state machine, not as a separate runtime music engine.
- `PlayAfterCurrentTrack` is useful when you want to avoid cutting a track mid-song.

