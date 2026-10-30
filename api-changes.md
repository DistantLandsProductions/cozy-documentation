---
icon: file-lines
tags:
  - api
---

# API Changes

## API Changes

COZY 4 contains many major API changes for better code hygeine, performance, and usability. This page covers the majority of the _runtime_ API changes that will cause issues when upgrading.

{% hint style="info" %}
**NOTE:** It is strongly recommended that you fully remove COZY 3 and create a backup of your project before upgrading to COZY 4 due to the number of changes
{% endhint %}

## Render Pipeline

COZY 4 is URP **only** and does not support HDRP or BiRP

## Core

### CozyWeather.cs

#### Enforced capitalization rules

* Changed CozyWeather.instance to CozyWeather.Instance

#### Removed extraneous features from CozyWeather.cs

* Moved atmosphere properties to the Atmosphere Module in the parameters struct
* Lock to camera settings and custom pivot removed in favor of the new track point system
* Global static settings (DisplayGizmos, FreezeUpdateInEditMode, etc.) moved to CozyPreferences
* Removed cloud and star particle coloring feature
* Removed references to mesh layers in favor of the new renderer feature system
* Moved event logic to individual modules

#### Added "Providers" to encapsulate individual features

* Moved weather and filter properties to FXProvider
* Created MaterialProvider for managing references to COZY materials
* Created VFXProvider for managing VFX
* Created VFXBlockingProvider for managing VFX blocking

#### Execution logic

* Changed events from static to instanced
* Changed execution events to Action types instead of delegate functions
* Removed UpdateFXWeights
* Removed PropogateVariables to OnSendToGPU
* Changed names to start with "On" to follow convention

#### Modules are now interface-typed

### CozySystem.cs

#### Changed

* weight is now read-only. The public weight field is replaced by Weight (get-only). The main weather instance calculates it at runtime. To influence it, set TargetWeight.
* targetWeight is now a property. TargetWeight is virtual, so subclasses can override it. The backing field is private and serialized.
* priority is now a property. Priority has a serialized backing field with a minimum of -999. Systems with equal priority are weighted against each other, and higher priority is evaluated later and takes precedence.
* CozySystem is now partial. It carries \[AddComponentMenu("")] so it no longer shows in the Add Component menu.
* The public OnEnable() is removed. The system no longer calls CozyWeather.instance.SetupSystems() when enabled.
* SkipTime(MeridiemTime) is replaced by Skip(MeridiemTimeDelta). The old method was an empty stub. The new one forwards the delta to every ISkippable module.

#### Added

* Module management, moved from CozyWeather into the base class so biomes get it too:
  * AddModule() and AddModule(Type), which validate ICozyModule and \[CozyModule] and warn on duplicates.
  * RemoveModule() and RemoveModule(Type).
  * HasModule() and HasModule(Type).
  * GetModule(out T), GetModules() and Get(ref T), which resolve by \[CozyModule] priority, then by name, with single and list caches.
  * ResetModule(Type) and ResetModules().
  * ModuleHolder (auto-creates a “Modules” child), ModuleArray and ActiveAndEnabledModules.
* Child lookup helpers: GetChild(string), GetChild(string) and FindChildrenComponentsByTag().
* Save and load via ISaveable modules:
  * Save(slot) and Load(slot) use PlayerPrefs (CZY\_Save\_{slot}).
  * GetSaveString() and LoadFromString() use JSON.

### CozyModule.cs

#### Added

* ICozyModule implementation. CozyModule now implements the interface, which is what CozySystem uses to add, query and cache modules.
* Active property (defaults to true). CozySystem.ActiveAndEnabledModules filters on it.
* Implicit bool conversion, so a module can be null-checked like a normal Unity object (if (module)).
* Declarative dependencies:
  * ModuleRequirements (virtual) and the Requirements accessor.
  * DependsOn() through DependsOn\<T1, T2, T3, T4, T5>() helpers, so a module can declare up to five required module types.
