---
icon: cloud
---

# Clouds

## Volumetric

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement. Textures are packed such that the B value determines the cloud density</td></tr>
<tr><td>noiseTexture</td><td>Texture3D</td><td>Sets the texture volumetric for erosion and detailing</td></tr>
<tr><td>height</td><td>float</td><td>Sets the height of the cumulus layer</td></tr>
<tr><td>darkeningIntensity</td><td>float</td><td>Darkens the cloud layer in thick clouds</td></tr>
<tr><td>litColor</td><td>color</td><td>Sets the color of the lit clouds</td></tr>
<tr><td>shadeColor</td><td>color</td><td>Sets the color of the shaded clouds</td></tr>
<tr><td>placementScale1</td><td>float</td><td>Sets the primary scale for volumetric cloud placement mask.</td></tr>
<tr><td>placementScale2</td><td>float</td><td>Sets the secondary scale for volumetric cloud placement mask.</td></tr>
<tr><td>density</td><td>float</td><td>Sets the density of the volumetric layer</td></tr>
<tr><td>noiseScale</td><td>float</td><td>Sets the scale of the noise for the volumetric layer</td></tr>
<tr><td>noiseAmount</td><td>float</td><td>Controls the strength of noise erosion on cloud edges.</td></tr>
<tr><td>placementHeight</td><td>float</td><td>Sets the base elevation height where volumetric cloud rendering starts.</td></tr>
<tr><td>ramp</td><td>Texture2D</td><td>Ramp texture driving height-based density and lighting gradients.</td></tr>
<tr><td>stepSize</td><td>float</td><td>Sets the raymarching sample step distance inside the clouds.</td></tr>
<tr><td>steps</td><td>float</td><td>Sets the total number of raymarching sample iterations.</td></tr>
<tr><td>lODCoefficient</td><td>float</td><td>Controls the distance-based level of detail reduction factor.</td></tr>
<tr><td>lODSteps</td><td>float</td><td>Sets the reduced raymarching step count applied at distance.</td></tr>
<tr><td>blueNoise</td><td>Texture2D</td><td>Blue noise texture used for jittering raymarch offsets to reduce banding.</td></tr>
<tr><td>windStrength</td><td>float</td><td>Controls how strongly wind speeds move the volumetric cloud noise.</td></tr>
<tr><td>highlightBrightness</td><td>float</td><td>Sets the intensity brightness of light highlights along cloud edges.</td></tr>
<tr><td>highlightStepSize</td><td>float</td><td>Sets the raymarching step size for computing light highlights.</td></tr>
</tbody></table>

## Cumulonimbus

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement. Textures are packed such that the B value determines the cloud density</td></tr>
<tr><td>ramp</td><td>Texture2D</td><td>Ramp texture driving height-based density and lighting gradients.</td></tr>
</tbody></table>

## Cumulus

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement. Textures are packed such that the B value determines the cloud density</td></tr>
<tr><td>erosionTexture</td><td>Texture2D</td><td>Sets the texture used for erosion and detailing</td></tr>
<tr><td>height</td><td>float</td><td>Sets the height of the cumulus layer</td></tr>
<tr><td>litColor</td><td>color</td><td>Sets the color of the lit clouds</td></tr>
<tr><td>shadeColor</td><td>color</td><td>Sets the color of the shaded clouds</td></tr>
<tr><td>thickness</td><td>float</td><td>Sets the thickness of the cumulus layer for fake lighting</td></tr>
<tr><td>density</td><td>float</td><td>Sets the density of the cumulus layer</td></tr>
<tr><td>windStrength</td><td>float</td><td>Controls the movement speed of the cumulus cloud layer based on wind.</td></tr>
<tr><td>cohesion</td><td>float</td><td>Sets the cohesion of the cumulus layer</td></tr>
</tbody></table>

## Altocumulus

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement.</td></tr>
<tr><td>height</td><td>float</td><td>Sets the height of the layer</td></tr>
<tr><td>textureScale</td><td>Vector3</td><td>Sets the scale of the cirrus texture</td></tr>
<tr><td>color</td><td>color</td><td>Sets the color of the clouds</td></tr>
<tr><td>density</td><td>float</td><td>Sets the density of the layer</td></tr>
<tr><td>ramp</td><td>float</td><td>Controls the power for each individual cloud.</td></tr>
<tr><td>windStrength</td><td>float</td><td>Controls the movement speed of the layer based on wind.</td></tr>
</tbody></table>

## Cirrus

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement. Textures are packed such that the B value determines the cloud density</td></tr>
<tr><td>height</td><td>float</td><td>Sets the height of the layer</td></tr>
<tr><td>textureScale</td><td>Vector3</td><td>Sets the scale of the texture</td></tr>
<tr><td>color</td><td>color</td><td>Sets the color of the clouds</td></tr>
<tr><td>density</td><td>float</td><td>Sets the density of the layer</td></tr>
<tr><td>windStrength</td><td>float</td><td>Controls the movement speed of the cloud layer based on wind.</td></tr>
<tr><td>wispFactor</td><td>float</td><td>Sets the power of the layer</td></tr>
</tbody></table>

## Contrails

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th></tr></thead><tbody>
<tr><td>mainTexture</td><td>Texture2D</td><td>Sets the main texture used for placement.</td></tr>
<tr><td>height</td><td>float</td><td>Sets the height of the layer</td></tr>
<tr><td>textureScale</td><td>Vector3</td><td>Sets the scale of the texture</td></tr>
<tr><td>color</td><td>color</td><td>Sets the color of the lit clouds</td></tr>
<tr><td>density</td><td>float</td><td>Sets the density of the layer</td></tr>
<tr><td>windStrength</td><td>float</td><td>Controls the movement speed of the cloud layer based on wind.</td></tr>
</tbody></table>
