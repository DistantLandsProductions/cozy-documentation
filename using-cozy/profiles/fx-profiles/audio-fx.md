---
icon: music
---

# Audio FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/AudioFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`AudioFX` is a reference-based FX profile for playing procedural weather or ambience audio from a Unity `AudioSource`. It is a good fit for looping rain, thunder ambience, wind, or environment audio that should rise and fall with the active weather state.

## What it does

This FX creates an `AudioSource` instance and sets its clip, mixer group, loop behavior, and volume to match the current weather weight. It is useful when you want sound to react smoothly to the strength of a weather state instead of toggling abruptly.

## Typical use cases

### Rain or wind ambience

Use a looping clip so the sound layer increases as rain or wind intensity increases.

### Weather-specific sound design

One `AudioFX` can be assigned to a weather profile to make storms sound louder, airier, or more ominous as the profile intensifies.

### Mixer-safe audio layering

Because it exposes an `AudioMixerGroup`, it can route sound through a dedicated COZY weather bus, making it easier to mix with gameplay or music FX.

## Notes

- This is a reference FX, so it instantiates and manages a runtime object rather than just modifying a parameter set.
- It is designed for looping ambience content rather than one-shot event playback.
- The volume scales based on the active weight of the weather or ambience state.