* ResetModule(), which deinitializes, reinitializes and resubscribes the module in one call.
* SubscribeToExecutionEvents() and UnsubscribeToExecutionEvents() as overridable hooks. Subscribing unsubscribes first, so calling it twice no longer creates duplicate handlers.
* LoadSceneMode parameter on OnSceneLoaded, passed through from CozyWeather.

#### Removed

* UpdateFXWeights() and its CozyWeather.UpdateFXWeights subscription
* SetupModule(Type\[] requirements). Requirements now come from ModuleRequirements.
* Weather-sphere redirect in InitializeModule(). A module added directly onto the CozyWeather GameObject is no longer destroyed and re-added through CozyWeather.InitializeModule(Type). Modules must now be added with CozySystem.AddModule.

#### Changed

* Renamed members:
  * weatherSphere → WeatherSphere
  * system → System (now virtual)
  * UpdateWeatherWeights() → OnUpdateWeatherWeights()
  * PropogateVariables() → PropagateVariables() (typo fixed)
  * CozyUpdateLoop() → OnCozyUpdateLoop()
* Event wiring:
  * Handlers subscribe to OnFrameReset, OnUpdateWeatherWeights, OnSendToGPU and OnCozyUpdateLoop.
  * PropagateVariables now runs on OnSendToGPU.
  * OnEnable and OnDisable are private, and they call InitializeModule and DeinitializeModule plus the subscribe and unsubscribe hooks.
  * InitializeModule() and DeinitializeModule() are now empty virtual hooks. The enabled guard and the event wiring moved out of them.
* SetupModule() now takes no arguments. It reads Requirements and uses WeatherSphere.HasModule and AddModule to add anything missing, logging the same message.
* CheckIfModuleCanBeRemoved and CheckIfModuleCanBeAdded went from internal virtual to public virtual.
* Migration: any custom module that overrides UpdateWeatherWeights, PropogateVariables, CozyUpdateLoop or SetupModule(Type\[]), or reads weatherSphere or system, needs updating to the new names and signatures. Any use of UpdateFXWeights needs another approach.

## Data

### MeridiemTime

#### Added

* **12-hour model with `Meridiem` enum (AM/PM).** `hours` is now strictly 1-12 and each time carries a `meridiem`. The old class stored 0-23 hours with no meridiem.
* **Always-normalized values.** All constructors route through one core constructor that wraps the time into a single day, so out-of-range inputs and negative values balance correctly.
* **New constructors and factories:**
  * `MeridiemTime(hour, minute, Meridiem)` and `MeridiemTime(hour, minute, second, millisecond, Meridiem)`.
  * `From24Hour(...)` for 24-hour input.
  * `ToClamped(float)` for clamping a day percentage.
* **Time arithmetic and comparison:**
  * `+` and `-` with `MeridiemTimeDelta`, and `-` between two times returning a `MeridiemTimeDelta`.
  * `<`, `>`, `==` and `!=`.
  * `IComparable<MeridiemTime>`, `IEquatable<MeridiemTime>`, plus `Equals` and `GetHashCode` overrides.
* **Helpers:**
  * `AbsoluteHour` (0-23) and `AsPercentage()`.
  * `FloorToMinute` and `FloorToHour`.
  * `WrapInt(...)`.
* **Presets:** `Noon`, `Midnight`, `SixAM`, `SixPM`, plus `Sunrise` and `Sunset`, which read from `CozyTransitModule` when it exists and fall back to 6 AM and 6 PM.
* **Formatting:** `StandardTime()`, `MilitaryTime()` and `FullMilitaryTime()`.
* **Implicit conversions to and from `double`.**

#### Removed

* **The `timeAsPercentage` field.** Use `AsPercentage()` or the implicit `float` conversion.
* **The `MeridiemTime(int hour, int minute)` and `MeridiemTime(int, int, int, int)` constructors,** and the parameterless constructor. Pass a `Meridiem`, or use `From24Hour`.
* **The `new string ToString()` hiding method.** It is replaced by a proper `ToString()` override.

#### Changed

