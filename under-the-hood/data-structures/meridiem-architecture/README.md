---
icon: hourglass-half
---

# Meridiem Architecture

The Meridiem system is COZY’s structured time and calendar framework. It is used to represent the current time of day, the current date, meaningful portions of the day such as Dawn or Night, and scheduled events that happen at specific times or across date ranges.

Rather than relying on raw numeric values or a generic timestamp, COZY uses dedicated data types to describe:

* the current clock time
* the current calendar date
* a time delta or duration
* a named block of the day
* recurring or one-time events

This makes COZY’s time system easier to reason about, easier to serialize, and more reliable for gameplay systems that depend on the day/night cycle, event timing, or save/load behavior.



## Why The Meridiem System

The Meridiem system exists because COZY needs a robust, expressive model for time that goes beyond a simple float value. A plain float can represent the percentage of the day, but it does not clearly express:

* whether a value is a clock time or a duration
* whether a value is a date, a time, or an event window
* how a time should wrap around midnight
* how different systems should react to hour changes, day changes, and scheduled events

By using the Meridiem system, COZY can cleanly separate:

* time-of-day logic
* calendar/date logic
* block-of-day logic
* event scheduling logic

This separation is important because a weather system, a calendar system, and an event system all need to respond to time in different ways. The Meridiem system gives each part a consistent, shared representation so they can work together without conflicting assumptions.

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h2><i class="fa-clock">:clock:</i></h2></td><td align="center"><h3>Time</h3></td><td align="center">Core time object for COZY</td><td><a href="meridiemtime.md">meridiemtime.md</a></td></tr><tr><td align="center"><h2><i class="fa-calendar">:calendar:</i></h2></td><td align="center"><h3>Date</h3></td><td align="center">Defines a date</td><td><a href="meridiemdate.md">meridiemdate.md</a></td></tr><tr><td align="center"><h2><i class="fa-calendar-check">:calendar-check:</i></h2></td><td align="center"><h3>Event</h3></td><td align="center">Lets you define an event based on the calendar</td><td><a href="meridiemevent.md">meridiemevent.md</a></td></tr><tr><td align="center"><h2><i class="fa-timer">:timer:</i></h2></td><td align="center"><h3>Time Delta</h3></td><td align="center">Defines a duration or change in time</td><td><a href="meridiemtimedelta.md">meridiemtimedelta.md</a></td></tr><tr><td align="center"><h2><i class="fa-sunset">:sunset:</i></h2></td><td align="center"><h3>Block</h3></td><td align="center">Define a block or section of time in a day</td><td><a href="meridiemblock.md">meridiemblock.md</a></td></tr></tbody></table>
