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

COZY's stars are created using a cubemap. The cubemap may be rotated based on your needs in the [atmosphere-module](../using-cozy/modules/atmosphere-module/ "mention")

COZY's default star, galaxy, and constellation textures are modified from NASA's [Deep Star Maps 2020](https://svs.gsfc.nasa.gov/4851/)

> NASA/Goddard Space Flight Center Scientific Visualization Studio. Gaia DR2: [ESA/Gaia/DPAC](https://gea.esac.esa.int/archive/documentation/GDR2/Miscellaneous/sec_credit_and_citation_instructions/). Constellation figures based on those developed for the IAU by Alan MacRobert of _Sky and Telescope_ magazine (Roger Sinnott and Rick Fienberg).

## FAQs

### My Scene is Dark at Night!

If your scene is dark at night, there may be a few things at play.&#x20;

#### Your moon directional light is too dim for your post processing setup

Every scene and project are different and different projects may have different goals. If the night is too dark, it may be a good idea to try increasing your moon's directional light intensity in the [atmosphere-module](../using-cozy/modules/atmosphere-module/ "mention").

#### Your ambient lighting is too dim

For the time between sunset and moonrise, there may be a moment that has neither the sun or the moon light very bright in the scene. To avoid this scenario, boost your ambient lighting intensity at the two times that lighting swaps from sun to moon (around 4:30 AM and 7:30 PM). To avoid this looking flat, it would be a good idea to have a harsher gradient from the zenith to the ground ambient colors.&#x20;

<pre class="language-mermaid"><code class="lang-mermaid">graph LR
<strong>  ZA[Zenith A]--> ZB[Zenith B]
</strong>  HA[Horizon A]--> HB[Horizon B]
  GA[Ground A]--> GB[Ground B]
  
    style ZA fill:#9c488b,stroke:#333,stroke-width:2px,color:#fff
    style ZB fill:#d46ebf,stroke:#333,stroke-width:2px,color:#fff
    style HA fill:#805276,stroke:#333,stroke-width:2px,color:#fff
    style HB fill:#805276,stroke:#333,stroke-width:2px,color:#fff
    style GA fill:#42213c,stroke:#333,stroke-width:2px,color:#fff
    style GB fill:#381631,stroke:#333,stroke-width:2px,color:#fff
</code></pre>

#### The Moon is in the Wrong Phase

When using a realistic phase, the moon light will _not_ be the same from night-to-night. On a full moon night, the moon is on the opposite of the Earth from the sun and fully lights the scene.

<img src="../.gitbook/assets/file.excalidraw (11).svg" alt="" class="gitbook-drawing">

When the moon phase is a new moon, the moon is on the same side of the Earth as the sun, and is below the horizon at night. This means that there is **no** directional light in the scene at that time.

<img src="../.gitbook/assets/file.excalidraw (13).svg" alt="" class="gitbook-drawing">

Darker nights is a normal byproduct of this feature. If you want all of your nights to be uniformly bright, you have a few options.

1. Try increasing ambient light
2. Set your moon phase mode to linear and the moon placement to always oppose sun