* **`MeridiemTime` is now a `struct`, not a class.** It is copied by value and can no longer be `null`.
* **`ToString()` respects the user's time unit.** `CozyPreferences.TimeUnit` selects `h:mm AM/PM` (standard) or 24-hour output. Before, it always printed 24-hour `HH:mm`.
* **`FullString()`** now prints `h:mm:ss:mmm AM/PM`. Milliseconds use 3 digits instead of 4, which fixes the old `D4` padding.
* **`float` and `DateTime` conversions** now go through the normalized millisecond total. The `DateTime` conversion uses `AbsoluteHour`.
* **The implicit `string` conversion** now calls `ToString()`, so it follows the time-unit preference.
* **Migration:** code that reads `hours` as 0-23, constructs a time without a `Meridiem`, checks `time == null`, or uses `timeAsPercentage` needs updating. Use `AbsoluteHour`, `From24Hour` and `AsPercentage()`.

#### Added new MeridiemTimeDelta struct

The delta struct is unbound by 12 hour format and useful for adding and subtracting time

### MeridiemDate

Added new MeridiemDate script that handles date formatting

### MeridiemEvent

COZY 4 adds a new calendar event system that lets you schedule events based on time of day, date, season, etc. This replaces the old Habits module in terms of functionality.

* **Unified Interface (`IMeridiemEvent`)**: Defines core calendar-based events with support for start/end dates, specific times, durations, overnight checks, and repeat styles.
* **Asset-Based Events (`StaticEvent`)**: Implements a Unity `ScriptableObject` (`Distant Lands/Cozy/Meridiem Event`) allowing developers to configure and save preset events directly inside the Unity Editor.
* **Code-Driven Events (`RuntimeEvent`)**: Provides constructors for dynamically instantiating and configuring calendar events at runtime via code.
* **Lifecycle Callbacks**: Built-in `Action` delegates (`OnEventStart`, `OnEventRunning`, `OnEventEnd`) to easily hook custom game logic into different phases of an event.
* **Flexible Scheduling**: Supports all-day toggles, date ranges, 24-hour limits, and custom repeat styles.
* **Event Categories (`MeridiemEventType`)**: Includes built-in categorization options such as Weather, Holiday, Status, WorldEvent, Player, NPC, Enemy, and Ambient.
* **Utility & Tracking Methods**: Includes helper functions like `DoesEventHappenToday`, `DoesEventHappenAllDay`, and relative date offset calculations.

### Climate properties

All climate properties have been moved to unique structs that store data. This value can be localized based on your needs (e.g. convert temperature from Fahrenheit to Celsius).

## Modules

### Atmosphere Module

#### Added

* **Per-module atmosphere pipeline.** The module now owns its own state instead of writing into `CozyWeather` fields:
  * `Parameters` (`AtmosphereParameters`) holds the combined values for the frame.
  * `AtmosphereModel` is built from the profile and evaluated against the time of day.
  * `UpdateModel()` rebuilds the model. It runs when the profile is assigned, on `OnValidate` and on `InitializeModule`.
* **`IAtmosphereModule` implementation** and the `[CozyModule("Atmosphere", ...)]` attribute, so the module works with the new `CozySystem` module registry. The module is also hidden from the Add Component menu.
* **Biome blending through `ApplyBiome(biome, weight)`.** It replaces the long per-field lerp loop.
* **Extension hooks:**
  * `RunBeforeBiomes` and `RunAfterBiomes` events.
  * A serialized `overrides` list of `AtmosphereOverride`.
* **Sun and moon simulation inside the module:**
  * Public `SunDirection`, `MoonDirection`, `SunLight`, `MoonLight` and `StrongestLight`.
  * Static lighting, quantized lighting, and sky pitch and rotation preferences.
  * Moon placement modes (`AlwaysOpposeSun` and `Realistic`) with orbit period, declination and phase, driven by the calendar.
* **Scene lighting control:**
  * Ambient lighting (gradient or flat).
  * Sun and moon color, intensity and shadows, with a minimum light angle.
  * A `LightningLightingOverride` that dims the lights.
  * Sun and moon lens flares with camera occlusion.
