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

