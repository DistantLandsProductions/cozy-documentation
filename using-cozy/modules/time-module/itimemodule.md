---
tags:
  - api
---

# ITimeModule

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Interfaces/ITimeModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

Implement to control the time of day on a module

## Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="118.33331298828125">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="cZMjpHGngrUG" label="MeridiemTime" color="blue"></option><option value="Q3K6K6B9yMnp" label="float" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>CurrentTime</td><td><span data-option="cZMjpHGngrUG">MeridiemTime</span></td><td>Access the current time of day.</td></tr><tr><td>ModifiedTime</td><td><span data-option="Q3K6K6B9yMnp">float</span></td><td>Access the perceived time of day based on the sun. One full day is 1.0. This is modified by adding Actions to the OnModifyTime event. Always 0 at midnight, 0.25 at sunrise, 0.50 at noon, and 0.75 at sunset regardless of the modifications made.</td></tr><tr><td>TimeMovementSpeed</td><td><span data-option="Q3K6K6B9yMnp">float</span></td><td>Specifies the amount of in-game minutes that pass in a real-world second.</td></tr><tr><td>DayAndTime</td><td><span data-option="Q3K6K6B9yMnp">float</span></td><td>Returns the index of the current day in the with the time added as a decimal. For example, 6 AM on March 3rd will return 62.25</td></tr><tr><td>PauseTime</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Determines if time is currently paused</td></tr></tbody></table>

## Events

<table><thead><tr><th width="148.33331298828125">Name</th><th width="102.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>OnModifyTime</td><td><span data-option="k402so3SSkqF">ModifyTime</span></td><td>Add time modification methods that will be used when the modified time (sent to the atmosphere) is calculated. Useful for modifying the time of day that certain solar events (such as sunrise and sunset) occur.</td></tr><tr><td>OnNewHour</td><td><span data-option="yC7kqSQfcOk9">NewHour</span></td><td>Event that runs every hour</td></tr><tr><td>OnNewMinute</td><td><span data-option="pmO4CJbOGqkz">NewMinute</span></td><td>Event that runs every minute</td></tr></tbody></table>

***

## Inherited

### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added. </p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