* **Cloud shadows.** A compute-shader cookie texture is generated for the sun when volumetric clouds and cloud shadows are enabled, with configurable resolution, size, steps and blur.
* **Style-gated shader uploads.** Variables are grouped into Lighting, Sky, Fog, Clouds and Sunshafts and are only sent for features the current `CozyStyle` uses.
* **Change detection.** Only values that differ from `lastFrameParameters` are uploaded, with a full resend after `UpdateModel()`.
* **Cloud wind offset.** It accumulates from the Wind module and is sent as a global.
* **`GetLightStrength(Light)` helper.**

#### Removed

* **`ChangeAtmosphere(profile, time)`**, the `TransitionAtmosphere` coroutine and `transitioningAtmosphere`. Nothing in this file replaces timed profile transitions.
* **`SetAtmosphereVariables()`** and the field-by-field copy into `CozyWeather`.
* **The `LateUpdate` biome and shader step.** It used to call `ComputeBiomeWeights()` and `weatherSphere.UpdateShaderVariables()`.
* **The null-profile warning.** `PropagateVariables` no longer returns early without a profile.
* **The public `atmosphereProfile` field.**
* **The `usePhysicalSunHeight` switch.** The module always uses `Time.ModifiedTime`, falling back to 0.5.
* **The `System.Linq`, `System.Collections` and `DistantLands.Cozy.Data` usings.**

#### Changed

* **Renamed members and base class:**
  * Base class `CozyBiomeModuleBase<T>` becomes `CozyBiomeModule<T>`.
  * `PropogateVariables()` becomes `PropagateVariables()` (typo fixed).
  * `weatherSphere` becomes `WeatherSphere`.
  * `isBiomeModule` becomes `IsBiomeModule`.
* **`AtmosphereProfile` is now a property** over a private serialized field. Setting it rebuilds the model.
* **`InitializeModule()` is now overridden.** Non-biome modules reset their parameters, find the sun, moon and flare objects, and set the flare occlusion camera.
* **Shader values are no longer routed through `CozyWeather`.** They are sent straight to global shader properties from the module.
* **The parameter set is regrouped** into Lighting, Sky, Fog, Clouds and Sunshafts sections with new names. Review any custom shaders or profiles that rely on the COZY 3 names.
* **URP is now required by this file.** It uses `UniversalAdditionalLightData` and `LensFlareComponentSRP` with no `COZY_URP` guard. Built-in and HDRP projects won't compile it as is.
* **Migration:** code that reads atmosphere values from `CozyWeather` fields, sets `atmosphereProfile` directly, or calls `ChangeAtmosphere` needs updating. Use `AtmosphereProfile`, `Parameters` and the new hooks.

### Time Module

#### Added

* **Calendar built into the Time module.** It now implements `ITimeModule`, `ICalendarModule`, `ICalendarEventsModule`, `ISaveable` and `ISkippable`, and is registered with `[CozyModule("Time", ...)]`. It is hidden from the Add Component menu.
* **Calendar and dates:**
  * `CurrentDate` (`MeridiemDate`) replaces `currentDay` and `currentYear`.
  * `OnChangeDay` and `OnChangeYear` events.
  * `ProgressDay` toggle.
  * `DayAndTime` property.
* **Calendar events:**
  * `StaticEvents` (serialized) and `RuntimeEvents`.
  * `AddEvent()` and `RemoveEvent()`.
  * `GetEventsOnDay(date)` and `RefreshTodaysEvents()`.
  * `EventsToday`, with all-day and overnight handling. Events are updated every frame in `Update`.
* **Time events and modification:**
  * `OnNewHour` and `OnNewMinute` (with old and new values).
  * `OnModifyTime`, with `ModifiedTime` exposing the result.
* **Time blocks.** `CurrentBlock` and `ChangeBlockEvent` track Dawn, Morning, Day, Afternoon, Evening, Twilight and Night, using the boundaries in `CozyPreferences`.
* **`SmoothlySkipTime(newTime, duration, moveTimeForward)`.** It supports forward or backward movement and rolls the date over midnight.
* **Save and load** via `Save()` and `Load()`, covering time, date and runtime events.
* **`SkipTime(MeridiemTimeDelta)`.** It applies a delta and carries overflow into the date.
* **Public time settings:** `TimeMovementSpeed`, `PauseTime` and `CurrentTime`, now backed by serialized fields on the module.

