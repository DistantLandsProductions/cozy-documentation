---
tags:
  - integration
  - api
  - tutorial
---

# Build an Integration

A weather system is only as effective as the world it lives in. With COZY integrations, easily add support for any third-party plugin directly within the COZY UI.

## What is an Integration?

An integration in COZY is a system that functions as a bridge between the COZY system and any other third party code. The most important thing about an integration is that it needs to be decoupled from any direct COZY code or any third party code. This lets packages be removed when needed without breaking operations.

## Creating an Integration

Creating an integration for a third party package is simple!

{% stepper %}
{% step %}
### Create a New C# Script

Create a new script that derives from CozyIntegration and has the `[Serializable]` and `[CozyIntegration]` attributes

<pre class="language-csharp" data-expandable="true"><code class="lang-csharp">// Base script for an integration

#if COZY_WEATHER

using System;
using UnityEngine;
using DistantLands.Cozy;

[Serializable]
[CozyIntegration(true, false, "Custom Integration", "IconPath", "https://yoursite.com")]
<strong>public class CustomCozyIntegration : CozyIntegration
</strong>{
    
}

#endif
</code></pre>

{% hint style="info" %}
Use conditional compilation to ensure that this code does not compile if COZY is not installed. If you are a third party asset provider, you can include this code with your asset and it will not cause errors in a user's project _unless_ they import COZY 4 and then remove it.
{% endhint %}

The `CozyIntegration` Attribute tells the integrations window, A.) this class is an integration to display, and B.) how to display the settings for this integration.

<table><thead><tr><th width="169">Name</th><th width="90.7142333984375">Type<select><option value="ndIdXyLYwgYx" label="bool" color="blue"></option><option value="M6up4sBWzCtY" label="string" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>displayToggle</td><td><span data-option="ndIdXyLYwgYx">bool</span></td><td>Should a toggle to enable and disable this integration be visible in the window</td></tr><tr><td>displayApplyButton</td><td><span data-option="ndIdXyLYwgYx">bool</span></td><td>Should a button to apply the integration be exposed?</td></tr><tr><td>name</td><td><span data-option="M6up4sBWzCtY">string</span></td><td>The display name for the integration</td></tr><tr><td>iconPath</td><td><span data-option="M6up4sBWzCtY">string</span></td><td>The path for the icon for the integration. Must be placed in a Resources folder.</td></tr><tr><td>packageLink</td><td><span data-option="M6up4sBWzCtY">string</span></td><td>URL for the package or documentation</td></tr></tbody></table>
{% endstep %}

{% step %}
### Setup Installation Checks

An integration has three required sanity checks for different installation scenarios

#### PackageInstalled

The `PackageInstalled` bool returns true if the third party package is installed. For any integration that ships with the code that it integrates with, this can always be true. Otherwise, it should be wrapped in a conditional compilation statement

{% code expandable="true" %}
```csharp
    public class CustomCozyIntegration : CozyIntegration
    {
        public override bool PackageInstalled
        {
            get
            {
#if COMPILER // <- Replace with your conditional compiler
                return true;
#else
                return false;
#endif
            }
        }
```
{% endcode %}

#### IntegrationInstalled

The `IntegrationInstalled` bool is used to check if any additional importing is needed for the integration to work properly. For most integrations, this is always true:

{% code expandable="true" %}
```csharp
        public override bool IntegrationInstalled => true;
```
{% endcode %}

For any integration that needs additional changes (generally shader integrations like water shaders, etc.) in order to function, a check can be implemented here. This example is taken from Crest 5's integration:

{% code expandable="true" %}
```csharp
        public override bool IntegrationInstalled
        {
            get
            {
#if COZY_CREST
                // ShaderGraphPatcher is a COZY editor utility that makes shader changes
                return ShaderGraphPatcher.Installed("Packages/com.waveharmonic.crest/Runtime/Shaders/Surface/Water.shadergraph");
#else
                return false;
#endif
            }
        }

```
{% endcode %}

This works hand in hand with the `ApplyIntegration()` and `UnapplyIntegration()` functions:

