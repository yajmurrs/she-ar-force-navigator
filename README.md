# She'ar Force Navigator

**Where on the Moon can you see both the Sun and Earth?**

She'ar Force Navigator is a scroll-driven, single-page web experience about the lunar south pole. It was built by an independent student team for the **NASA Space Apps Challenge 2026** in the [Lunar Landing Site Navigator](https://www.spaceappschallenge.org/2026/challenges/lunar-landing-site-navigator/) challenge.

For three sample sites near the Artemis III candidate regions, it shows, hour by hour from **14 Nov to 14 Dec 2026 (UTC, 721 hourly samples)**, whether the Sun, Earth, or both stand above the local terrain skyline.

> ⚠️ Research prototype. It is **not** a certified landing-site, power, or communications assessment, and it is **not** a NASA product.

## Run it

It needs no build step, no server, and no dependencies.

- **Locally:** download or clone the repository and open `index.html` in a modern browser.
- **GitHub Pages:** go to *Settings → Pages*, then choose *Deploy from a branch*, `main`, `/ (root)`. The site will be served at `https://<user>.github.io/<repo>/`.

The only external request is for Google Fonts. Without it, the page falls back to system fonts.

## What's on the page

| Chapter | Content |
|---|---|
| Cold open | Title and question |
| 01 · Descent | Canvas animation descending onto the south pole, with the three sample sites marked (positions are schematic) |
| 02 · The view | First-person 360° horizon. The real Sun and Earth tracks move behind a skyline built from the data. Includes a timeline, play/pause and a site switcher |
| 03 · Verdict | The share of the 30 days in which each body was above the skyline at each site |
| 04 · Coordinate explorer | Enter a latitude/longitude. Inside the ~2 × 2 km footprint of a sample, it gives a hypothetical estimate from that sample's data. Anywhere else, it says sufficient data is not available |
| Mission notes | Method, limitations, sources and AI-use disclosure |

A built-in integrity check, shown in the top bar, recomputes the visible-hour counts from the raw hourly flags and compares them with the stored summary values.

## Results (share of 721 hours with the body's center above the skyline)

| Site | Location | Sampling | Sun | Earth | Both |
|---|---|---|---|---|---|
| MM-01 · Mons Mouton | 85.4° S, 31.7° E | bilinear | 53.81 % | 95.70 % | 53.81 % |
| | | nearest | 55.06 % | 100 % | 55.06 % |
| MMP-02 · Mons Mouton Plateau | 84.3° S, 30.6° E | bilinear | 26.77 % | 60.47 % | 26.77 % |
| | | nearest | 19.56 % | 47.43 % | 19.28 % |
| NR-03 · Nobile Rim 1 vicinity | 85.4° S, 37.3° E | bilinear | 29.96 % | 0 % | 0 % |
| | | nearest | 25.52 % | 0 % | 0 % |

The difference between bilinear and nearest-pixel terrain sampling shows how sensitive these numbers are. Treat every percentage as approximate. The NR-03 Earth result (0 of 721 hours) needs independent verification.

## Method

- **Sun and Earth directions:** NASA/JPL Horizons, sampled hourly from 14 Nov to 14 Dec 2026 (UTC).
- **Terrain skyline:** LOLA south-polar digital elevation model, at 20 m resolution in the near field and 80 m in the far field. The first 40 m around the observer are excluded.
- **Visibility rule:** a body counts as visible when the center of its disc is above the skyline. Disc size, eclipses and link budgets are not modeled.
- **Display:** the on-screen skyline is rebuilt from the samples along the Sun and Earth tracks, with interpolation between them. Elevation is exaggerated and the foreground ridges are illustrative only.

## Repository layout

```
index.html                    The complete site: HTML, CSS, JS and embedded data, in one file
data/shear_force_data.json    The same dataset, extracted from index.html for reuse
data/README.md                Field descriptions for the dataset
LICENSE                       MIT license (code)
```

`index.html` is the source of truth. The JSON file is an exact copy of the `const D = {...}` object embedded in the page, and the page also exposes it at runtime as `window.SHEAR_DATA`.

## Data sources

- [JPL Horizons API](https://ssd-api.jpl.nasa.gov/doc/horizons.html)
- [NASA PGDA: LOLA south-polar topography](https://pgda.gsfc.nasa.gov/products/78)
- [LOLA archive (PDS Geosciences Node)](https://imbrium.mit.edu/)
- [NASA Moon Trek](https://trek.nasa.gov/moon/)

NASA and USGS are data sources only and do not endorse this project.

## Use of artificial intelligence

- The website was designed and coded with Claude (Anthropic), using the team's data.
- The earlier prototype and the data-processing code were written with ChatGPT (OpenAI).
- The site contains no AI-generated images or video. Every frame is drawn live from the data.
- The team is responsible for checking the data and the claims.

## License

Code: [MIT](LICENSE). The underlying NASA data products are subject to their own terms, which are generally public domain for NASA-produced data.

---

*SHE'AR FORCE · independent student team · NASA Space Apps Challenge 2026*
