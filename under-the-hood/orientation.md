---
icon: compass
---

# Orientation

Orientation lets you rotate COZY's sky to match your world. You can change the global orientation in the [preferences.md](../using-cozy/preferences.md "mention") window. These directions _should no&#x74;_&#x62;e changed at runtime as changes will leak into your project data. If you need to change direction at runtime, ensure that you set it back to its original value when the game closes to avoid making permanant changes.

{% hint style="info" %}
COZY does _not_ automatically adjust day length based on sky pitch and rotation rather opting for a stylized approach for more control. To adjust the sun's path through the sky, use the [transit-module.md](../using-cozy/modules/transit-module.md "mention")
{% endhint %}

## Sky Pitch

Control the pitch of the sun in the sky. Positive values move the sun towards the southern hemisphere (giving an appearance of being further north on the planet), negative values move the sun towards the northern hemisphere (giving an appearance of being further south on the planet).

## Sky Rotation

Sets the global North vector. A value of 0 sets the North vector to (1, 0, 0), rotating clockwise over 360°.

## API

<details>

<summary>Get Compass Directions (North, South, East, West)</summary>

```c#
// Grab North
Vector3 north = CozyPreferences.North;
// Grab West
Vector3 north = CozyPreferences.West;

// South and East are derived from North and West (-North and -West)
Vector3 east = CozyPreferences.East;
Vector3 south = CozyPreferences.South;
```

</details>