#### Removed

* **`PerennialProfile` dependency.** The module no longer reads these settings from a profile:
  * `resetTimeOnStart`, `startTime`, `pauseTime`, `timeMovementSpeed`, `modulateTimeSpeed` and `timeSpeedMultiplier`.
  * `daysPerYear`, realistic and leap years, and the month tables.Time settings now live on the module. Confirm where year length and month data moved.
* **Year and date handling:**
  * `currentDay`, `currentYear`, `AbsoluteDay` and `DaysPerYear`.
  * `yearPercentage` and `GetCurrentYearPercentage()`.
  * `DayAndTime()` as a method (now a property).
  * `MonthTitle()` and `GetCurrentMonth()`.
* **Date override.** `CozyDateOverride`, `overrideDate` and the `parentModule` field.
* **Transit integration:**
  * The `transit` reference.
  * `modifiedDayPercentage`.
  * `GetSunTransitTime()`.
  * Use `ModifiedTime` and `OnModifyTime` instead.
* **`TransitionTime()`** and `transitioningTime`. `SmoothlySkipTime` is the replacement.
* **`SetHour()` and `SetMinute()`.**
* **Both `SkipTime(MeridiemTime)` overloads,** including the days-to-skip version and the manual calls into the Ambience module and each `CozySystem`. `CozySystem.Skip` now forwards to `ISkippable` modules.
* **Event raising through the weather sphere:** `weatherSphere.events.RaiseOnDayChange()` and `RaiseOnYearChange()`. Use `OnChangeDay` and `OnChangeYear` instead.
* **The `Start()` method.** Setup now happens in `InitializeModule()`.
* **The `[Obsolete] GetDaysPerYear()`.**
* **`weatherSphere.timeModule` assignment.** The module no longer registers itself on the sphere.

#### Changed

* **`currentTime` becomes `CurrentTime` (property).** The setter fires hour and minute events when they change. The default is now 0.5 (noon) instead of 0.
* **Module wiring:** `InitializeModule()` and `DeinitializeModule()` now subscribe and unsubscribe `UpdateTimeBlock` and `RefreshTodaysEvents`.
* **`CheckIfModuleCanBeAdded`** now rejects a second `ITimeModule`, `ICalendarModule` or `ICalendarEventsModule`, instead of checking for `SystemTimeModule`.
* **`CheckIfModuleCanBeRemoved`** is now `public` and uses `HasModule<CozyTransitModule>()`.
* **Time progression:**
  * `ManageTime()` advances by `TimeMovementSpeed * deltaTime` and constrains in a local float.
  * Midnight rollover moves `CurrentDate` forward or back when `ProgressDay` is on.
  * Speed modulation is evaluated at the current time.
* **Naming:** `weatherSphere` becomes `WeatherSphere`.
* **Migration:** code that reads `currentTime`, `currentDay`, `currentYear`, `yearPercentage` or `modifiedDayPercentage`, calls `SkipTime(MeridiemTime)`, `TransitionTime`, `MonthTitle` or `GetSunTransitTime`, or relies on `PerennialProfile` or the sphere's `events` needs updating. Use `CurrentTime`, `CurrentDate`, the calendar events and `ISkippable`.

### Weather Module

#### Added

* **State machine base class.** The module now derives from `CozyStateMachineModule<WeatherProfile>` and implements `IWeatherModule`. It is registered with `[CozyModule("Weather", ...)]` and hidden from the Add Component menu. Weather is now a single current profile with transitions rather than a weighted blend of many profiles.
* **Initialization behavior.** `WeatherInitializationBehavior` chooses what happens at start:
  * `SetForecast` queues `StartingForecast`.
  * `SetWeather` uses `StartingWeather`, and falls back to a random profile with a warning if it is null.
  * `SetRandomWeather` (default) picks a random profile.Setup only runs in play mode.
