---
icon: gear
---

# Preferences

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>

COZY Preferences store global settings for COZY that are applied in every scene. These are static and not meant to be changed at runtime.

## Orientation

### Sky Pitch

Control the pitch of the sun in the sky. Positive values move the sun towards the southern hemisphere (giving an appearance of being further north on the planet), negative values move the sun towards the northern hemisphere (giving an appearance of being further south on the planet). See [orientation.md](../under-the-hood/orientation.md "mention")

### Sky Rotation

Sets the global North vector. See [orientation.md](../under-the-hood/orientation.md "mention")

## Units

### Temperature Unit

Sets the current [temperature.md](../under-the-hood/data-structures/climate/temperature.md "mention") unit. Use this to swap from Fahrenheit to Celsius or Kelvin. Default value is Fahrenheit.

### Pressure Unit

Sets the current [pressure.md](../under-the-hood/data-structures/climate/pressure.md "mention") unit. Use this to swap from inHg to hPa or Atm. Default value is inHg.

### Time Unit

Sets the current [meridiemtime.md](../under-the-hood/data-structures/meridiem-architecture/meridiemtime.md "mention") unit. You can use either Standard (12-hour format) or Military (24-hour format). Default is Standard.

### Show Seconds

Should editor fields show seconds by default?

### Show Milliseconds

Should editor fields show milliseconds by default?

### Date Format

Sets the date format for editor fields. This is used to decide which comes first; the month, day, or year.

## Time

### Months

Sets the default year used in your project. Each month contains a name and an integer determining the number of days in that month. COZY does not support leap years currently. If this is a needed feature for you, feel free to let us know! [support.md](../support.md "mention")

### Starting Weekday

Sets the day of the week for "day 0".

### Block Times (Dawn, Morning, Etc.)

Sets the start and end times for a named [meridiemblock.md](../under-the-hood/data-structures/meridiem-architecture/meridiemblock.md "mention"). This does _not_ set the time that a particular sun position happens, but changes the times that are associated with a particular name. used by the [blocks.md](../extensions/blocks.md "mention") module, the [meridiemevent.md](../under-the-hood/data-structures/meridiem-architecture/meridiemevent.md "mention") system, and the [meridiemblock.md](../under-the-hood/data-structures/meridiem-architecture/meridiemblock.md "mention") system.

## Editor Settings

### Update in Edit Mode

If false, suppresses all calculations in edit mode. Disable for better in-editor performance.

### Don't Destroy Weather On Load

