---
icon: forward-fast
tags:
  - api
---

# ISkippable

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Interfaces/ISaveableModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

Allows a module to change data when time is skipped

## Methods

<table><thead><tr><th width="148.33331298828125">Name</th><th width="102.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="6HBSlly2tiSA" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>SkipTime</td><td><span data-option="6HBSlly2tiSA">void</span></td><td>Skip time by a certain factor</td></tr></tbody></table>

***

## Inherited

### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added. </p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