* **Change mode.** `WeatherChangeMode` (default `ChangeWhenWeatherFinishes`) controls whether the state machine timer advances. `WeatherChangeTime` is stored on the module.
* **Next-weather selection.** `NextWeatherSelectionMode` supports three modes:
  * `Forecast`: takes the next entry from the queue.
  * `Random`: picks uniformly from the forecast profile.
  * `WeightedRandom`: weights candidates by `GetChance` against a `ConditionSnapshot` (date, time and conditions), starting from the profiles that can follow the last one.
* **Forecast queue:**
  * `CurrentForecast` is a list of `WeatherPattern` entries with start and end date and time.
  * `PopulateForecast()` fills the queue up to `forecastAheadAmount`.
  * `QueueWeather(profile)` picks a random duration between the profile's min and max time.
  * `QueueWeather(profile, duration)` takes an explicit `MeridiemTimeDelta`. Both reject null profiles and zero durations.
* **`ForecastProfile` property** over a private serialized field.

#### Removed

* **The weighted multi-profile ecosystem.** Gone from this file:
  * `ecosystem`, `Ecosystem` and `ICozyEcosystem`.
  * `currentWeatherProfiles` and the `WeatherRelation` list.
  * The weight merging in `ManageGlobalEcosystem()` and `UpdateWeatherByWeight()`.
  * The `strongestWeather` tracking.
* **Local cloud and filter state:**
  * `cumulus`, `cirrus`, `altocumulus`, `cirrostratus`, `chemtrails`, `nimbus` and the nimbus and border values.
  * `fogDensity`, `filterSaturation`, `filterValue`, and the filter, sun and cloud colors.
  * `defaultClouds` and `defaultFilter`, plus `ResetClouds()` and `ResetFilter()`.
  * `PropogateVariables()`, which copied them to `CozyWeather`. Confirm that FX profiles now write these directly.
* **Per-frame FX weighting.** `UpdateFXWeights()` calling `SetWeatherWeight` on each profile is removed, along with `UpdateWeatherWeights()` and `FrameReset()` overrides.
* **Event raising:** `weatherSphere.events.RaiseOnWeatherChange()`. Weather change notification is not in this file, so check that the base class raises it.
* **`LocalSystem` and `Awake()`, `Start()` and `RunChecks()`.** FX effect initialization in `Start()` is gone, and the `Resources.Load` of default profiles no longer happens.
* **Biome support in this file.** Biome registration (`AddBiome`, `biomes`, `ComputeBiomeWeights`, `isBiomeModule`) and the `CozyBiomeModuleBase<T>` base class are removed. Confirm that biome weather is handled elsewhere.
* **The `weatherSphere.weatherModule` assignment.**
* **The `DistantLands.Cozy.Data`, `System.Linq` and `CozySearchable` usages.**

#### Changed

* **Base class:** `CozyBiomeModuleBase<CozyWeatherModule>` becomes `CozyStateMachineModule<WeatherProfile>`.
* **`InitializeModule()`** now calls the base and creates an empty forecast list. The biome and weather sphere wiring is removed.
* **Weather lives on profiles.** `WeatherProfile`, `StartingWeather` and `StartingForecast` use `[SerializeReference]`.
* **Renamed members:** `weatherSphere` becomes `WeatherSphere`.
* **Migration:** code that reads `cumulus`, `fogDensity` or the filter values from the module, uses `ecosystem` or `currentWeatherProfiles`, or relies on `onWeatherChange` needs updating. Use `CurrentForecast`, `QueueWeather` and the state machine API. Existing scenes will lose their weather profile lists and ecosystem data, so plan for asset migration.

### Climate

#### Added

