---
icon: globe
---

# COZY Instance

When you first start with COZY, it may seem overwhelming at first. It can be difficult to know where to even start to make adjustments! This page is designed to help you get a better understanding of how COZY works as a system combining all of the parts needed to make a weather system function in Unity.

## What is it?

The COZY instance refers to the active COZY weather script in your scene; the singleton. It is a special instance of CozySystem.cs that handles the global state of the weather system.

{% hint style="warning" %}
COZY is a singleton system meaning that you can only have **ONE** instance of COZY active at a time. This does not mean that you cannot have different results in different areas, but you need to do this the COZY way through [biomes.md](biomes.md "mention"), [modules](modules/ "mention"), and [profiles](profiles/ "mention").
{% endhint %}

## What does it do?

The instance is responsible for...

1. Holding and managing [modules](modules/ "mention")
2. Managing keywords for [features](features/ "mention")
3. Holding, managing, and blocking [fx-profiles](profiles/fx-profiles/ "mention")
