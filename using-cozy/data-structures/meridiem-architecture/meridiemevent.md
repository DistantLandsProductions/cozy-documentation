---
icon: sunset
tags:
  - data
  - api
---

# MeridiemEvent

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Time/IMeridiemEvent.cs" class="button secondary" data-icon="code">View on GitHub</a>

`RuntimeEvent` and `StaticEvent` are the two event object types used by COZY's Meridiem event system. They represent scheduled time-based occurrences that can be evaluated against the current date and time. They both implement IMeridiemEvent

## Overview

Both event types describe a time window or all-day occurrence that may occur on a specific date, across a range of dates, or in a repeating pattern. They are designed to work with the [time-module](../../modules/time-module/ "mention") so that gameplay logic, ambience state, and world progression can respond to scheduled moments in the day.

The main distinction is:

* `RuntimeEvent` is created and managed at runtime through code.
* `StaticEvent` is an authored asset type, usually created as a [ScriptableObject](https://docs.unity3d.com/6000.2/Documentation/Manual/class-ScriptableObject.html) in the editor.

This makes the two types complementary: author content can be stored as reusable assets, while gameplay systems can create dynamic events on the fly.

### Common Usage Examples

#### Create a static event

Create a new static event using the Create Asset Menu in Unity (Assets/Create/Distant Lands/Cozy/Meridiem Event). You can then edit the properties for the event in the inspector

<figure><img src="../../../.gitbook/assets/image (20).png" alt="" width="563"><figcaption></figcaption></figure>

To see this added to your calendar, be sure to [add this as a static event](../../modules/time-module/#add-events) in the [time-module](../../modules/time-module/ "mention")

#### Create a runtime event in code

```csharp
RuntimeEvent myEvent = new RuntimeEvent(
    new MeridiemDate(4, 15, 2026),
    new MeridiemTime(9, 0, Meridiem.AM),
    new MeridiemTime(10, 0, Meridiem.AM),
    new RepeatNever(),
    "Morning Briefing");

timeModule.AddEvent(myEvent);
```

#### Listen for an event

You can use the [meridiem event listener](https://app.gitbook.com/o/8BSPwfZaF6QMPy2VJpaj/s/Ob7r9cp7YUzVvftisWP3/~/edit/~/changes/1/under-the-hood/events#meridiem-event-listener) to listen for events without any extra code. If you **do** want to listen for events in C#, you can use this pattern

```csharp
// Refer to the event you are listening for. This can be a runtime event as well!
public StaticEvent Event => _event;
[SerializeField]
private StaticEvent _event;

// Subscribe to all events
void OnEnable()
{
    _event.OnEventStart += OnStart;
    _event.OnEventRunning += OnUpdate;
    _event.OnEventEnd += OnEnd;
}

// Unsubscribe from all events
void OnDisable()
{
    _event.OnEventStart -= OnStart;
    _event.OnEventRunning -= OnUpdate;
    _event.OnEventEnd -= OnEnd;
}

// Runs when the event starts
void OnStart() {

}

// Runs when the event ends
void OnEnd() {

}

// Runs every frame the event is ongoing
void OnUpdate() {

}
```

#### Read all events for the current day

```csharp
var events = timeModule.EventsToday;
```

#### Refresh the current day's event list

```csharp
timeModule.RefreshTodaysEvents();
```

## API

### Shared Properties

| Name               | Type                       | Description                                                              |
| ------------------ | -------------------------- | ------------------------------------------------------------------------ |
| `StartDate`        | `MeridiemDate`             | The start date of the event.                                             |
| `EndDate`          | `MeridiemDate`             | The end date of the event, or the same date if a date range is not used. |
| `StartTime`        | `MeridiemTime`             | The start time of the event.                                             |
| `EndTime`          | `MeridiemTime`             | The end time of the event.                                               |
| `AllDay`           | `bool`                     | Whether the event spans the entire day.                                  |
| `DateRange`        | `bool`                     | Whether the event uses a date range rather than a single date.           |
| `RepeatStyle`      | `MeridiemEventRepeatStyle` | The repeat behavior used by the event.                                   |
| `Overnight`        | `bool`                     | Whether the event spans midnight and continues into the next day.        |
| `Duration`         | `MeridiemTimeDelta`        | The total duration of the event window.                                  |
| `DurationInDays`   | `int`                      | The total number of days covered by the event duration.                  |
| `EventName`        | `string`                   | The event name.                                                          |
| `EventDescription` | `string`                   | A descriptive text field for the event.                                  |
| `EventType`        | `MeridiemEventType`        | The general category or type of the event.                               |
| `IsEventRunning`   | `bool`                     | Whether the event is currently active/running.                           |
| `OnEventStart`     | `Action`                   | Optional callback executed when the event begins.                        |
| `OnEventRunning`   | `Action`                   | Optional callback executed while the event is active.                    |
| `OnEventEnd`       | `Action`                   | Optional callback executed when the event ends.                          |

### Shared Functions / Methods

| Name                                                                                      | Type   | Description                                                             |
| ----------------------------------------------------------------------------------------- | ------ | ----------------------------------------------------------------------- |
| `DoesEventHappenToday(MeridiemDate date)`                                                 | `bool` | Checks whether the event occurs on the supplied date.                   |
| `DoesEventHappenAllDay(MeridiemDate date)`                                                | `bool` | Checks whether the event is an all-day event on the supplied date.      |
| `GetRelativeStartDate(MeridiemDate date, out int startDateOffset, out int endDateOffset)` | `void` | Determines the relative date offsets for overnight or repeating events. |
| `UpdateEvent(bool isRunning)`                                                             | `void` | Updates the event's running state.                                      |

### RuntimeEvent-Specific Details

`RuntimeEvent` is used when creating event objects dynamically at runtime. It is typically created in code and pushed into the time module's event list.

#### RuntimeEvent Constructors

| Name                                                                                                                                                                                                                                                                 | Type           | Description                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------------ |
| `RuntimeEvent(MeridiemDate date, MeridiemTime startTime, MeridiemTime endTime, MeridiemEventRepeatStyle repeatStyle, string eventName = "New Event", string eventDescription = "", MeridiemEventType eventType = MeridiemEventType.None)`                            | `RuntimeEvent` | Creates a single-date runtime event.       |
| `RuntimeEvent(MeridiemDate startDate, MeridiemDate endDate, MeridiemTime startTime, MeridiemTime endTime, MeridiemEventRepeatStyle repeatStyle, string eventName = "New Event", string eventDescription = "", MeridiemEventType eventType = MeridiemEventType.None)` | `RuntimeEvent` | Creates a runtime event with a date range. |

### Notes

* Use `RuntimeEvent` when you need to generate an event dynamically during gameplay.
* Use `StaticEvent` when you want a serialized, reusable, editor-authored event definition.
* Both types integrate with the time module's event lookup and scheduling system.
