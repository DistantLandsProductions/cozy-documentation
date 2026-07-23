---
description: Implements ITimeModule, ICalendarModule, and ICalendarEventsModule
icon: clock
tags:
  - module
  - tutorial
  - api
---

# Time Module

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Modules/CozyTimeModule.cs" class="button secondary" data-icon="code">View on GitHub</a>

<figure><img src="../../../.gitbook/assets/image (16).png" alt="" width="563"><figcaption></figcaption></figure>

The Time Module is the core time and calendar system used by COZY. Use this system to control the time of day (in conjunction with the [atmosphere-module](../atmosphere-module/ "mention")), call events based on the time and day and set the date for seasonal effects (such as the [climate-module](../climate-module/ "mention"))

This module makes use of the [meridiem-architecture](../../../under-the-hood/data-structures/meridiem-architecture/ "mention") to set the time and date in an approachable format both on the front end and in code. These can be cast to the more common [DateTime struct](https://learn.microsoft.com/en-us/dotnet/api/system.datetime?view=net-10.0) when needed.

## Usage Examples

<details>

<summary>Set Time Via Script</summary>

You can either set the time directly, or use the `SmoothlySkipTime` method to change the current time over a set duration.

```csharp
//Get the time module (see Module API for more information about best practice)
CozyTimeModule timeModule;

// Sets the current time to 9:00 AM
timeModule.CurrentTime = new MeridiemTime(9, 00, Meridiem.AM);

// Smoothly interpolates the time to 5:00 AM over 5 seconds, moving forward only
timeModule.SmoothlySkipTime(new MeridiemTime(5,00, Meridiem.AM), 5);
```

</details>

<details>

<summary>Pause Time Movement</summary>

```csharp
// pauses the time movement
timeModule.PauseTime = true;
```

</details>

<details>

<summary>Trigger Gameplay or Visual Changes When Time Changes</summary>

```csharp
timeModule.OnNewHour += (oldHour, newHour) =>
{
    Debug.Log($"Hour changed from {oldHour} to {newHour}");
};

timeModule.OnChangeDay += () =>
{
    Debug.Log("A new day has started.");
};
```

</details>

<details>

<summary>Add Events</summary>

There are two types of [Broken link](/broken/pages/wwztKCxbPR6cJVyITtsE "mention") in COZY 4: static events and runtime events. Static events can only be added using the module UI. Simply drag and drop your event into the static events array

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

For runtime events, you will need to add them using C#.

```csharp
// Creates an event that occurs on Jan 1 2026 from 9:00 AM to 10:00 AM
MeridiemDate startDate = new MeridiemDate(1, 1, 2026);
MeridiemTime startTime = new MeridiemTime(9, 00, Meridiem.AM);
MeridiemTime endTime = new MeridiemTime(10, 00, Meridiem.AM);
RuntimeEvent runtimeEvent = new RuntimeEvent(startDate, startTime, endTime, 
            new RepeatNever(), 
            eventName: "My Event", 
            eventDescription: "Custom event created at runtime", 
            eventType: MeridiemEventType.None
);
            
timeModule.AddEvent(runtimeEvent);

// Depending on the event and when the code is called, you may need to also refresh events
timeModule.RefreshTodaysEvents();
```

</details>

## Widgets

<table data-view="cards"><thead><tr><th></th><th><select><option value="OBED6ZmA2lxZ" label="Small" color="blue"></option><option value="FZGc4BhztoCa" label="Medium" color="blue"></option><option value="CC3yrvOgAGU1" label="Large" color="blue"></option></select></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h3>Current Date</h3></td><td><span data-option="OBED6ZmA2lxZ">Small</span></td><td>Displays the current date. Drag to change.</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/20260722-1549-04.1366470.gif">20260722-1549-04.1366470.gif</a></td></tr><tr><td><h3>Current Time</h3></td><td><span data-option="OBED6ZmA2lxZ">Small</span></td><td>Displays the current time and time block. Drag to change.</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/Recording 2026-07-22 105134.gif">Recording 2026-07-22 105134.gif</a></td></tr><tr><td><h3>Today's Events</h3></td><td><span data-option="FZGc4BhztoCa">Medium</span></td><td>Displays a list of events that occur on today's date</td><td data-object-fit="contain"><a href="../../../.gitbook/assets/image (5).png">image (5).png</a></td></tr></tbody></table>

## API

### Properties

<table><thead><tr><th width="179.66668701171875">Name</th><th width="146.33331298828125">Type<select><option value="EKyPUQoLDXZT" label="bool" color="blue"></option><option value="FEKO6mTFyhqJ" label="Type[]" color="blue"></option><option value="cZMjpHGngrUG" label="MeridiemTime" color="blue"></option><option value="Q3K6K6B9yMnp" label="float" color="blue"></option><option value="iuk3Mkmn3uOz" label="MeridiemDate" color="blue"></option><option value="zsfOh0yky6Lj" label="AnimationCurve" color="blue"></option><option value="duFUNk6n6Hz9" label="MeridiemBlockType" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>resetTimeOnStart</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Should this system reset the time when it loads? (Scene change, application load, etc.)</td></tr><tr><td>startTime</td><td><span data-option="cZMjpHGngrUG">MeridiemTime</span></td><td>The time that this system should start at when the scene is loaded.</td></tr><tr><td>modulateTimeSpeed</td><td><span data-option="EKyPUQoLDXZT">bool</span></td><td>Should time speed modulate based on the current time of day?</td></tr><tr><td>timeSpeedMultiplier</td><td><span data-option="zsfOh0yky6Lj">AnimationCurve</span></td><td>Modulates the time speed based on the day percentage.</td></tr><tr><td>CurrentBlock</td><td><span data-option="duFUNk6n6Hz9">MeridiemBlockType</span></td><td>Get the current time block</td></tr></tbody></table>

### Public Methods

<table><thead><tr><th width="191">Name</th><th width="112.33331298828125">Type<select><option value="T38utvnjPxcU" label="ChangeMeridiemBlockEvent" color="blue"></option><option value="swrgKf1IV4Rn" label="void" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>RefreshTodaysEvents</td><td><span data-option="swrgKf1IV4Rn">void</span></td><td>Refresh the events that are happening today.</td></tr><tr><td>SmoothlySkipTime</td><td><span data-option="swrgKf1IV4Rn">void</span></td><td>Smoothly sets the time to a new value. Useful for skipping nights or other durations of time</td></tr></tbody></table>

### Events

<table><thead><tr><th width="174.33331298828125">Name</th><th width="212.33331298828125">Type<select><option value="T38utvnjPxcU" label="ChangeMeridiemBlockEvent" color="blue"></option></select></th><th>Description</th></tr></thead><tbody><tr><td>ChangeBlockEvent</td><td><span data-option="T38utvnjPxcU">ChangeMeridiemBlockEvent</span></td><td>Event that fires when the current time block changes</td></tr></tbody></table>

### Interfaces

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h3><i class="fa-clock">:clock:</i></h3></td><td align="center">ITimeModule</td><td><a href="itimemodule.md">itimemodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-calendar-days">:calendar-days:</i></h3></td><td align="center">ICalendarModule</td><td><a href="icalendarmodule.md">icalendarmodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-calendar-circle-plus">:calendar-circle-plus:</i></h3></td><td align="center">ICalendarEventsModule</td><td><a href="icalendareventsmodule.md">icalendareventsmodule.md</a></td></tr><tr><td align="center"><h3><i class="fa-floppy-disk">:floppy-disk:</i></h3></td><td align="center">ISaveable</td><td><a href="../extra-interfaces/isaveable.md">isaveable.md</a></td></tr><tr><td align="center"><h3><i class="fa-forward-fast">:forward-fast:</i></h3></td><td align="center">ISkippable</td><td><a href="../extra-interfaces/iskippable.md">iskippable.md</a></td></tr></tbody></table>
