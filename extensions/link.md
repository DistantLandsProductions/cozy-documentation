---
tags:
  - extension
  - module
  - networking
  - api
---

# Link

Link is the COZY multiplayer sync extension. It lets a networked game share time, weather, and ambience state across peers while keeping the state authoritative on the host or designated authority.

This is useful for competitive or cooperative projects where every connected client should see the same sky conditions and the same in-game date/time. Link does not reimplement full gameplay replication; instead, it synchronizes the COZY state that drives visuals and world ambience.

## What it does

Link broadcasts a compact `CozyLinkState` packet that contains:

- time of day and calendar date
- weather profile name
- ambience profile name
- version metadata

The module can synchronize:

- time and calendar values
- active weather profile
- active ambience profile

The authoritative peer sends state updates; receiving peers apply it locally when they are out of sync.

## Typical use cases

### Shared weather in multiplayer

A host chooses a weather profile and every client converges to the same active state without separate manual syncing.

### Synced day/night cycles

The time-of-day and date can be propagated across the network so each client experiences the same atmospheric timeline.

### Networked ambience playback

Link can synchronize ambience profile selection in addition to weather states, which keeps the audio/visual scene aligned.

## Core API

### `LinkModule`

```csharp
public class LinkModule : CozyModule
```

Key public members:

- `MonoBehaviour TransportComponent`
- `bool linkTime`
- `bool linkWeather`
- `bool linkAmbience`
- `float updateDelay`
- `float timeSettingSensitivity`

The module resolves a transport component, connects it, and broadcasts the current COZY state on a timer.

### `ICozyLinkTransport`

```csharp
public interface ICozyLinkTransport
{
    bool IsAuthority { get; }
    bool IsConnected { get; }
    void Send(CozyLinkState state);
    event Action<CozyLinkState> StateReceived;
}
```

This interface is implemented by networking adapters. The module remains transport-neutral and can work with any custom implementation that satisfies the interface.

### `CozyLinkState`

```csharp
public struct CozyLinkState
{
    public const int CurrentVersion = 1;

    public int Version;
    public bool HasTime;
    public float TimeOfDay;
    public int Year;
    public int Month;
    public int Day;
    public bool HasWeather;
    public string WeatherProfileName;
    public bool HasAmbience;
    public string AmbienceProfileName;
}
```

This is the network-neutral DTO used to package values for transport adapters.

### Transport adapters

Link includes optional adapters for common networking SDKs, including:

- FishNet
- Mirror
- Netcode for GameObjects
- Photon PUN
- PurrNet

Each adapter works through the same `ICozyLinkTransport` contract, so switching network providers is typically a matter of selecting the matching integration and enabling the required define symbol.

### Utility types

```csharp
public static class CozyLinkTransportUtility
public sealed class CozyLinkStateReceiver
```

These helpers serialize, deserialize, and validate state payloads before the value is applied locally.

## Example usage

```csharp
var link = weather.GetModule<LinkModule>();
if (link != null)
{
    link.linkTime = true;
    link.linkWeather = true;
    link.linkAmbience = true;
    link.updateDelay = 0.5f;
}
```

A custom adapter can be used by assigning a `MonoBehaviour` to `TransportComponent` that implements `ICozyLinkTransport`.

## Notes

- Profile names are resolved against each peer's local profile assets, so both sides need matching asset names.
- Link synchronizes the active profile selection, not the underlying blended weights.
- The current implementation is designed for lightweight state replication rather than full world simulation synchronization.
