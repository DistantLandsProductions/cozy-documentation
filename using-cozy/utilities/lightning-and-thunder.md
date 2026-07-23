---
icon: bolt-lightning
---

# Lightning & Thunder

Lightning and thunder are managed by the [thunder-fx.md](../profiles/fx-profiles/thunder-fx.md "mention") profiles.

COZY 4 uses a lightning attractor system that allows you to define areas that will be hit by lightning. When no attractors are present, lightning will strike a random spot within a 500m box around the player camera but will not call an event.

## Create an Attractor

Begin by creating a new game object in your scene. This can be any object. Then, add the lightning attractor component to it

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

## Strike Events

### Unity Events

The lightning attractor component comes with a public Unity Event that will be called when this attractor is struck by lightning. Use this to spawn explosion VFX, damage entities, etc.<br>

<figure><img src="../../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

### C\#

```csharp
// This script will register a callback for a lightning strike event
using UnityEngine;
using DistantLands.Cozy;

public class LightningListener : MonoBehaviour {

    public CozyLightningAttractor attractor;
    
    public void OnStrike() {
        // Use this method to do whatever you need to do when lightning strikes this point. 
        // Maybe damage a player or structur?
    }
    
    // Subscribe to event
    void OnEnable() {
        if (attractor == null) attractor = GetComponent<CozyLightningAttractor>();
        
        attractor.onStrikeEvent += OnStrike();
    }

    // Unsubscribe to event
    void OnDisable() {
        attractor.onStrikeEvent -= OnStrike();
    }
}
```
