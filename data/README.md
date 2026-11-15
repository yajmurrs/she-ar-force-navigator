# Dataset: `shear_force_data.json`

This file is an exact copy of the data object embedded in `../index.html`. A teammate's processing pipeline prepared the hourly records, and the site reads them as supplied.

## Top level

| Key | Meaning |
|---|---|
| `n` | Number of hourly samples (721). Sample `i` is at 2026-11-14 00:00 UTC + `i` hours |
| `sites` | Object keyed by site ID: `MM-01`, `MMP-02`, `NR-03` |
| `methods` | Summary rows, one per site and terrain-sampling method (`nearest`, `bilinear`) |

## `sites[ID]`

| Key | Meaning |
|---|---|
| `name`, `lat`, `lon` | Sample name, latitude (°), east longitude (°) |
| `h20`, `slope`, `slopeMax`, `span` | Local terrain statistics from the processing pipeline, as supplied |
| `sunEl`, `sunAz` | Sun elevation and azimuth (°) per hour, from JPL Horizons |
| `earthEl`, `earthAz` | Earth elevation and azimuth (°) per hour, from JPL Horizons |
| `sunHz`, `earthHz` | Terrain skyline elevation (°) along the Sun and Earth direction per hour, from the LOLA DEM |
| `f.sun`, `f.earth`, `f.both` | Visibility flag strings of length `n`: `"1"` means the body's center is above the skyline in that hour |

## `methods[]`

| Key | Meaning |
|---|---|
| `site`, `region`, `method` | Site ID, region label, terrain sampling (`nearest` or `bilinear`) |
| `n` | Number of hours |
| `sunOpen`, `earthOpen`, `bothOpen` | Visible-hour counts |
| `sun`, `earth`, `both` | The same counts as percentages of `n` |

The flag strings in `sites` match the `bilinear` rows. The site's built-in data check verifies this when the page loads.
