---
icon: chart-simple
---

# Multi FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/MultiFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`MultiFX` is a composite FX profile that runs multiple child FX profiles together. It is used when a single weather state needs to layer several effects, each weighted by its own curve and condition evaluation.

## What it does

`MultiFX` stores a list of `MultiFXType` entries:

* `CozyFXProfile FX`
* `WeightedChanceCurve intensityCurve`

When the parent FX is active, each child FX is invoked with a per-item intensity derived from the current conditions and the active weather weight.

## Typical use cases

### Combine layered effects

Use one Multi FX to run Cloud FX, Fog FX, and Filter FX together as a single reusable weather mood.

### Condition-driven layered behavior

Each child can have a unique intensity curve so some effects become stronger under certain scenes or climate states.

### Compact FX compositions

Instead of manually chaining many separate profiles, Multi FX provides a single object that manages a bundle.

## Notes

* This is a compositional profile for combining multiple FX assets into one effect bundle.
* It can be used to simplify complex weather states.
* Each child effect is still a real `CozyFXProfile`, so the underlying effect system remains modular.
