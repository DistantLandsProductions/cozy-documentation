---
icon: tree-palm
---

# Climate

COZY uses custom data types for all climate related properties for better localization, reduced boilerplate code, and easier workflows.

<table data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><h2><i class="fa-temperature-list">:temperature-list:</i></h2></td><td align="center"><h3>Temperature</h3></td><td><a href="temperature.md">temperature.md</a></td></tr><tr><td align="center"><h2><i class="fa-droplet">:droplet:</i></h2></td><td align="center"><h3>Humidity</h3></td><td><a href="humidity.md">humidity.md</a></td></tr><tr><td align="center"><h2><i class="fa-gauge">:gauge:</i></h2></td><td align="center"><h3>Pressure</h3></td><td><a href="pressure.md">pressure.md</a></td></tr><tr><td align="center"><h2><i class="fa-fan">:fan:</i></h2></td><td align="center"><h3>Air Quality</h3></td><td><a href="air-quality.md">air-quality.md</a></td></tr><tr><td align="center"><h2><i class="fa-sun">:sun:</i></h2></td><td align="center"><h3>UV Index</h3></td><td><a href="uv-index.md">uv-index.md</a></td></tr><tr><td align="center"><h2><i class="fa-cloud-drizzle">:cloud-drizzle:</i></h2></td><td align="center"><h3>Precipitation Chance</h3></td><td><a href="precipitation-chance.md">precipitation-chance.md</a></td></tr></tbody></table>

## Climate Range

The `ClimateRanges` struct is responsible for holding daily min and max values for temperature, humidity, pressure, etc.

## Climate Snapshot

The `ClimateSnapshot` struct represents the current climate values at a particular point in the simulation (normally date and time).