* **Module registration.** The module implements `IClimateModule`, `ISeasonModule` and `IPrecipitationModule`. It is registered with `[CozyModule("Climate", ...)]` and hidden from the Add Component menu.
* **Typed climate properties.** `Temperature`, `Humidity`, `Pressure`, `UVIndex` and `AirQuality` are now `ClimateProperty<T, TDelta>` values with daily `High` and `Low`, a `Current` value and a biome `Offset`. Pressure, UV index and air quality are new, and temperature is unit-aware.
* **Seasons.** `CurrentSeason` and `OnChangeSeason` are driven by the season start days on the `ClimateProfile`.
* **Extreme days.** `HottestDayOfTheYear` and `ColdestDayOfTheYear` are computed lazily and refreshed on year change.
* **Daily ranges.** `UpdateDiurnal()` pulls the day's highs and lows from the profile on each day change. Current values are interpolated along each property's diurnal curve.
* **`GetRangesAtDayAndTime(date, time)`.** It returns a `ClimateSnapshot` for any date and time, replacing the old `GetTemperature(time)` and `GetHumidity(time)`.
* **Precipitation chances:**
  * `ConvectiveRainChance` and `StratiformRainChance`.
  * `RainChanceCalculationMode` (`Calculated`, `Seasonal`, `Manual`). `Calculated` derives chances from temperature, humidity and pressure.
  * `convectiveChanceOffset` and `stratiformChanceOffset`.
* **Accumulation API.** `AccumulatedSnow`, `AccumulatedRain`, `SnowAccumulationSpeed` and `RainAccumulationSpeed` are public properties.
* **Native fallback.** If there is no Calendar module, the climate module switches to `Native` control.

#### Removed

* **Flat float state:**
  * `currentTemperature` and `currentPrecipitation`. Use `Temperature.Current` and `Humidity.Current`.
  * `localTemperatureFilter` and `localPrecipitationFilter`.
  * The internal `temperatureOffset` and `precipitationOffset` floats.
* **Getters:** `GetTemperature()`, `GetTemperature(time)`, `GetHumidity()` and `GetHumidity(time)`. The `[Obsolete]` `GetPrecipitation()` overloads are also gone.
* **`snowSpeed` and `rainSpeed` fields.** They are replaced by the accumulation speed properties.
* **`UpdateBiomeModule()`** and the per-frame lerp of absolute biome values.
* **Sphere wiring:**
  * The `weatherSphere.climateModule` assignment.
  * `isBiomeModule`, `AddBiome()` and `ComputeBiomeWeights()`.
  * The `base.InitializeModule()` and `base.DeinitializeModule()` calls.
* **The `DistantLands.Cozy.Data` using.**

#### Changed

* **Naming and base class:**
  * Base class `CozyBiomeModuleBase<T>` becomes `CozyBiomeModule<T>`.
  * `CozyUpdateLoop()` becomes `OnCozyUpdateLoop()`.
  * `weatherSphere` becomes `WeatherSphere`.
* **`ControlMethod` is now nested** in the module (`Profile` or `Native`) instead of `CozyWeather.ControlMethod`.
* **Biome blending is additive.** Biomes add weighted offsets to each property in `ApplyBiome` instead of lerping absolute temperature and precipitation values.
* **Precipitation is split out.** `UpdatePrecipitation()` now holds the snow and groundwater logic. It only accumulates in play mode, but the shader globals are still set in edit mode.
* **Shader globals** use `CozyShaderIDs` (`baseWeatherSnow`, `baseWeatherWetness`) instead of string names.
* **Snow melt** compares against 32°F using the typed `Temperature`.
* **Event wiring.** `InitializeModule()` and `DeinitializeModule()` subscribe and unsubscribe `UpdateDiurnal`, `UpdateCurrentSeason` and `UpdateExtremeDays` on the Calendar module.
* **Migration:** code that reads `currentTemperature`, `currentPrecipitation`, `snowSpeed` or `rainSpeed`, calls `GetTemperature` or `GetHumidity`, or sets the local filters needs updating. Use the typed properties, `GetRangesAtDayAndTime` and the accumulation properties. Existing scenes will lose the old filter values, so plan for asset migration.

### Wind Module

#### Added

* **Module registration.** The module derives from `CozyBiomeModule<CozyWindModule>` and implements `IWindModule`. It is registered with `[CozyModule("Wind", ...)]` and hidden from the Add Component menu.
* **Overridable wind settings.** Each setting is a serialized range value that can be overridden per biome, with a public property:
  * `WindStrength`, `WindSpeed` and `Heading`.
  * `HeadingVariance` and `WindSpeedVariance`.
  * `GustingPower` and `GustingFrequency`.
