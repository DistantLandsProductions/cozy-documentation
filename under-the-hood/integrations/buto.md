---
cover: ../../.gitbook/assets/image (48).png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: full
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
tags:
  - integration
---

# Buto

> Buto is a powerful volumetric lighting and volumetric fog asset for Unity URP. It provides you with a wide range of advanced features to take your game's atmosphere to the next level.

<p align="center"><a href="https://assetstore.unity.com/packages/vfx/shaders/fullscreen-camera-effects/buto-volumetric-fog-and-volumetric-lighting-for-urp-258881?aid=1011luj9X" class="button secondary">Purchase</a></p>

## Installation

Requires no further installation once Buto and COZY 4 are both installed.

## Scene Setup

Create a new Global Volume with a Buto volume component in your scene. Once this is done, COZY will automatically take control of the volume and apply the fog colors to that volume.

<figure><img src="../../.gitbook/assets/image (49).png" alt="" width="563"><figcaption></figcaption></figure>

## Configuration

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

### Fog Brightness Multiplier

Multiplies the fog brightness by a coefficient

### Fog Density Multiplier

Multiplies the fog density by a coefficient

## Limitations

### Volumetric Clouds

Due to the way that Buto is rendered, it will always render over the volumetric clouds. This can cause issues where the bottom of the cloud is cutoff when flying through clouds as seen here:

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

### Global Volume

COZY will automatically assign the first available global volume with a Buto component as the main Buto instance. If you are using other global volumes that you blend based on weights, these will not also be adjusted by COZY. I recommend using COZY's Atmosphere Biome Modules to get around this.

### Data Sanctity

Buto is managed through the Volume system in Unity. Due to the way that the volume system works, the only way to dynamically change the values used by Buto (without interpolating mutliple volumes) is to make changes to the volume data. This is technically a breach of the data layer and may appear as a change in your version control.&#x20;
