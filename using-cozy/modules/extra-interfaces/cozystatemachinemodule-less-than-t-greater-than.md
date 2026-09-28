---
description: 'T : CozyProfile, IStateMachineProfile'
icon: arrows-turn-to-dots
---

# CozyStateMachineModule\<T>

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Base/CozyStateMachineModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

The state machine module is a base class for any modules that use a state machine to blend between playable profiles over time. This data can then be used to call the Play function on the generic profile based on the weights for each assigned profile.

## Overview

Many modules in COZY require a state machine in order to function properly. Most notably, the [ambience-module](../ambience-module/ "mention"), [weather-module](../weather-module/ "mention"), and the [resound.md](../../../extensions/resound.md "mention") extension all use state machines to determine when profiles play, how profiles are resolved, etc. The StateMachineModule is a parent class that holds features like biome blending, profile resolution, setting and changing profiles over time, and more.

## Build Your Own

Using this parent class, it is simple to build your own modules that use a state machine fro whatever features you need to implment! This example uses a pre-set queue to play profiles one after the other.

{% hint style="info" %}
See [build-a-module](../../../extending-cozy/build-a-module/ "mention") for more information on how to build your own modules to extend COZY
{% endhint %}

{% stepper %}
{% step %}
### Create a Profile

A StateMachineModule requires a playable profile that implements CozyProfile and IStateMachineProfile. This can hold any data, but must implement the interface. Create a new C# file and place it anywhere in your project.

```cs
// Profile used for a state machine
using DistantLands.Cozy;

public class StateProfile : CozyProfile, IStateMachineProfile
{
    public MeridiemTimeDelta MinTime = minTime;
    [SerializeField]
    private MeridiemTimeDelta minTime = new MeridiemTimeDelta(0,30);
    public MeridiemTimeDelta MaxTime = maxTime;
    [SerializeField]
    private MeridiemTimeDelta maxTime = new MeridiemTimeDelta(1,00);
    
    /// <summary>
    /// Runs when the profile plays
    /// </summary>
    /// <param name="weight">0-1 float that is determined by the current weight of this profile</param>
    public void Play(float weight)
    {
        Debug.Log($"Playing {name} at a weight of {weight}");
    }
}
```
{% endstep %}

{% step %}
### Create the Module

Once that is done, you are ready to create your own module! Use this script example to see how this can be done. Create a new C# file and place it anywhere in your project.

```csharp
// State Machine Module

[ExecuteAlways]
[AddComponentMenu("")]
[CozyModule("My State Machine", "Your/IconPath", "State machine tutorial code", "Tutorial", true)]
public class MyStateMachineModule : CozyStateMachineModule<StateProfile>
{
    public StateProfile[] profileQueue;
    private int queueIndex;
    
    // Checks to see if the state machine timer should be updated. If so, the profiles 
    // will automatically change when thyy are finihsed
    public override bool UpdateStateMachineTimer => true;
    
    // Set the intial behavior for the system
    public override void SetupStateMachine() 
    {
        if (profileQueue != null && profileQueue.Length > 0)
            SetProfile(initialProfile, transition: false);
    }
    
    // Get the next profile for the state machine when the current profile finishes
    public override StateProfile GetNextProfile(StateProfile lastProfile, ConditionSnapshot conditions) 
    {
        if (profileQueue == null || profileQueue.Length == 0)
            return lastProfile;
        
        queueIndex++;
        
        if (queueIndex >= profileQueue.Length)
            queueIndex = 0;
        
        return profileQueue[queueIndex];
    }
}
```
{% endstep %}

{% step %}
### Create the Editor

After creating the runtime module, you need to create a simple editor to let this communicate with the COZY UI. Create a new C# file and place it in an Editor folder in your project.

