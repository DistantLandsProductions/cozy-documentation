---
tags:
  - api
  - tutorial
  - module
---

# Build a Module

## Creating a Module

{% stepper %}
{% step %}
### Create a New Script

Create a new C# script in your project. Name this whatever you like!\
Then, include DistantLands.Cozy and UnityEngine and inherit from CozyModule. Lastly, add the ExecuteAlways, AddComponentMenu, and CozyModule attributes to the class.&#x20;

The CozyModule attribute defines the way that your custom module will be displayed in the editor, as well as its runtime behavior.

```csharp
using DistantLands.Cozy;
using UnityEngine;

/// <summary>
/// Create a custom module for COZY 4
/// </summary>
[ExecuteAlways]
[AddComponentMenu("")]
public class CustomModule : CozyModule
{

}
```
{% endstep %}

{% step %}
### Setup Requirements

#### Add the CozyModule Attribute

Every module made for COZY needs the CozyModule attribute in order to appear in the UI and function properly with other modules. Add the attribute to your class like this

```csharp
[CozyModule("Custom Module", "My Icon", "Description for the module.", "Category", true, 0)]
```

<table><thead><tr><th width="172">Name</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>The display name of the COZY Module</td></tr><tr><td><code>icon</code></td><td>The name of the icon. Must be placed in a Resources/COZY Icons folder (for example, Assets/Resources/COZY Icons/My Icon).</td></tr><tr><td><code>tooltip</code></td><td>The tooltip/description for the module.</td></tr><tr><td><code>category</code></td><td>The title for the category that this module is in in the dropdown. This is case sensitive! Base COZY modules are in these categories, however you can create your own when needed:<br>- Atmosphere<br>- Time<br>- Ecosystem<br>- Integration<br>- Utility</td></tr><tr><td><code>biomeCompatible</code></td><td>Determines if this module can be added to biomes. Requires a module set up for use with a biome (see <a data-mention href="build-a-biome-module.md">build-a-biome-module.md</a>)</td></tr><tr><td><code>priority</code></td><td>Set the priority for executing logic on this module.</td></tr></tbody></table>

#### (Optional) Add Requirements

Your custom module may rely on data from another existing module. In this case, you will need to declare it as a dependency to prevent any issues. You can do so by overriding the `ModuleRequirements` Type array using the `DependsOn` syntax like this:

```c#
public override Type[] ModuleRequirements => DependsOn<CozyClimateModule>();
```

You can also add other requirements using this format

```csharp

public override bool CheckIfModuleCanBeAdded(out string warning)
{
    if (condition)
    {
        warning = "Cannot be removed.";
        return false;
    }

    warning = "";
    return true;
}

public override bool CheckIfModuleCanBeRemoved(out string warning)
{
    if (condition)
    {
        warning = "Cannot be removed.";
        return false;
    }

    warning = "";
    return true;
}
```
{% endstep %}

{% step %}
### Execution

#### Setup/Cleanup

Use the IntializeModule and DeinitializeModule methods to run your setup and cleanup logic for your module

```csharp
/// <summary>
/// Runs setup logic for the module
/// </summary>
public override void InitializeModule()
{
    
}

/// <summary>
/// Runs cleanup logic for the module
/// </summary>
public override void DeinitializeModule()
{
    
}
```

#### Runtime

Modules run several execution events every frame to split execution into different methods. A module is not required to override all of these methods when not needed.

```csharp
/// <summary>
/// Runs first
/// Reset parameters that are modified at runtime
/// </summary>
public override void FrameReset()
{

}

/// <summary>
/// Runs second
/// Update the weights for profiles and applies them to the parameters
/// </summary>
public override void OnUpdateWeatherWeights()
{

}

/// <summary>
/// Runs third
/// Send data to the GPU based on the parameters
/// </summary>
public override void PropagateVariables()
{

}

/// <summary>
/// Runs last
/// Execute runtime logic based on the parameters
/// </summary>
public override void OnCozyUpdateLoop()
{

}
```
{% endstep %}

{% step %}
### Accessing COZY

In order to access COZY's instance in your modules, use the `WeatherSphere` accessor.
{% endstep %}

{% step %}
### Create an Editor

In order to render in the weather manager, your custom module needs an editor script. To get started, create a new C# script in an editor folder in your project. Use this template to get started quickly with a new inspector

<pre class="language-csharp"><code class="lang-csharp">using DistantLands.Cozy.EditorScripts;
using UnityEditor.UIElements;
using UnityEngine.UIElements;
using UnityEngine;
<strong>
</strong><strong>public class CustomModuleEditor : CozyModuleEditor
</strong>{

    VisualElement root;

    public override VisualElement DisplayUI()
    {
        root = new VisualElement();

        // For each property in your module, add a property field. Change variable1 to your variable name
        PropertyField variable1 = new PropertyField();
        variable1.BindProperty(serializedObject.FindProperty("variable1"));
        root.Add(variable1);

        return root;
    }
}
</code></pre>

Learn more about UI Toolkit for more information on working with this: [https://docs.unity3d.com/Manual/UIElements.html](https://docs.unity3d.com/Manual/UIElements.html)
{% endstep %}
{% endstepper %}

## Going Deeper

### Override Existing Functionality

When creating a new module, you may be trying to create a new behavior for an existing feature such as weather control or time control. COZY 4's interface-based design lets you create your own module that can directly interface with other pre-existing modules. Interfaces split modules into individual features, packaged to be easy to implement. Each module may implement as many interfaces as you like.

You can see a list of interfaces that can be overridden in the page for each module.

## Complete Example

### Module

```csharp
using System;
using DistantLands.Cozy;
using UnityEngine;
using UnityEngine.SceneManagement;

/// <summary>
/// Create a custom module for COZY 4
/// </summary>
[ExecuteAlways]
[AddComponentMenu("")]
[CozyModule("Custom Module", "Icons/My Icons", "Description for the module.", "Category", true, 0)]
public class CustomModule : CozyModule
{
    public override Type[] ModuleRequirements => DependsOn<CozyClimateModule>();

    /// <summary>
    /// Runs setup logic for the module
    /// </summary>
    public override void InitializeModule()
    {

    }

    /// <summary>
    /// Runs cleanup logic for the module
    /// </summary>
    public override void DeinitializeModule()
    {

    }

    /// <summary>
    /// Runs first
    /// Reset parameters that are modified at runtime
    /// </summary>
    public override void FrameReset()
    {

    }

    /// <summary>
    /// Runs second
    /// Update the weights for profiles and applies them to the parameters
    /// </summary>
    public override void OnUpdateWeatherWeights()
    {

    }

    /// <summary>
    /// Runs third
    /// Send data to the GPU based on the parameters
    /// </summary>
    public override void PropagateVariables()
    {

    }

    /// <summary>
    /// Runs last
    /// Execute runtime logic based on the parameters
    /// </summary>
    public override void OnCozyUpdateLoop()
    {

    }

}
```
