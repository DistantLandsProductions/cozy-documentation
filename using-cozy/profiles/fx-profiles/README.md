---
coverY: 0
layout:
  width: default
  cover:
    visible: false
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# FX Profiles

FX Profiles are containers of data that are attached to [weather-profile.md](../weather-profile.md "mention") and [ambience-profile.md](../ambience-profile.md "mention")s to modify the scene when a state becomes active. They give COZY a clean layer between profile metadata and runtime world changes.

The concrete FX profile types in COZY fall into two broad groups:

## Parameter FX

These profiles tweak the active COZY simulation values rather than creating scene objects.

- [Cloud FX](cloud-fx.md)
- [Climate FX](climate-fx.md)
- [Filter FX](filter-fx.md)
- [Fog FX](fog-fx.md)
- [Precipitation FX](precipitation-fx.md)
- [Wind FX](wind-fx.md)
- [Event FX](event-fx.md)
- [Multi FX](multi-fx.md)

## Reference FX

These profiles create or drive runtime scene references like audio sources, volumes, VFX, particle systems, or lightning managers.

- [Audio FX](audio-fx.md)
- [Thunder FX](thunder-fx.md)
- [Post Processing FX](post-processing-fx.md)
- [Particle FX](particle-fx.md)
- [Visual Effect Graph FX](visual-effect-graph-fx.md)

## Why FX profiles matter

Instead of embedding all visual and audio logic directly into each weather state, each profile can declare a reusable behavior package. That means a single weather profile might combine a `CloudFX`, a `FogFX`, and a `ThunderFX` without duplicating complexity across many different states.

