---
icon: rainbow
---

# Sky

## Gradient

Sets the base vertical gradient for the sky.

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>zenithColor</td><td>color</td><td>Sets the color of the zenith (or top) of the skybox at a certain time. Starts and ends at midnight.</td></tr>
<tr><td>horizonColor</td><td>color</td><td>Sets the color of the horizon (or middle) of the skybox at a certain time. Starts and ends at midnight.</td></tr>
<tr><td>groundColor</td><td>color</td><td>Sets the color of the ground (or bottom) of the skybox at a certain time. Starts and ends at midnight.</td></tr>
<tr><td>zenithExponent</td><td>float</td><td>Controls the exponent used to modulate from the horizon color to the zenith color of the sky.</td></tr>
<tr><td>groundExponent</td><td>float</td><td>Controls the exponent used to modulate from the horizon color to the ground color of the sky.</td></tr>
<tr><td>offset</td><td>float</td><td>Controls the vertical position offset of the sky gradient.</td></tr>
</tbody></table>

## Two Tone

Shades the horizon two different tones based on the sun direction.

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>sunSideColor</td><td>color</td><td>Sets the color of the sun side of the horizon at a certain time. Starts and ends at midnight.</td></tr>
<tr><td>antiSunSideColor</td><td>color</td><td>Sets the color opposite to the sun side of the horizon at a certain time. Starts and ends at midnight.</td></tr>
<tr><td>offset</td><td>float</td><td>Controls the offset used to modulate from the sun side color to the anti-sun side color of the sky.</td></tr>
<tr><td>exponent</td><td>float</td><td>Controls the exponent used to modulate from the sun side color to the anti-sun side color of the sky.</td></tr>
</tbody></table>

## Stars

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color of the star cubemap</td></tr>
<tr><td>cubemap</td><td>Cubemap</td><td>The cubemap used for the stars.</td></tr>
<tr><td>intensity</td><td>float</td><td>Multiplies the color for the stars by a set value</td></tr>
<tr><td>rotationOffset</td><td>float</td><td>Rotates the cubemap around the primary axis. For pitch rotation, use the pitch setting in the COZY Preferences section.</td></tr>
<tr><td>mode</td><td>select</td><td>How often should the star dome rotate?</td></tr>
<tr><td>twinkleAmount</td><td>float</td><td>Sets the amount for stars to fade out when twinkling. A twinkle amount of 0 means no fade, and a twinkle amount of 1 fades completely.</td></tr>
<tr><td>twinkleSpeed</td><td>float</td><td>Sets the rate at which stars twinkle.</td></tr>
<tr><td>twinkleNoise</td><td>Cubemap</td><td>Gives a noise offset for how much stars twinkle.</td></tr>
</tbody></table>

## Constellations

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color of the constellation cubemap. This is multiplied with the star color.</td></tr>
<tr><td>cubemap</td><td>Cubemap</td><td>The cubemap used for the constellations. Aligned with the stars cubemap. Uses the red channel for the alpha of the constellations</td></tr>
<tr><td>intensity</td><td>float</td><td>Multiplies the color for the constellations by a set value</td></tr>
<tr><td>shimmerAmount</td><td>float</td><td>Sets the amount for constellations to fade out one at a time. Constellations use the value in the green channel to determine their offset.</td></tr>
<tr><td>shimmerSpeed</td><td>float</td><td>How quickly will constellations fade in and out.</td></tr>
</tbody></table>

## Galaxy

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>primaryColor</td><td>color</td><td>Sets the main tint color of the galaxy.</td></tr>
<tr><td>secondaryColor</td><td>color</td><td>Sets the secondary accent color of the galaxy.</td></tr>
<tr><td>tertiaryColor</td><td>color</td><td>Sets the tertiary accent color of the galaxy.</td></tr>
<tr><td>intensity</td><td>float</td><td>Multiplies the overall intensity of the galaxy.</td></tr>
<tr><td>cubemap</td><td>Cubemap</td><td>Set the texture for the galaxy</td></tr>
</tbody></table>