* **Rate controls:** `WindSpeedChangeRate` and `HeadingChangeRate`, clamped to a minimum of 0.001.
* **`WindParameters`.** This holds the combined per-frame values. It is reset in `FrameReset()` from any overridden settings, then blended by biomes.
* **Compass-based direction.** `Heading` is in degrees, clockwise from the North set in `CozyPreferences`, and it follows `SkyRotation`.
  * `WindDirection` is now calculated from the heading.
  * Setting `WindDirection` converts the vector back to a heading. It ignores a zero vector or a mostly vertical one.
* **Custom shader globals.** `globalShaderProperties` is a list of `WindProperty` entries (name and type). The supported types are `HeadingDegrees`, `HeadingRadians`, `Direction`, `WindSpeed`, `WindStrength`, `GustingPower` and `GustingFrequency`. Property IDs are cached on `InitializeModule()`.
* **Biome blending.** `ApplyBiome()` blends heading and gusting frequency by weight. It also applies gusting power and wind strength when the biome overrides them.
* **`windZoneMultiplier`** scales the Unity `WindZone` strength.

#### Removed

* **The default `WindFX` profile.**
  * `defaultWindProfile` and its `Resources.Load` of `Default Profiles/Default Wind`.
  * Defaults now live in the serialized fields: strength 0, speed 5, heading 0.
* **The flat fields:** `windAmount`, `windGusting`, `windSpeed` (as a float) and `windChangeSpeed`.
* **The Perlin-driven random direction.** `overrideWindDirection` is gone. The direction is now the heading plus variance.
* **`WindSpeedInKnots`.**
* **Zephyr integration.** The `ZEPHYR` code is gone: the `zephyrWind` reference and its direction and strength updates. A `zephyrMultiplier` field remains but nothing uses it.
* **`Start()`.** It used to assign `weatherSphere.windModule`, load the default profile, and seed the random generator. The seed is now set in `InitializeModule()`.
* **The `useWindzone` toggle.** The wind zone is updated whenever one is assigned.
* **The `DistantLands.Cozy.Data` using and the `base.DeinitializeModule()` call.**

#### Changed

* **Naming and base class:**
  * Base class `CozyModule` becomes `CozyBiomeModule<CozyWindModule>`.
  * `CozyUpdateLoop()` becomes `OnCozyUpdateLoop()`.
  * `useShaderWind` becomes `useShaders`.
* **Wind zone drive:** `windMain` uses `WindParameters.windStrength * windZoneMultiplier`. It no longer uses `windMultiplier`. Pulse magnitude and frequency come from the gusting settings.
* **Shader globals.** `CZY_WindDirection` is still sent as direction × strength × `windMultiplier`, now with the compass-based direction. `CZY_WindTime` advances by `windSpeed`.
* **Edit mode.** The update loop returns early outside play mode, so wind no longer animates or updates shader globals in the editor.
* **Migration:** code that reads `windAmount`, `windSpeed`, `windGusting` or `windChangeSpeed`, sets `overrideWindDirection`, uses `defaultWindProfile`, or relies on the Zephyr hook needs updating. Use the properties above and `WindParameters`. Existing scenes will lose values from the old wind profile, so plan for asset migration.

### Satellite Module

Removed the old satellite module and added moon settings and rendering directly to the Atmosphere module

### Event Module

Removed the old event module in favor of the new event listener scripts

### Integration Modules

Integrations are moved to a first-party integration system applied globally instead of a per-instance module system

### Save/Load Module

Removed module. Logic can now be run directly from the weather sphere without the need for a module

### Interactions Module & System Time Module

Removed modules

## Integrations

Integrations are given first-party support through the new Integrations window. Any integrations created using modules needs to be updated to this new system!

## Shaders

### Moved to ShaderGraph

All shaders are now built with HLSL and placed in a Shader Graph wrapper for full-screen effects and better cross version support looking forward at the URP changes in the near future.

### New Renderer Feature System

COZY 4 removes the old in-scene mesh layer system in favor of a modern renderer feature based approach. This will also be easier to integrate with third party assets such as water or fog assets.
