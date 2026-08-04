---
icon: cube
tags:
  - biome
---

# Biomes

Biomes define custom settings for a specific volume or area in COZY and behave very similarly to Unity's [Volume](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/Volumes.html) system.

## Biome Control

### Global vs. Local

Biomes can be controlled in one of two ways: global or local volumes. A global biome will always apply its effect (based on its weight and priority) no matter where the [track-point.md](utilities/track-point.md "mention") is. Local biomes are limited to an area defined by colliders or splines and will interpolate their weight based on a transition distance.

#### Biome Shapes

Local biomes can be defined by colliders or splines. In order to add a shape to your biome, create a new game object with a collider or spline and add it as a child under the biome. As many colliders and splines as you need may be added to define the shape exactly as needed!

### Weight

Biomes are applied based on a weight value. This weight determines how much the biomes are lerped in. At a weight of 0, the biome is not applied at all. At a weight of 1, the biome is completely applied.

### Priority

Priority lets you define biomes within biomes and sort them based on priority. Areas with higher priority _override_ areas of low priority. For example, say you have an evil island on your map and need the fog to be dense and dark while in that region.

<img src="../.gitbook/assets/file.excalidraw (9).svg" alt="" class="gitbook-drawing">

Inside that evil island, you might want a smaller zone that defines a volcano region with reddish fog.

<img src="../.gitbook/assets/file.excalidraw (10).svg" alt="" class="gitbook-drawing">

You don't want to have a cutout in your evil island biome, so you would assign a higher priority to the volcano biome to allow it to override the evil island biome

## Biome Modules

Biomes apply changes in the same way as the [cozy-instance.md](cozy-instance.md "mention"); using modules to manage instances of data. Not all modules are supported on biomes.

## Usage Examples

<details>

<summary>Creating a Biome</summary>

{% stepper %}
{% step %}
#### Create the Object

Navigate to GameObject/Distant Lands/COZY: Stylized Weather 4/Create (Global or Local) Biome

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Add Biome Module

Use the <i class="fa-plus">:plus:</i> icon in the UI to add new modules to your biome.
{% endstep %}

{% step %}
#### (Optional) Define an Area for a Local Biome

Add colliders or spline containers to your biome to define an area that the biome will be applied in
{% endstep %}
{% endstepper %}



</details>

<details>

<summary>Adjust Weight at Runtime</summary>



</details>



## API
