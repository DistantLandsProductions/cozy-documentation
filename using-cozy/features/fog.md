---
icon: cloud-fog
---

# Fog

## Gradient

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color1</td><td>color</td><td>Sets the primary fog color band.</td></tr>
<tr><td>color2</td><td>color</td><td>Sets the secondary fog color band.</td></tr>
<tr><td>color3</td><td>color</td><td>Sets the tertiary fog color band.</td></tr>
<tr><td>color4</td><td>color</td><td>Sets the quaternary fog color band.</td></tr>
<tr><td>color5</td><td>color</td><td>Sets the quinary fog color band.</td></tr>
<tr><td>density1</td><td>float</td><td>Sets the density value for the primary fog band.</td></tr>
<tr><td>density2</td><td>float</td><td>Sets the density value for the secondary fog band.</td></tr>
<tr><td>density3</td><td>float</td><td>Sets the density value for the tertiary fog band.</td></tr>
<tr><td>density4</td><td>float</td><td>Sets the density value for the quaternary fog band.</td></tr>
<tr><td>density5</td><td>float</td><td>Sets the density value for the quinary fog band.</td></tr>
<tr><td>start1</td><td>float</td><td>Sets the start distance for the primary fog band.</td></tr>
<tr><td>start2</td><td>float</td><td>Sets the start distance for the secondary fog band.</td></tr>
<tr><td>start3</td><td>float</td><td>Sets the start distance for the tertiary fog band.</td></tr>
<tr><td>start4</td><td>float</td><td>Sets the start distance for the quaternary fog band.</td></tr>
<tr><td>start5</td><td>float</td><td>Sets the start distance for the quinary fog band.</td></tr>
</tbody></table>

## Sun Light Flare

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color tint of the sun fog light flare.</td></tr>
<tr><td>squish</td><td>float</td><td>Controls the squish/distortion shape of the light flare.</td></tr>
<tr><td>intensity</td><td>float</td><td>Sets the intensity brightness of the sun light flare.</td></tr>
<tr><td>falloff</td><td>float</td><td>Controls the falloff rate for the light flare effect.</td></tr>
<tr><td>minDistance</td><td>float</td><td>Sets the minimum rendering distance for the light flare.</td></tr>
<tr><td>maxDistance</td><td>float</td><td>Sets the maximum rendering distance for the light flare.</td></tr>
</tbody></table>

## Moon Light Flare

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color tint of the moon fog light flare.</td></tr>
<tr><td>squish</td><td>float</td><td>Controls the squish/distortion shape of the light flare.</td></tr>
<tr><td>intensity</td><td>float</td><td>Sets the intensity brightness of the moon light flare.</td></tr>
<tr><td>falloff</td><td>float</td><td>Controls the falloff rate for the light flare effect.</td></tr>
<tr><td>minDistance</td><td>float</td><td>Sets the minimum rendering distance for the light flare.</td></tr>
<tr><td>maxDistance</td><td>float</td><td>Sets the maximum rendering distance for the light flare.</td></tr>
</tbody></table>

## Two Tone

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>sunSideColor</td><td>color</td><td>Sets the fog color facing toward the sun direction.</td></tr>
<tr><td>antiSunSideColor</td><td>color</td><td>Sets the fog color facing away from the sun direction.</td></tr>
<tr><td>sunSideDensity</td><td>float</td><td>Controls the density of the fog facing toward the sun direction.</td></tr>
<tr><td>antiSunSideDensity</td><td>float</td><td>Controls the density of the fog facing away from the sun direction.</td></tr>
<tr><td>smoothness</td><td>float</td><td>Controls the blend smoothness between sun side and moon side fog.</td></tr>
<tr><td>offset</td><td>float</td><td>Controls the directional offset separating the sun and moon fog colors.</td></tr>
</tbody></table>

## Height

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>color</td><td>color</td><td>Sets the color tint of the height fog.</td></tr>
<tr><td>falloff</td><td>float</td><td>Controls how quickly height fog dissipates vertically.</td></tr>
<tr><td>smoothness</td><td>float</td><td>Controls the softness transition for height fog bounds.</td></tr>
<tr><td>baseHeight</td><td>float</td><td>Sets the base elevation plane where height fog starts.</td></tr>
<tr><td>density</td><td>float</td><td>Sets the overall density of the height fog layer.</td></tr>
<tr><td>variationNoise</td><td>Texture3D</td><td>Set the texture used for noise variation.</td></tr>
<tr><td>variationAmount</td><td>float</td><td>Control the amount of variation</td></tr>
<tr><td>variationTextureScale</td><td>Vector3</td><td>Sets the scale of the height fog variation</td></tr>
<tr><td>variationTextureFlow</td><td>Vector3</td><td>Sets the movement speed and direction of the height fog variation</td></tr>
</tbody></table>

## Base

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>densityMultiplier</td><td>float</td><td>Global multiplier applied to overall fog density.</td></tr>
<tr><td>height</td><td>float</td><td>Sets the base elevation height for fog in the background.</td></tr>
<tr><td>smoothness</td><td>float</td><td>Controls the transition smoothness of the fog in the background.</td></tr>
<tr><td>baseHeight</td><td>float</td><td>Sets the base height (in meters) for the foreground fog.</td></tr>
<tr><td>baseSmoothness</td><td>float</td><td>Sets the base smoothness (in meters) for the foreground fog.</td></tr>
<tr><td>transitionDistance</td><td>float</td><td>Sets the distance (in meters) that the fog will transition from the height-based fog (foreground) to the angle-based fog (background).</td></tr>
</tbody></table>
