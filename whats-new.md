---
description: The road from 3.7 to 4.0
icon: burst-new
---

# What's New?

COZY 4 focuses on improving a few key aspects of COZY 3: visuals, functionality, UI/UX, performance, and exciting things like code hygiene and architectural changes

### Visuals

* Fog
  * New froxel-based volumetric fog
* Clouds
  * New raymarched volumetric clouds
  * Updated 2D cloud algorithms for better visuals, performance, and artistic freedom
* Sky
  * Added two-tone fog and sky coloring for improved scene depth
  * Moon is now a part of the atmosphere rendering process and can have its color, phase, etc. influenced by atmosphere modules (Atmosphere, Blocks, etc.)
  * Stars and constellations can now twinkle at night
* Lighting
  * Sun and moon can now be quantized to prevent light jitter
  * Sun and moon can now have a minimum angle to prevent dark scenes
  * Shadow intensity can now be controlled by the atmosphere module

### Functionality

* Meridiem System
  * After the introduction of the meridiem time struct in COZY 3, now even more systems in COZY will be utilizing this method for data storage
  * MeridiemDate: stores a date (month, day, year) in time.
  * MeridiemTime: upgraded time functions to be more specific. You can now set times in code using AM and PM. (E.g. 11:59 PM instead of 23:59).
  * MeridiemBlock: defines a block of time in the day. Used for events, Blocks, and Transit.
  * MerdiemTimeDelta: defines a duration of time. Used for times that do not have clock rules applied to them (i.e. a 13 hour long event is not the same as 1 PM).
  * MeridiemEvent: defines a calendar event that will be called by the time module.
* True Localization
  * Time, temperature, pressure, and date formats can be changed in editor allowing you properly switch from Fahrenheit to Celsius without changing any data in COZY
* New Integrations System
  * Integrations are no longer modules but located in a separate tab
  * Integrations can now automatically update ShaderGraph files when needed
  * New integrations for the following assets
    * &#x20;
* New Climate data
  * Rather than using animation curves, COZY 4 defines four seasons that interpolate all properties based on the time of year.
  * Seasons are defined by 5 changing properties: temperature, humidity, air pressure, UV index, and air quality.
  * Each property can have a min and max value as well as a modulated offset for more variation day to day. This can be controlled on a per season basis as well for more violent storms as weather changes quickly in spring and autumn.
  * Split rain chance into two values: stratiform rain chance and convective rain chance. These are used to control the chance for light rain and heavy rain separately to mirror real life
  * Seasons can also be used for meridiem events
* Weather
  * New forecast profile system that automatically identifies errors in your forecast
  * Lateral shifts now let you dynamically change the weather based on the current climate. If rain gets too cold, swap to snow.
* Events
  * Removed events module in favor of individual module events.
  * Time Events
    * Events for new minute, hour, day, year
    * New Merdiem Event system
      * Create static events with custom repeating patterns
      * Create events based on world conditions rather than set dates (e.g. coldest day of the year, full moon, first day of a season, etc.)
      * Define a start and end date and time
      * Hook events up to start, end, and while active events
      * Create dynamic events at runtime
  * Weather events
  * Ambience change events
  * Event listener helper script provides a no-code UI to grab meridiem and weather events
* FX
  * Thunder
    * New thunder attractor script will attract lightning strikes and call an event when struck
    * New VFX graph based lightning effect
  * New VFX Graph integration
  *

### UI/UX

* Dynamic Icon System
  * COZY modules will automatically update their icons to show you how changes to one module impact the system as a whole
  * Modules are now always displayed at the top of the COZY weather editor for easy access
* Widget System Improvements
  * Introduced in COZY 3.6.0, widgets were designed to share a bit of information as well as be clickable. Now in COZY 4, these serve as areas to modify data as well as view information
  * Modules may now have more than one widget when needed
  * Widgets may be hidden or shown by right clicking on the module icon.
* Module UI
  * Atmosphere module UI
    * Organize each feature individually
    * Only control what you need
    * Automatically warns you when you are wasting computation on a feature that is unused
  * Time Module UI
    *

