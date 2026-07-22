---
icon: floppy-disk
tags:
  - api
---

# ISaveable

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Interfaces/ISaveableModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

Allows a module to save and load data when needed.

## Saving and Loading Data

COZY 4 saves module data in a `List<SavedData>` format that is then converted to a JSON string for easy saving and loading. You can either use the default command to save the string to the [PlayerPrefs](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/PlayerPrefs.html) or grab the string yourself to save in a third party system.

Any module that implements ISaveable will automatically save and load data along with the other modules. Any CozySystem (COZY instance or biomes) can also save and load data.

```csharp
// Save data to PlayerPrefs
// Leave slot empty to automatically save to slot 0
CozyWeather.Instance.Save();
// There can be any number of save slots. Save slots are stored in the PlayerPrefs
// using this key: CZY_Save_{slot}
// Save to slot 1
CozyWeather.Instance.Save(1);

//Load data form PlayerPrefs
// Leave slot empty to automatically load from slot 0
CozyWeather.Instance.Load();
// Load from slot 1
CozyWeather.Instance.Load(1);

// Gets a save string to be saved in a third party save system
string saveString = CozyWeather.Instance.GetSaveString();

// Loads from a custom save string
CozyWeather.Instance.LoadFromString(saveString);
```

## Save/Load for Custom Modules

Implementing this interface is easy! All you have to do is use the save and load methods to convert the data that needs to be saved to JSON strings. Here is an implementation example from the Time Module:

```csharp
public SavedData Save()
{
    // Save each piece of data as a JSON string in a string array
    List<string> saveString = new()
    {
        JsonUtility.ToJson(CurrentTime),
        JsonUtility.ToJson(CurrentDate),
        JsonUtility.ToJson(RuntimeEvents)
    };
    
    // Then return a new SavedData with the type name and the string array
    return new SavedData(GetType().Name, saveString);
}

public void Load(SavedData saveString)
{
    // Load data in the same order that it was saved
    CurrentTime = JsonUtility.FromJson<MeridiemTime>(saveString.properties[0]);
    CurrentDate = JsonUtility.FromJson<MeridiemDate>(saveString.properties[1]);
    RuntimeEvents = JsonUtility.FromJson<List<RuntimeEvent>>(saveString.properties[2]);
}
```

## Methods

<table><thead><tr><th width="88.99993896484375">Name</th><th width="102.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="6HBSlly2tiSA" label="void" color="blue"></option><option value="yEGsMYs0bBBS" label="SavedData" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Save</td><td><span data-option="yEGsMYs0bBBS">SavedData</span></td><td>Saves the data of this module into a custom SavedData struct</td></tr><tr><td>Load</td><td><span data-option="6HBSlly2tiSA">void</span></td><td>Loads the current state of the module based on a SavedData struct</td></tr></tbody></table>

***

## Inherited

### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added. </p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
