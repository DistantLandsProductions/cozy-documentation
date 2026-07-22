---
tags:
  - api
---

# IAtmosphereModule

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/Interfaces/IAtmosphereModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

Implement for any module that manages atmosphere properties.

## Properties

<table><thead><tr><th width="136.33331298828125">Name</th><th width="168.333251953125">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="ZNAD0ac2Urqp" label="AtmosphereParameters" color="blue"></option><option value="ksE4BNxkLF9Y" label="Vector3" color="blue"></option><option value="0TudOX4NH3gX" label="Light" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Parameters</td><td><span data-option="ZNAD0ac2Urqp">AtmosphereParameters</span></td><td>Holds a list of atmosphere parameters that will be passed out to the shader</td></tr><tr><td>SunDirection</td><td><span data-option="ksE4BNxkLF9Y">Vector3</span></td><td>Grab the current sun direction</td></tr><tr><td>MoonDirection</td><td><span data-option="ksE4BNxkLF9Y">Vector3</span></td><td>Grab the current moon direction</td></tr><tr><td>SunLight</td><td><span data-option="0TudOX4NH3gX">Light</span></td><td>Grab the current sun light</td></tr><tr><td>MoonLight</td><td><span data-option="0TudOX4NH3gX">Light</span></td><td>Grab the current moon light</td></tr><tr><td>StrongestLight</td><td><span data-option="0TudOX4NH3gX">Light</span></td><td>Grab the current strongest light (either the sun or the moon)</td></tr></tbody></table>

## Inherited

### Properties

<table><thead><tr><th width="148.33331298828125">Name</th><th width="83.6666259765625">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>Active</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Set whether the module is active and enabled</td></tr><tr><td>Requirements</td><td><span data-option="FEKO6mTFyhqJ">Type[]</span></td><td><p>List up to 5 required modules on the system in order for this module to be added. </p><p>Use the DependsOn&#x3C;Types> method to get the list of types.</p></td></tr></tbody></table>

### Public Methods

<table data-search="true"><thead><tr><th width="261.6666259765625">Name</th><th width="81">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="3xR5IBfbjYVq" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ResetModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Resets the module to all default settings</td></tr><tr><td>InitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added and when the game starts</td></tr><tr><td>DeinitializeModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is removed and when the game ends</td></tr><tr><td>CheckIfModuleCanBeRemoved</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has dependencies that prevent it from being removed</td></tr><tr><td>CheckIfModuleCanBeAdded</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Checks if this module has any conflicts that prevent it from being added</td></tr><tr><td>SetupModule</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when the module is added to the weather manager but before the initialize module function.</td></tr><tr><td>OnSceneLoaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is loaded</td></tr><tr><td>OnSceneUnloaded</td><td><span data-option="3xR5IBfbjYVq">void</span></td><td>Runs when a scene is unloaded</td></tr></tbody></table>
