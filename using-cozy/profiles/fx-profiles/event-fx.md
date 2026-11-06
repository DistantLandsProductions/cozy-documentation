---
icon: bolt
---

# Event FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/EventFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`EventFX` is a lightweight timed notification FX. Rather than changing a weather value directly, it emits lifecycle callbacks when the effect starts, updates, or ends. This makes it useful for custom scripts, gameplay hooks, or integration points that need to react when a weather/ambience state becomes active.

## What it does

This FX exposes events:

- `OnStart`
- `OnUpdate`
- `OnEnd`

When the FX weight is above `0.5f`, it triggers start/update behavior; when it falls below that threshold, it stops. This makes it a useful bridge between COZY profile logic and external gameplay systems.

## Typical use cases

### Gameplay event triggers

Fire a script when a storm enters a heavy phase or when a weather profile becomes active.

### Audio or VFX scheduling

Hook into `OnStart` or `OnEnd` to trigger custom audio, particles, or ambience transitions not covered by built-in FX types.

### Custom integrations

If you need to respond to COZY state changes with your own C# logic, `EventFX` is the cleanest minimal hook.

## Notes

- This profile does not directly render or modify world values.
- It acts as a signal and hook layer between COZY state changes and custom code.
- It is ideal for integration scenarios and custom gameplay callbacks.
