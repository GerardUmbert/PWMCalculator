# PWM Fan Curve Comparator

A single-page, browser-based tool to simulate and visually compare two PWM fan speed curves side by side — no build step, no install, just open it in a browser.

**Live demo:** https://gerardumbert.github.io/PWMCalculator/

## What it does

The tool plots fan speed (RPM) against temperature (°C) for two independent fan profiles ("Old Fan" and "New Fan") on the same chart, so you can see exactly how two fan curves diverge across the operating range.

Each profile is defined by the same set of parameters a BIOS/fan controller typically exposes:

- **Min RPM** / **Max RPM** — the fan's speed floor and ceiling.
- **Start Temp (Fan Start)** — the temperature at which the fan begins ramping up from its start speed.
- **Full Speed Temp** — the temperature at which the fan reaches Max RPM.
- **Start PWM** — the PWM duty cycle (0–255) applied at/below Start Temp, converted to RPM between Min and Max RPM.
- **Fan Off** — below a configurable temperature, the fan is fully stopped (0 RPM) instead of idling at its start speed.
- **Delta Temp (hysteresis)** — a hysteresis band so RPM only updates once temperature has moved a set number of degrees from the last committed value, avoiding chatter from small fluctuations. When combined with Fan Off, it also debounces the off/on transition.

Between Start Temp and Full Speed Temp, RPM ramps linearly from the Start PWM-derived speed to Max RPM.

### Heating vs. cooling curves

When **Fan Off** or **Delta Temp** is enabled for a profile, the tool draws two curves for it: a solid line for the rising-temperature (heating) sweep and a dashed line for the falling-temperature (cooling) sweep. This surfaces the hysteresis behavior — the two sweeps diverge near the thresholds where hysteresis holds the last RPM value.

### Interactive controls

- Each profile has its own panel with sliders for every parameter, so you can tune Old Fan and New Fan independently and watch the chart update live.
- Enabling **Drag handles on chart** shows two draggable points on that profile's curve: the start knee (Start Temp / start RPM) and the full-speed knee (Full Speed Temp). Dragging them updates the underlying sliders directly.
- The shaded band on the chart (45–78°C) marks a reference operating range.
- Each panel shows the computed **Speed at start temp** for quick reference.

## Usage

1. Open [`index.html`](index.html) in any modern browser (or visit the [live demo](https://gerardumbert.github.io/PWMCalculator/)) — everything runs client-side.
2. Adjust the sliders in the **Old Fan** and **New Fan** panels to match the curves you want to compare (e.g. values from a fan's datasheet or your BIOS fan control settings).
3. Optionally enable **Fan Off** and/or **Delta Temp (hysteresis)** per profile to model stop-start and hysteresis behavior.
4. Optionally enable **Drag handles on chart** to adjust a curve's knee points directly by dragging on the chart.
5. Hover the chart to read exact RPM values at a given temperature for each curve.

## Tech stack

- [Vue 3](https://vuejs.org/) for reactive state and UI.
- [Chart.js 4](https://www.chartjs.org/) with the [annotation plugin](https://github.com/chartjs/chartjs-plugin-annotation) for the chart.
- [Tailwind CSS](https://tailwindcss.com/) (CDN build) for layout and styling.

All dependencies are loaded from CDN inside a single HTML file — there is no build process.

## Deployment

The site is deployed automatically to GitHub Pages from `index.html` on every push to `main` via the workflow in [`.github/workflows/pages.yml`](.github/workflows/pages.yml).

## License

See repository for license details.