## Rainbow

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>placement</td><td>float</td><td>Controls the rotational offset and position of the rainbow in the sky.</td></tr>
<tr><td>texture</td><td>Texture2D</td><td>Sets the rainbow gradient texture.</td></tr>
<tr><td>width</td><td>float</td><td>Sets the width of the rainbow arc.</td></tr>
<tr><td>intensity</td><td>float</td><td>Sets the maximum opacity and brightness of the rainbow. This is modulated by the Climate module.</td></tr>
</tbody></table>

## Light Columns

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color of the light columns.</td></tr>
<tr><td>texture</td><td>Texture2D</td><td>Sets the ribbon texture used for light columns.</td></tr>
<tr><td>intensity</td><td>float</td><td>Sets the brightness intensity of the light columns.</td></tr>
<tr><td>height</td><td>float</td><td>Controls the vertical height scale of the light columns.</td></tr>
<tr><td>position</td><td>float</td><td>Controls the horizontal positioning of the light columns.</td></tr>
</tbody></table>

## Shooting Stars

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the main color of the shooting stars.</td></tr>
<tr><td>secondaryColor</td><td>color</td><td>Sets the secondary trailing color of the shooting stars.</td></tr>
<tr><td>intensity</td><td>float</td><td>Sets the brightness intensity of the shooting stars.</td></tr>
<tr><td>lifetime</td><td>float</td><td>Controls how long each shooting star remains visible.</td></tr>
<tr><td>particleCount</td><td>float</td><td>Sets the maximum number of shooting stars that can spawn concurrently.</td></tr>
<tr><td>width</td><td>float</td><td>Sets the width of the shooting star trail.</td></tr>
<tr><td>travelDistance</td><td>float</td><td>Sets the distance traveled by each shooting star during its lifetime.</td></tr>
<tr><td>delay</td><td>float</td><td>Sets the delay interval between shooting star spawns.</td></tr>
</tbody></table>

## Sun Disk

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>haloColor</td><td>color</td><td>Sets the color of the solar halo.</td></tr>
<tr><td>haloFalloff</td><td>float</td><td>Controls the falloff rate for the solar halo fading outwards.</td></tr>
<tr><td>color</td><td>color</td><td>Sets the color of the sun disk sprite.</td></tr>
<tr><td>size</td><td>float</td><td>Sets the scale size of the sun disk in the sky.</td></tr>
<tr><td>texture</td><td>Texture2D</td><td>Sets the texture used for rendering the sun disk.</td></tr>
</tbody></table>

## Moon Disk

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>displayStyle</td><td>select</td><td>Sets the display style for the moon.</td></tr>
<tr><td>placementMode</td><td>select</td><td>Sets the placement mode for the moon.</td></tr>
<tr><td>phaseMode</td><td>select</td><td>Determines the phase mode used for the moon.</td></tr>
<tr><td>color</td><td>color</td><td>Sets the color of the moon sprite in the sky.</td></tr>
<tr><td>size</td><td>float</td><td>Sets the size of the moon sprite in the sky.</td></tr>
<tr><td>rotation</td><td>float</td><td>Changes the orientation of the moon sprite in the sky.</td></tr>
<tr><td>texture</td><td>Texture2D</td><td>Sets the texture used for the moon.</td></tr>
<tr><td>normalMap</td><td>Texture2D</td><td>Sets the normal map used for the moon.</td></tr>
<tr><td>normalStrength</td><td>float</td><td>Sets the strength of the normal map for the moon.</td></tr>
<tr><td>declination</td><td>float</td><td>Sets the strength of the declination. Declination offsets the moon from the celestial plane (in line with the sun). Moves back and forth following a sine wave.</td></tr>
<tr><td>declinationPeriod</td><td>float</td><td>Set the number of days between full cycles of declination.</td></tr>
<tr><td>declinationOffset</td><td>float</td><td>Offsets the period for the sine wave of declination.</td></tr>
<tr><td>orbitPeriod</td><td>float</td><td>Set the number of days between full cycles the orbit.</td></tr>
<tr><td>orbitOffset</td><td>float</td><td>Offsets the period for the orbit.</td></tr>
</tbody></table>