```csharp
    public override void ApplyIntegration()
    {
        ShaderGraphPatcher.PatchShader("Packages/com.waveharmonic.crest/Runtime/Shaders/Surface/Water.shadergraph", "SurfaceDescription.Emission");
    }

    public override void UnapplyIntegration()
    {
        ShaderGraphPatcher.UnpatchShader("Packages/com.waveharmonic.crest/Runtime/Shaders/Surface/Water.shadergraph", "SurfaceDescription.Emission");
    }
```

#### CheckStatus

`CheckStatus` checks the current active status of the integration in the scene. If your third party package uses a manager (or something similar) in the scene, use this method to ensure that it is in the scene. It also has a string `out` parameter that lets you send more details about the status:

{% code expandable="true" %}
```csharp
        public override bool CheckStatus(out string errorMessage)
        {
            if (yourIntegration.Instance) {
                errorMessage = "";
                return true;
            }
            else 
            {
                errorMessage = "No instance in the scene!";
                return false;
            }
        }
```
{% endcode %}
{% endstep %}

{% step %}
### Running Logic

The only time that the integration code runs at runtime is when COZY is initialized and deinitialized (runs with the `OnEnable` and `OnDisable` methods).

{% code expandable="true" %}
```csharp
        public override void Initialize()
        {
#if COMPILER
            if (CozyWeather.Instance != null) weather = CozyWeather.Instance;
            
            // Subscribe to the update loop if you need logic to run every frame
            CozyWeather.CozyUpdateLoop += UpdateIntegration;

            // Run additional setup checks here
#endif
        }

        private void UpdateIntegration()
        {
#if !COMPILER
            return;
#else
            if (!ActiveAndEnabled) return;
            if (CozyWeather.Instance == null) return;

            // Run update logic here
#endif
        }

        public override void Deinitialize()
        {
#if COMPILER
            // Unsubscribe to events to stop the update loop
            CozyWeather.CozyUpdateLoop -= UpdateIntegration;
#endif
        }
```
{% endcode %}
{% endstep %}

{% step %}
### Expose Properties

Any public properties in the class are automatically exposed to the settings window. Declare them like any other variables in a class.

{% code expandable="true" %}
```csharp
    public class CustomCozyIntegration : CozyIntegration
    {
        public float floatA;
        public bool boolB;
        ...
```
{% endcode %}
{% endstep %}
{% endstepper %}

## Complete Integration Setup

Feel free to copy this code to build your integration:

{% code expandable="true" %}
```cs
// COZY Integration
#if COZY_WEATHER

using System;
using UnityEngine;
using DistantLands.Cozy;

[Serializable]
[CozyIntegration(true, false, "Custom Integration", "IconPath", "https://yoursite.com")]
public class CustomCozyIntegration : CozyIntegration
{
    public float floatA;
    public bool boolB;
    
    public override bool PackageInstalled
    {
        get
        {
#if COMPILER // <- Replace with your conditional compiler
            return true;
#else
            return false;
#endif
        }
    }
    
    public override bool IntegrationInstalled => true;
    
    public override bool CheckStatus(out string errorMessage)
    {
        errorMessage = "";
        return true;
    }
    
    public override void Initialize()
    {
#if COMPILER
        if (CozyWeather.Instance != null) weather = CozyWeather.Instance;
        
        // Subscribe to the update loop if you need logic to run every frame
        CozyWeather.CozyUpdateLoop += UpdateIntegration;

        // Run additional setup checks here
#endif
    }

    private void UpdateIntegration()
    {
#if !COMPILER
        return;
#else
        if (!ActiveAndEnabled) return;
        if (CozyWeather.Instance == null) return;

        // Run update logic here
#endif
    }

    public override void Deinitialize()
    {
#if COMPILER
        // Unsubscribe to events to stop the update loop
        CozyWeather.CozyUpdateLoop -= UpdateIntegration;
#endif
    }
    public override void ApplyIntegration()
    {

    }

    public override void UnapplyIntegration()
    {

    }
}
#endif
```
{% endcode %}

## Inclusion in Package

I am always looking for new integrations to include in the base package. If you have developed an integration that would be useful for COZY 4, please reach out to me via email or Discord