```csharp
// Editor for State Machine Module

using UnityEngine;
using UnityEditor;
using UnityEngine.UIElements;
using UnityEditor.UIElements;

[CustomEditor(typeof(MyStateMachineModule))]
public class MyStateMachineModuleEditor : CozyBiomeModuleEditor
{
    VisualElement root;
    MyStateMachineModule module;

    void OnEnable()
    {
        if (target)
            module = (MyStateMachineModule)target;

    }
        
    public override VisualElement DisplayUI()
    {
        root = new VisualElement();
        root.AddToClassList("section-bg");
        
        PropertyField profileQueue = new();
        profileQueue.BindProperty(serializedObject.FindProperty("profileQueue"));
        root.Add(profileQueue);

        return root;
    }
    
    public override VisualElement DisplayBiomeUI()
    {
        root = new VisualElement();
        root.AddToClassList("section-bg");
        
        PropertyField profileQueue = new();
        profileQueue.BindProperty(serializedObject.FindProperty("profileQueue"));
        root.Add(profileQueue);

        return root;
    }
}
```

This is a bare-bones editor but can be extended to include more UI as needed for your project.
{% endstep %}
{% endstepper %}

## API

### Properties

<table><thead><tr><th width="191">Name</th><th width="199">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="6HBSlly2tiSA" label="void" color="blue"></option><option value="SI6HWEVdth26" label="Dictionary<T, float>" color="blue"></option><option value="eWEOwkTAr20E" label="Dictionary<T, ProfileWeight>" color="blue"></option><option value="P5T1CEHEvuKg" label="MeridiemTimeDelta" color="blue"></option><option value="QRYqds3bTqov" label="float" color="blue"></option><option value="5dbig6BtMwZl" label="Action<T, T>" color="blue"></option><option value="zHtuiTxaQ94H" label="T" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ProfileWeights</td><td><span data-option="SI6HWEVdth26">Dictionary&#x3C;T, float></span></td><td>Holds the resolved final weights of the profiles in the state machine</td></tr><tr><td>LocalProfileWeights</td><td><span data-option="eWEOwkTAr20E">Dictionary&#x3C;T, ProfileWeight></span></td><td>Holds the local profile weights of this module based on the current system or biome</td></tr><tr><td>TimeTillProfileChange</td><td><span data-option="P5T1CEHEvuKg">MeridiemTimeDelta</span></td><td>Get the time (in in-game hours and minutes) till the next profile starts changing</td></tr><tr><td>TransitionTime</td><td><span data-option="QRYqds3bTqov">float</span></td><td>Determine the amount of time (is real-world seconds) it takes to change the active profile</td></tr><tr><td>OnProfileChange</td><td><span data-option="5dbig6BtMwZl">Action&#x3C;T, T></span></td><td>Runs when the current profile changes. Takes in the old profile and new profile as arguments</td></tr><tr><td>CurrentProfile</td><td><span data-option="zHtuiTxaQ94H">T</span></td><td>Get the current resolved profile</td></tr><tr><td>CurrentLocalProfile</td><td><span data-option="zHtuiTxaQ94H">T</span></td><td>Get the current profile for this system</td></tr><tr><td>TimerSpeedMultiplier</td><td><span data-option="QRYqds3bTqov">float</span></td><td>Change the rate at which time moves for the state machine. For example, if it will normally take 2 in game hours before a profile changes, a multiplier of 2 will make it take 1 hour to complete.</td></tr></tbody></table>

### Abstract Methods

<table><thead><tr><th width="229.66668701171875">Name</th><th width="102.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="6HBSlly2tiSA" label="void" color="blue"></option><option value="NIZngfiIWOeZ" label="T" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>UpdateStateMachineTimer</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Should the state machine update the timer? If not, you need to handle changing profiles manually.</td></tr><tr><td>SetupStateMachine</td><td><span data-option="6HBSlly2tiSA">void</span></td><td>Runs when the state machine is setup. Override this method to implement initial behavior</td></tr><tr><td>GetNextProfile</td><td><span data-option="NIZngfiIWOeZ">T</span></td><td>Gets the next profile after the previous profile finishes</td></tr></tbody></table>

### Methods

<table><thead><tr><th width="148.33331298828125">Name</th><th width="102.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="6HBSlly2tiSA" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ChangeProfile</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Tries to change the profile to the next profile. Returns true if the operation succeeds</td></tr><tr><td>SetProfile</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Sets the current profile immediately. Duration is calculated based on the min and max time for the profile. Returns true if the operation succeeds</td></tr></tbody></table>

### Inherited

#### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added.</p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

#### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