Does not destroy COZY when loading a new scene. See [Unity's documentation](https://docs.unity3d.com/6000.5/Documentation/ScriptReference/Object.DontDestroyOnLoad.html) for more information.

### Fog

When disabled, the fog is hidden in edit mode.

### Gizmos

Enables and disables all COZY-related gizmos in the scene view.

### Tooltips

Enables COZY tooltips in the editor.

## FX

### Render FX Blocking

Should [fx-blocking.md](utilities/fx-blocking.md "mention") for VFX Graph be rendered?

### FX Render Distance

Sets the render distance for VFX

### FX Render Height

Sets the height for the FX block rendering camera.

### FX Blocking Resolution

Sets the resolution for the FX blocking texture. Higher values lead to lower performance but higher visual fidelity

### FX Blocking Layer Mask

Sets the layer mask of objects that will block VFX

## Quality

### Fog Downsampling

Sets the downsampling of the volumetric fog. Higher values lead to better performance, but lower visual fidelity.

### Cloud Downsampling

Sets the downsampling of the volumetric clouds. Higher values lead to better performance, but lower visual fidelity.

## Calendar

Enable and disable different event types in the calendar in the editor. This _does not_ disable the event type at runtime.

## API
### Properties
<table><thead><tr><th width="179.66668701171875">Name</th><th width="146.33331298828125">Type<select><option value="Qg9dLjdYc4kv" label="float" color="blue"></option><option value="KobA3DE40Gkr" label="TemperatureUnit" color="blue"></option><option value="uNDfW6OETNYf" label="PressureUnit" color="blue"></option><option value="4uNWdG4hLVON" label="MeridiemTime.Unit" color="blue"></option><option value="PMvQM2SWda7I" label="bool" color="blue"></option><option value="Qi69jhbNvW4D" label="int" color="blue"></option><option value="0QNnBTLx765A" label="MonthData[]" color="blue"></option><option value="UyKfTmZqoEUh" label="DateFormat" color="blue"></option><option value="KAEZMRLJbfdt" label="DayOfWeek" color="blue"></option><option value="bjjENAv9IIcE" label="MeridiemBlock" color="blue"></option><option value="YGXQ7Bl0n1K9" label="CozyStyle[]" color="blue"></option><option value="WYVTLi22X9MI" label="CozyStyle" color="blue"></option><option value="uo932IRNcJ5F" label="Vector3" color="blue"></option><option value="zOtySybVFnjb" label="Downsampling" color="blue"></option><option value="ger1mdjLQiXL" label="CozyPreferences" color="blue"></option><option value="QaxOCxGuXVQz" label="List<CozyIntegration>" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>SkyPitch</td><td><span data-option="Qg9dLjdYc4kv">float</span></td><td>Gets the pitch angle (-90 to 90) of the sky.</td></tr><tr><td>SkyRotation</td><td><span data-option="Qg9dLjdYc4kv">float</span></td><td>Gets the rotation angle (0 to 360) of the sky dome.</td></tr><tr><td>TemperatureUnit</td><td><span data-option="KobA3DE40Gkr">TemperatureUnit</span></td><td>Gets the globally configured unit for temperature measurements.</td></tr><tr><td>PressureUnit</td><td><span data-option="uNDfW6OETNYf">PressureUnit</span></td><td>Gets the globally configured unit for pressure measurements.</td></tr><tr><td>TimeUnit</td><td><span data-option="4uNWdG4hLVON">MeridiemTime.Unit</span></td><td>Gets the globally configured display unit for time.</td></tr><tr><td>ShowSeconds</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Indicates whether seconds should be displayed in time formatting.</td></tr><tr><td>ShowMilliseconds</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Indicates whether milliseconds should be displayed in time formatting.</td></tr><tr><td>MonthsPerYear</td><td><span data-option="Qi69jhbNvW4D">int</span></td><td>Gets the total number of months configured per year.</td></tr><tr><td>Months</td><td><span data-option="0QNnBTLx765A">MonthData[]</span></td><td>Array containing configuration data for each month in the calendar.</td></tr><tr><td>DaysPerYear</td><td><span data-option="Qi69jhbNvW4D">int</span></td><td>Gets the total calculated number of days in a full calendar year.</td></tr><tr><td>NumericDateFormat</td><td><span data-option="UyKfTmZqoEUh">DateFormat</span></td><td>Gets the order in which month, day, and year are formatted (MDY, DMY, YMD).</td></tr><tr><td>StartingWeekday</td><td><span data-option="KAEZMRLJbfdt">DayOfWeek</span></td><td>Gets the day of the week assigned to the first day of year 0.</td></tr><tr><td>HandleSceneLighting</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether COZY manages scene lighting dynamically.</td></tr><tr><td>UpdateInEditMode</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether COZY updates continuously in Unity Editor edit mode.</td></tr><tr><td>Fog</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether fog rendering is enabled globally.</td></tr><tr><td>FollowCamera</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether the sky dome matches the main camera position.</td></tr><tr><td>Gizmos</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether editor scene view gizmos are drawn.</td></tr><tr><td>Tooltips</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether inspector tooltips are displayed.</td></tr><tr><td>Graphs</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether custom inspector graphs are rendered.</td></tr><tr><td>DontDestroyWeatherOnLoad</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether weather system objects persist across scene loads.</td></tr><tr><td>RenderFXBlocking</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Gets or sets whether FX blocking mask rendering is enabled.</td></tr><tr><td>FXRenderDistance</td><td><span data-option="Qg9dLjdYc4kv">float</span></td><td>Render distance around the camera for weather FX blocking mask.</td></tr><tr><td>FXRenderHeight</td><td><span data-option="Qg9dLjdYc4kv">float</span></td><td>Render height limit for weather FX blocking mask.</td></tr><tr><td>FXBlockingResolution</td><td><span data-option="Qi69jhbNvW4D">int</span></td><td>Resolution of the rendered FX blocking texture.</td></tr><tr><td>FXBlockLayerMask</td><td><span data-option="Qi69jhbNvW4D">int</span></td><td>Layer mask specifying objects that block weather particle effects.</td></tr><tr><td>DisplayMiscEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for miscellaneous events.</td></tr><tr><td>DisplayWeatherEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for weather events.</td></tr><tr><td>DisplayHolidayEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for holiday events.</td></tr><tr><td>DisplayStatusEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for status events.</td></tr><tr><td>DisplayWorldEventEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for world events.</td></tr><tr><td>DisplayPlayerEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for player-related events.</td></tr><tr><td>DisplayNPCEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for NPC-related events.</td></tr><tr><td>DisplayEnemyEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for enemy-related events.</td></tr><tr><td>DisplayAmbientEvents</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Toggles timeline display for ambient events.</td></tr><tr><td>DawnTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the dawn period.</td></tr><tr><td>MorningTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the morning period.</td></tr><tr><td>DayTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the day period.</td></tr><tr><td>AfternoonTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the afternoon period.</td></tr><tr><td>EveningTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the evening period.</td></tr><tr><td>TwilightTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the twilight period.</td></tr><tr><td>NightTimes</td><td><span data-option="bjjENAv9IIcE">MeridiemBlock</span></td><td>Time range definition for the night period.</td></tr><tr><td>Styles</td><td><span data-option="YGXQ7Bl0n1K9">CozyStyle[]</span></td><td>Array of custom inspector styling presets available.</td></tr><tr><td>CurrentStyle</td><td><span data-option="WYVTLi22X9MI">CozyStyle</span></td><td>Gets the active inspector styling preset.</td></tr><tr><td>North</td><td><span data-option="uo932IRNcJ5F">Vector3</span></td><td>Calculated unit vector pointing North relative to sky rotation.</td></tr><tr><td>West</td><td><span data-option="uo932IRNcJ5F">Vector3</span></td><td>Calculated unit vector pointing West relative to sky rotation.</td></tr><tr><td>South</td><td><span data-option="uo932IRNcJ5F">Vector3</span></td><td>Calculated unit vector pointing South relative to sky rotation.</td></tr><tr><td>East</td><td><span data-option="uo932IRNcJ5F">Vector3</span></td><td>Calculated unit vector pointing East relative to sky rotation.</td></tr><tr><td>CloudDownsampling</td><td><span data-option="zOtySybVFnjb">Downsampling</span></td><td>Downsampling quality factor for volumetric cloud rendering.</td></tr><tr><td>FogDownsampling</td><td><span data-option="zOtySybVFnjb">Downsampling</span></td><td>Downsampling quality factor for fog rendering.</td></tr><tr><td>Instance</td><td><span data-option="ger1mdjLQiXL">CozyPreferences</span></td><td>Singleton instance reference of CozyPreferences loaded from Resources.</td></tr><tr><td>Setup</td><td><span data-option="PMvQM2SWda7I">bool</span></td><td>Returns true if the CozyPreferences singleton instance has been successfully initialized.</td></tr><tr><td>Integrations</td><td><span data-option="QaxOCxGuXVQz">List<CozyIntegration></span></td><td>List of active third-party integrations configured for COZY.</td></tr></tbody></table>

### Public Methods

<table><thead><tr><th width="191">Name</th><th width="112.33331298828125">Type<select><option value="FKVfP3lauu2g" label="void" color="blue"></option><option value="YyJp124gDufn" label="CozyStyle" color="blue"></option><option value="3k5JgxZsPE6K" label="SerializedObject" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetDaysPerYear</td><td><span data-option="FKVfP3lauu2g">void</span></td><td>Recalculates and caches the total number of days per year based on current month lengths.</td></tr><tr><td>SelectStyle(int id)</td><td><span data-option="YyJp124gDufn">CozyStyle</span></td><td>Selects and activates a UI style preset by array index.</td></tr><tr><td>SelectStyle(string id)</td><td><span data-option="YyJp124gDufn">CozyStyle</span></td><td>Selects and activates a UI style preset by string identifier.</td></tr><tr><td>GetSerializedSettings</td><td><span data-option="3k5JgxZsPE6K">SerializedObject</span></td><td>Returns a Unity SerializedObject representation of the settings asset (Unity Editor only).</td></tr></tbody></table>

### MonthData Properties

<table><thead><tr><th width="179.66668701171875">Name</th><th width="146.33331298828125">Type<select><option value="pirA3RaufSQ5" label="string" color="blue"></option><option value="M4D4b8dCl1G1" label="int" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>name</td><td><span data-option="pirA3RaufSQ5">string</span></td><td>Display name of the month.</td></tr><tr><td>days</td><td><span data-option="M4D4b8dCl1G1">int</span></td><td>Number of days in the month.</td></tr></tbody></table>
