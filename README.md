# Alex's Boating App 🚣

A real-time Potomac River conditions tracker built for boaters launching near **38.9038°N, 77.0815°W (Washington, DC)**. Displays live weather, tides, water quality, E. coli monitoring, and NWS alerts in a single mobile-friendly web page — no app store, no install, no account required.

**Live app:** [alexs-boating-app.github.io] https://github.com/alexanderplionis-ctrl

---

## Features

- **NWS Active Weather Alerts** — real-time warnings and advisories from the National Weather Service
- **Current Conditions** — air temperature, wind speed and direction, cloud cover, UV index, and precipitation
- **Water Parameters** — water temperature (°F/°C), gage height, discharge rate, and turbidity from USGS sensors
- **Tide Predictions** — next 6 high/low tides from the nearest NOAA station
- **E. Coli Monitoring** — live sampling data from Fletcher's Cove (Site PMS01, DOEE), including the most recent reading, Safe/Caution/Unsafe status, and recent sample history
- **12-Hour Forecast** — scrollable hourly cards with temperature, precipitation probability, and wind
- **Storm & Precipitation Risk** — 3-day precipitation probability and weather outlook
- **Safety Banner** — automatically triggers at the top of the page for dangerous wind, thunderstorms, elevated gage height, or unsafe E. coli levels
- **Status Indicators** — live green/red dots in the header for each data source (Weather, Tides, USGS, NWS, E. Coli)

---

## Data Sources

| Data | Source | Update Frequency |
|------|--------|-----------------|
| Weather & Forecast | [Open-Meteo](https://open-meteo.com) | Hourly |
| Tide Predictions | [NOAA CO-OPS Station 8594900](https://tidesandcurrents.noaa.gov/stationhome.html?id=8594900) | On demand |
| Water Parameters | [USGS NWIS Site 01651800](https://waterdata.usgs.gov/monitoring-location/01651800/) | ~15 min |
| Weather Alerts | [NWS API](https://api.weather.gov) | Real-time |
| E. Coli | [DC Open Data — Potomac Interceptor Spill Sampling (PMS01)](https://opendata.dc.gov/datasets/potomac-interceptor-e-coli-sample-results) | Daily |

---

## Technology

Built entirely in a single self-contained HTML file using:

- **HTML** — page structure and content
- **CSS** — light blue nautical theme optimized for bright outdoor conditions, with Bebas Neue and Space Mono fonts
- **JavaScript** — fetches all five APIs in parallel, parses responses, calculates safety thresholds, and dynamically renders the UI

**657 lines of code. Zero dependencies. No build step. No backend. No framework.**

---

## How It Works

When the page loads (or when you tap Refresh), the app simultaneously fetches data from all five APIs. Each section renders independently as its data arrives. If any source fails, that section shows an error message while the rest of the app continues to function normally.

The safety banner at the top of the page auto-triggers when any of the following conditions are detected:
- Wind speed above 20 mph
- Active thunderstorm (NWS weather code ≥ 95)
- USGS gage height above 8 ft
- E. coli at Caution or Unsafe levels at Fletcher's Cove

---

## Usage

Open the live URL in any modern browser — desktop or mobile. No login, no API keys, and no installation required. All data APIs are free and publicly accessible.

**To add to your iPhone home screen:**
1. Open the URL in Safari
2. Tap the Share button → **Add to Home Screen**
3. The app will appear as a full-screen icon on your home screen

---

## Local Development

Since this is a single HTML file, there is no build process. To run locally:

1. Clone the repository
2. Open `index.html` in any browser
3. All API calls are made directly from the browser — no local server needed

```bash
git clone https://github.com/YOUR-USERNAME/alexs-boating-app.git
cd alexs-boating-app
open index.html   # macOS
start index.html  # Windows
```

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

*Data is provided for informational purposes only. Always exercise good judgment on the water and check official sources before boating.*
