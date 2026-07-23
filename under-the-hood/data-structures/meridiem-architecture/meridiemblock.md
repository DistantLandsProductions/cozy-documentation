---
icon: sunset
tags:
  - data
  - api
---

# MeridiemBlock

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Time/MeridiemBlock.cs" class="button secondary" data-icon="code">View on GitHub</a>

[meridiemblock.md](meridiemblock.md "mention") is COZY's structured representation of a named segment of the day. It is used to describe broader periods of time such as Dawn, Morning, Day, Afternoon, Evening, Twilight, and Night.

## Overview

A [meridiemblock.md](meridiemblock.md "mention") represents a range or phase of the day defined by a start time and an end time. This makes it useful for systems that need to react to time-of-day categories rather than exact timestamps. Block times are determined in the [preferences.md](../../../using-cozy/preferences.md "mention") window.

COZY uses this model to map the current time to a simpler semantic block, which is then used by systems such as weather, lighting, ambience, and gameplay state transitions.

### Common Usage Examples

#### Create a block from a start and end time

```csharp
MeridiemBlock block = new MeridiemBlock(
    new MeridiemTime(6, 0, Meridiem.AM),
    new MeridiemTime(8, 0, Meridiem.AM));
```

#### Convert a block type to its block definition

```csharp
MeridiemBlock block = MeridiemBlockType.Dawn;
```

#### Read the current semantic block from the time system

```csharp
MeridiemBlockType currentBlock = timeModule.CurrentBlock;
```

## API

### Properties

| Name        | Type           | Description                      |
| ----------- | -------------- | -------------------------------- |
| `startTime` | `MeridiemTime` | The beginning of the time block. |
| `endTime`   | `MeridiemTime` | The end of the time block.       |

### Functions / Methods

| Name               | Type     | Description                                                                                                     |
| ------------------ | -------- | --------------------------------------------------------------------------------------------------------------- |
| `ToString()`       | `string` | Returns the block name as a string representation of the related `MeridiemBlockType`.                           |
| `Equals(object o)` | `bool`   | Compares the current block against another object and returns whether they represent the same block definition. |
| `GetHashCode()`    | `int`    | Returns the hash code for the block.                                                                            |

### Operators

| Name                                                 | Type                | Description                                                                                                       |
| ---------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `operator ==`                                        | `bool`              | Compares two `MeridiemBlock` values for equality.                                                                 |
| `operator !=`                                        | `bool`              | Compares two `MeridiemBlock` values for inequality.                                                               |
| `implicit operator MeridiemBlockType(MeridiemBlock)` | `MeridiemBlockType` | Converts a `MeridiemBlock` into its related block enum value.                                                     |
| `implicit operator MeridiemBlock(MeridiemBlockType)` | `MeridiemBlock`     | Converts a `MeridiemBlockType` into its corresponding `MeridiemBlock` definition from the configured preferences. |

#### `MeridiemBlockType`

The block type enum defines the standard semantic categories used by COZY:

| Name        | Type                | Description                                                  |
| ----------- | ------------------- | ------------------------------------------------------------ |
| `Dawn`      | `MeridiemBlockType` | The early transitionary time before full daylight.           |
| `Morning`   | `MeridiemBlockType` | The period just after dawn and before the middle of the day. |
| `Day`       | `MeridiemBlockType` | The brightest portion of the day.                            |
| `Afternoon` | `MeridiemBlockType` | The period after midday and before the evening transition.   |
| `Evening`   | `MeridiemBlockType` | The transition into sunset and cooler lighting.              |
| `Twilight`  | `MeridiemBlockType` | The low-light period before nightfall.                       |
| `Night`     | `MeridiemBlockType` | The dark period of the day.                                  |
| `None`      | `MeridiemBlockType` | No block is active.                                          |
