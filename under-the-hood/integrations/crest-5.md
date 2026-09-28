---
cover: ../../.gitbook/assets/image (42).png
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

# Crest 5

> Crest is a class-leading water system authored by professional game developers.

<p align="center"><a href="https://assetstore.unity.com/packages/tools/particles-effects/crest-water-5-oceans-rivers-lakes-268614?aid=1011luj9X" class="button secondary">Purchase</a></p>

{% hint style="warning" %}
Important! Crest 5 is only supported with Planar reflections enabled. See [#reflections](crest-5.md#reflections "mention") for more information
{% endhint %}

## Installation

Once Crest 5 and COZY 4 are installed, you will need to install the integration node into Crest 5's shader graph.&#x20;

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Pressing install will inject a node directly into the shader graph right before the emission is sent out of the shader. If you update Crest 5, you will need to reinstall the integration.

## Scene Setup

Integration requires no scene setup.

## Configuration

No settings for this integration.

## Limitations

### Reflections

Crest 5 is only supported with Planar reflections enabled. This is because Crest 5 is made with shader graph and adds reflections after the color is passed to the COZY Fog node. If these reflections are still enabled, the water in your scene will be slightly too light compared to other objects in the fog.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<p align="center">Planar Reflections Disabled</p>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

<p align="center">Planar Reflections Enabled</p>
{% endcolumn %}
{% endcolumns %}

Be aware that this is a limitation of the integration and would require a major change to Crest 5 in order to work properly without planar reflections enabled. For performance, another workaround is disabling reflections completely on the water surface, however this has the downside of reducing the visual fidelity of the water.
