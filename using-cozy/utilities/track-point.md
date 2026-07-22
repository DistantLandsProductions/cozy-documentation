---
icon: arrows-to-circle
---

# Track Point

## Overview

Rather than being forced to place everything relative to the main camera like in previous versions, COZY 4 introduces a track point that centers your FX accordingly.

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th></th></tr></thead><tbody><tr><td align="center"><h2><i class="fa-arrows-to-circle" style="color:green;">:arrows-to-circle:</i></h2></td><td align="center"><h3>Follows Track Point</h3></td><td><ul><li>Biome calculation</li><li>FX (audio, particles and VFX Graph)</li></ul></td></tr><tr><td align="center"><h2><i class="fa-ban" style="color:red;">:ban:</i></h2></td><td align="center"><h3>Does Not Follow Track Point</h3></td><td><ul><li>Actual weather manager</li><li>Directional lights</li></ul></td></tr></tbody></table>

A track point is _not_ required, but will give you the most flexibility when developing. For an isometric game for example, you would want your FX and biome calculation to be done relative to the player as opposed to the camera.

{% hint style="info" %}
When a track point is not in use, the [Main Camera](https://docs.unity3d.com/6000.7/Documentation/ScriptReference/Camera-main.html) will be used as a pivot point
{% endhint %}

## Setting a Track Point

To set a track point, simply add the Track Point component to any game object. This will automatically be assigned as the track point in your scene!

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
You can have **only** **one** track point in your scene at a time. Any others will be destroyed.
{% endhint %}
