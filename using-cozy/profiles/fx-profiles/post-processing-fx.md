---
icon: image
---

# Post Processing FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/PostProcessingFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`PostProcessingFX` is a reference FX for Unity's Volume-based post-processing stack. It allows a COZY profile to drive a runtime `Volume` with a custom `VolumeProfile`, including weight and priority adjustments.

## What it does

This profile creates and manages a `Volume` instance with a user-provided profile. While the effect is active, it sets the volume weight using the current weather weight and `TransitionTimeModifier`.

## Typical use cases

### Weather-driven color grading

Attach a specific `VolumeProfile` to a storm or fog state for atmospheric adjustments.

### Split lighting and post-processing moods

Different weather states can use distinct post-processing profiles without hard-coding them into a scene controller.

### Cinematic transitions

Use this to ease from clear to stormy or vice versa with smooth post-processing weight blending.

## Notes

- This is a reference FX built around Unity `Volume` objects.
- It is ideal for atmosphere and post-processing-based weather states.
- It is not the same as `FilterFX`, which modifies COZY’s direct image parameters rather than a Unity Volume stack.
