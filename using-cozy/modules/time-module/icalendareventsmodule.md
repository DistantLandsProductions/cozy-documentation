---
tags:
  - api
---

# ICalendarEventsModule

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Interfaces/ICalendarEventsModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

Implement on a module to run MeridiemEvents

## Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="150.33331298828125">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="cZMjpHGngrUG" label="MeridiemTime" color="blue"></option><option value="Q3K6K6B9yMnp" label="float" color="blue"></option><option value="iuk3Mkmn3uOz" label="MeridiemDate" color="blue"></option><option value="KnNNqDNX8drJ" label="List<RuntimeEvent>" color="blue"></option><option value="GikIZmZMMFWm" label="List<StaticEvent>" color="blue"></option><option value="Y7PSZPpMzrdD" label="List<tuple?" color="blue"></option><option value="jPl1XRBebWYS" label="List<tuple>" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>RuntimeEvents</td><td><span data-option="KnNNqDNX8drJ">List&#x3C;RuntimeEvent></span></td><td>Collection of events added at runtime to the calendar system</td></tr><tr><td>StaticEvents</td><td><span data-option="GikIZmZMMFWm">List&#x3C;StaticEvent></span></td><td>Collection of static events added in the editor to the calendar system</td></tr><tr><td>EventsToday</td><td><span data-option="jPl1XRBebWYS">List&#x3C;tuple></span></td><td>All events that occur today</td></tr></tbody></table>

## Methods

<table><thead><tr><th width="157">Name</th><th width="142.99993896484375">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="wxGfgTW4OzPO" label="event" color="blue"></option><option value="k402so3SSkqF" label="ModifyTime" color="blue"></option><option value="yC7kqSQfcOk9" label="NewHour" color="blue"></option><option value="pmO4CJbOGqkz" label="NewMinute" color="blue"></option><option value="lAGODHLibcRr" label="ChangeDayEvent" color="blue"></option><option value="mTzzrdLTZn2k" label="ChangeYearEvent" color="blue"></option><option value="g90ms9Dtu4Em" label="void" color="blue"></option><option value="8kg5u6H6rhS9" label="List<IMeridiemEvent>" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>AddEvent</td><td><span data-option="g90ms9Dtu4Em">void</span></td><td>Add a new runtime event to the calendar</td></tr><tr><td>RemoveEvent</td><td><span data-option="g90ms9Dtu4Em">void</span></td><td>Remove an existing runtime event from the calendar</td></tr><tr><td>GetEventsOnDay</td><td><span data-option="8kg5u6H6rhS9">List&#x3C;IMeridiemEvent></span></td><td>Get a list of all events that occur on a specific day</td></tr></tbody></table>

***

## Inherited

### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added. </p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
