---
icon: file
tags:
  - profile
---

# Profiles

A **profile** in COZY is a static bit of data stored as a scriptable object to be loaded at runtime. Profiles are not designed to be manipulated at runtime, but loaded by modules that use their settings to change the overall effect of COZY.

This section covers the concrete profile assets that drive COZY's major systems:

* [Weather Profile](weather-profile.md) — defines the active state, timing, chances, and weather-specific FX for a single weather condition.
* [Atmosphere Profile](atmosphere-profile.md) — stores a list of atmospheric overrides used to shape the scene atmosphere.
* [Climate Profile](climate-profile.md) — defines seasonal temperature, humidity, pressure, and related climate ranges across the year.
* [Ambience Profile](ambience-profile.md) — drives non-weather ambient states and associated FX.
* [Forecast Profile](forecast-profile.md) — determines which weather profiles can follow one another and how forecast sequencing works.
* [FX Profiles](fx-profiles/) — reusable effect containers attached to weather and ambience profiles.
