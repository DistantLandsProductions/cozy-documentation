---
icon: ban
cover: ../../.gitbook/assets/image (20).png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
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
---

# FX Blocking

In case you haven't noticed, rain doesn't fall inside your house (ideally). COZY ships with two different FX blocking systems that are used depending on what FX system you are using.

## VFX Graph

### The Problem

[VFX Graph](https://docs.unity3d.com/Packages/com.unity.visualeffectgraph@17.5/manual/index.html) is an entirely GPU based particle system that can more efficiently render moving particles using [compute shaders](https://docs.unity3d.com/6000.5/Documentation/Manual/class-ComputeShader.html) authored through a node-based graph. While VFX Graph is incredibly efficient as a result, there are also tradeoffs. One such tradeoff, is that VFX cannot interact with physics and thus cannot interact with colliders. Because of this tradeoff in performance, we need to come up with a custom

### The Solution

To fake collisions for VFX Graph, a top down volume is rendered of the scene at runtime.

{% hint style="warning" %}
If you are not using VFX Graph or do not want to waste computation on additional collision logic, disable VFX Graph Blocking in the [preferences.md](../preferences.md "mention")
{% endhint %}

### API

## Shuriken

