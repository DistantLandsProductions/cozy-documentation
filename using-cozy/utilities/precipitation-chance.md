---
icon: cloud-drizzle
---

# Precipitation Chance

Precipitation chance drives the forecasting of rain and snow [weather-profile.md](../profiles/weather-profile.md "mention")s. Rather than have a single precipitation chance value, the chance is broken down into two values: stratiform and convective chance. These are two different rain chance types that break down rain chance into two more usable values. Light rain and heavy rain may _seem_ like the same type of thing, but the way that you get to either of these and what happens after each type of weather is very different.

{% hint style="info" %}
You can also set these values directly if you prefer to! Simply set the `Rain Chance Calculation Mode` in the [climate-module](../modules/climate-module/ "mention") to `manual`&#x20;

<p align="center"><img src="../../.gitbook/assets/image.png" alt="" data-size="original"></p>
{% endhint %}

## Convective Chance

Convective chance controls the fast-paced, violent storms (thunderstorms, blizzards, hail, etc.). They typically come quickly and dissipate even faster but leave behind wakes of destruction under a clear sky. In real life, these storms come in cumulonimbus clouds and are formed when atmospheric conditions are perfect for creating massive, towering rain clouds using updraftts; generally from a rise in temperature and drop in pressure.

{% hint style="info" %}
This is _massively_ oversimplified for the purposes of this system, but if you want to learn more, I highly recommend [_The Cloudspotter's Guide_](https://www.amazon.com/Cloudspotters-Guide-Science-History-Culture/dp/0399533451) by Gavin Pretor-Pinney.
{% endhint %}

Convective chance is calculated using the following equation:

$$
Convective= \left(\left(t+3\right)\cdot0.375\cdot h\right)^{2}\cdot\left(1-p\right)^{2}
$$

Where t, h, and p represent the normalized version of [temperature.md](../../under-the-hood/data-structures/temperature.md "mention"), [humidity.md](../../under-the-hood/data-structures/humidity.md "mention"), and [pressure.md](../../under-the-hood/data-structures/pressure.md "mention") respectively.

## Stratiform Chance

Stratiform rain chance leads to longer, gentler rain and has to do with the relationship of pressure to humidity independently of temperature. To prevent exploding rain chance, convective chance is subtracted from stratiform chance.

Stratiform chance is calculated using the following equation:

$$
Stratiform =(h\cdot(1-p^{2}))-clamp(Convective)
$$

## Working Together

Because convective chance can impact stratiform chance, it can be difficult to visualize how they interact. This graph shows how both of the rain chance values interact with each other as well as impact the overall chance that you will see rain at all (total rain chance). The values for humidity, pressure, and temperature are normalized from 0-1.

{% embed url="https://www.desmos.com/calculator/op5e3qo9fz" %}

View the graph to change values, to see different scenarios: [https://www.desmos.com/calculator/op5e3qo9fz](https://www.desmos.com/calculator/op5e3qo9fz)
