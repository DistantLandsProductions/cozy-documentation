---
icon: quote-left
---

# Release Notes

## v4.0.0

### Overview

The fourth major update to COZY: Weather is finally here! This update brings many new features, quality-of-life changes, and performance improvements to the asset that you love.

### What’s New

#### Visual & Rendering Systems

* Raymarched Volumetric Clouds: Brand-new raymarched volumetric cloud system along with updated 2D cloud algorithms for better visuals, performance, and artistic freedom.
* Froxel-Based Volumetric Fog: Complete overhaul bringing realistic, high-performance froxel fog into your scenes.
* Screenspace Sunshafts: Dedicated screenspace sunshafts feature for dynamic atmosphere lighting.
* Renderer Feature Architecture: Moved from nested spheres to a Renderer Feature approach for seamless integration and rendering with Unity 7.
* VFX Graph Integration: Most particle systems (including stylized lightning effects) have been migrated to Unity's VFX Graph.

#### Gameplay & Functionality

* Lightning Attractor System: Summon lightning strikes on customizable `Lightning Attractor` components placed in your scene. Calls events on hit (e.g., set trees on fire, damage players, or trigger gameplay mechanics).
* Climate & Seasonal Data Model: Replaced simple animation curves with 4 distinct, interpolating seasons.
  * Tracks temperature, humidity, air pressure, UV index, and air quality with min/max bounds and daily offset modulators.
  * Split rain probabilities into stratiform rain chance (light rain) and convective rain chance (heavy rain).
* Track Point System: COZY is no longer forced to strictly follow the main camera. Use the new `Track Point` component to easily set anchor locations for VFX and biome calculations.
* Event System Overhaul: Retired the standalone Events Module in favor of module-native events and no-code Event Listener helper scripts.
  * Time Events: Static repeating patterns, runtime dynamic events, world-condition events (e.g., coldest day of the year, full moon, season start), and simple time triggers (minute/hour/day/year).
  * Weather & Ambience Events: Direct hooks for changing weather and ambient states.

#### Meridiem System

* Deeply integrated data storage architecture introduced across the entire asset:
  * `MeridiemDate`: Handles structured date storage (Month, Day, Year).
  * `MeridiemTime`: Supports exact AM/PM or Military time setting in both code and inspector (e.g., `11:59 PM`).
  * `MeridiemBlock`: Defines daytime blocks used for events, blocks, and transitions.
  * `MeridiemTimeDelta`: Represents duration lengths independent of clock rules.
  * `MeridiemEvent`: Defines calendar events executed by the Time Module.

#### Integrations System

* Integrations are moved into Project Settings rather than existing as scene modules.
* Automatically updates ShaderGraph files when needed.
* Includes dedicated developer documentation for writing custom integrations.

### Improvements & Tweaks

#### UX & Workflow Improvements

* Atmosphere Browser Workflow: Dedicated profile browser lets you quickly search, select, preview, and edit atmosphere styles on the fly.
* Updated COZY Home UX:
  * Interactive Widgets: Modify settings directly from the main view without navigating deep into individual modules. Support for multiple widgets per module and right-click visibility toggling.
  * Module Header Navigation: Module selection row remains fixed at the top of the editor for instant switching.
  * Dynamic Module Icons: Displays live status indicators and real-time environment updates at a glance.
* Module-Specific Inspector UI Improvements:
  * Atmosphere: Clean modular layouts that automatically warn you if computation is being wasted on disabled/unused features.
  * Time: Integrated calendar view, AM/PM vs. military time toggle, and scheduled event tracker.
  * Weather & Forecasting: New forecast profile view identifying error states, showing sequence profiles, tracking lateral weather shifts (e.g., switching rain to snow when temperatures drop), and showing condition chances.

#### Localization

* True System Localization: Convert unit displays for time, temperature (°F/°C), pressure, and dates dynamically in the editor without altering or breaking underlying project data.

#### API & Codebase

* Interface-Driven Architecture: Modules now implement dedicated interfaces (`ITime`, `ICalendar`, `ICalendarEvents`, etc.) rather than hard-coded script references, enabling drop-in custom systems.
* Zero GC Allocation: Core runtime functions called per-frame are strictly garbage-free.
* Lighting Tweaks:
  * Added light quantization for the sun and moon to prevent light jitter.
  * Sun/moon minimum angles to ensure scenes never become unnaturally dark.
  * Two-tone fog and sky coloring for better depth perception.
  * Twinkling stars and constellation effects.
  * Moon lighting now reacts dynamically to active atmosphere modules and phases.

### Migration Notes

#### Deprecations & Removed Systems

* Interactions Module: Temporarily deprecated; a complete replacement will be created in the future.
* Habits & Plume Modules: Discontinued. Core functionality has been natively merged into the COZY 4 base package.
* Legacy Demo Scenes: Old demo assets have been removed and replaced with a modern demo suite.

#### API & Upgrade Steps

* No Backwards Compatibility: COZY 4 is a complete rewrite and cannot be automatically upgraded over COZY 3.
* Migration Requirement: You must fully delete the COZY 3 folder from your project before importing COZY 4.
