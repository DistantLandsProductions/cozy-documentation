---
icon: stars
---

# Moon and Stars

## Moon

The moon system handles both the visual rendering of the moon disk in the sky and the physical directional light it casts into your scene.

The moon is controlled by the [moon feature](../using-cozy/features/sky.md#moon-disk) and the [atmosphere-module](../using-cozy/modules/atmosphere-module/ "mention")

### Moon Phase

The moon's phase represents how much of the moon is currently illuminated.

* Placement Modes: The way the moon phase is calculated depends on your chosen Placement Mode. In `Realistic` mode, the phase is physically driven by the angle between the Sun and the Moon in the sky. In `Always Oppose Sun` mode, the phase is artificially driven by the orbit period to ensure consistent lighting.
* Lens Flare Scaling: If you are using moon lens flares, note that the intensity and scale of the flare are directly tied to the moon's phase. A full moon will cast a maximum-size lens flare, a crescent moon will have a proportionally smaller and dimmer flare, and a new moon (0% phase) will render no flare at all.

### Positioning

The moon travels across the sky based on your orbit and declination settings.

> Important Note on Moonset: To prevent the moon's directional light from shining straight up through the bottom of your terrain, the system uses a Minimum Angle clamp. As the moon sets, the physical Directional Light will stop rotating once it hits this minimum angle, even though the visual moon disk in the sky will continue to set below the horizon.

### Lighting and Shadows

The moon acts as a secondary directional light source for night scenes, but it comes with a few built-in optimizations to keep performance high and lighting looking natural.

* Shadow Priority: The system only allows one primary shadow caster at a time to save on rendering costs. The moon will only cast shadows if the sun is completely disabled. If both the sun and moon are active and above the horizon simultaneously, the sun takes priority and moon shadows are automatically disabled.
* Horizon Fade-Out: To mimic atmospheric scattering and prevent harsh lighting at grazing angles, the moon's light intensity automatically fades out as it approaches the horizon. If you are trying to manually force a very bright moon at the horizon and find the intensity is lower than expected, this automatic fade-out is the cause.

### Custom Moon Textures

You can replace the default moon disk texture with your own custom textures, but your texture file must be authored correctly for the sky shader to function.

{% hint style="info" %}
Your custom moon texture must have an active Alpha channel where the background is completely transparent. The sky shader relies on this alpha channel to create a culling mask (so the sky and stars aren't drawn over the moon). If you use a texture without an alpha channel (like a standard JPEG), the system will draw a solid black square around your moon.
{% endhint %}

## Stars

### Constellations



### Shooting Stars

