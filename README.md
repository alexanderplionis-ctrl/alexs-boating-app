# Alex's Boating App 🚣

A real-time Potomac River conditions tracker built for boaters launching near **38.9038°N, 77.0815°W (Washington, DC)**. Displays live weather, tides, water quality, E. coli monitoring, and NWS alerts in a single mobile-friendly web page — no app store, no install, no account required.

**Live app:** [YOUR-USERNAME.github.io/alexs-boating-app](https://YOUR-USERNAME.github.io/alexs-boating-app) *(replace with your actual URL)*

---

## Features

- **NWS Active Weather Alerts** — real-time warnings and advisories from the National Weather Service
- **Current Conditions** — air temperature, wind speed and direction, cloud cover, UV index, and precipitation
- **Water Parameters** — water temperature (°F/°C), gage height, discharge rate, and turbidity from USGS sensors
- **Tide Predictions** — next 6 high/low tides from the nearest NOAA station
- **E. Coli Monitoring** — live daily readings scraped directly from DC Water's Potomac Interceptor sampling page, showing Fletcher's Boathouse results with full recent history and Safe/Caution/Unsafe status
- **12-Hour Forecast** — scrollable hourly cards with temperature, precipitation probability, and wind
- **Storm & Precipitation Risk** — 3-day precipitation probability and weather outlook
- **Safety Banner** — automatically triggers at the top of the page for dangerous wind, thunderstorms, elevated gage height, or unsafe E. coli levels
- **Status Indicators** — live green/yellow/red dots in the header for each data source (Weather, Tides, USGS, NWS, E. Coli)

---

## Data Sources

| Data | Source | Update Frequency |
|------|--------|-----------------|
| Weather & Forecast | [Open-Meteo](https://open-meteo.com) | Hourly |
| Tide Predictions | [NOAA CO-OPS Station 8594900](https://tidesandcurrents.noaa.gov/stationhome.html?id=8594900) | On demand |
| Water Parameters | [USGS NWIS Site 01651800](https://waterdata.usgs.gov/monitoring-location/01651800/) | ~15 min |
| Weather Alerts | [NWS API](https://api.weather.gov) | Real-time |
| E. Coli | [DC Water — Potomac Interceptor Collapse Page](https://www.dcwater.com/about-dc-water/media/potomac-interceptor-collapse) (Fletcher's Boathouse) | Daily (weekdays) |

### A Note on E. Coli Data

Following the January 2026 Potomac Interceptor collapse, DC Water initiated daily E. coli sampling at ten locations along the Potomac River, including Fletcher's Boathouse — the closest active monitoring site to the boating coordinates used in this app. Because DC Water publishes results in an HTML table rather than a machine-readable API, the app fetches the page via a CORS proxy and parses the table directly in the browser — no API key or account required.

Results are available Monday–Friday; weekend results are posted the following Monday. The app tries three CORS proxies in sequence (corsproxy.io → allorigins.win → codetabs.com) so that if one is temporarily down the others serve as fallbacks.

DC Water has committed to daily sampling through July 5, 2026, transitioning to weekly sampling through September 10, 2026. The E. coli status dot turns **yellow** if the most recent reading is more than 3 days old.

E. coli thresholds used:
- ✅ **Safe:** < 410 MPN/100mL
- ⚠️ **Caution:** 410–1,000 MPN/100mL
- ❌ **Unsafe:** > 1,000 MPN/100mL

---

## Technology

Built entirely in a single self-contained HTML file using:

- **HTML** — page structure and content
- **CSS** — light blue nautical theme optimized for bright outdoor conditions, with Bebas Neue and Space Mono fonts
- **JavaScript** — fetches all five data sources in parallel, parses responses, calculates safety thresholds, and dynamically renders the UI
- **CORS Proxies** — corsproxy.io (primary), allorigins.win, and codetabs.com used in fallback chain to fetch DC Water's public E. coli table from the browser

**831 lines of code. Zero frontend dependencies. No build step. No backend server. No API key required.**

---

## How It Works

When the page loads (or when you tap Refresh), the app simultaneously fetches data from all five sources. Each section renders independently as its data arrives. If any source fails, that section shows an error message while the rest of the app continues to function normally.

The safety banner at the top of the page auto-triggers when any of the following conditions are detected:

- Wind speed above 20 mph
- Active thunderstorm (NWS weather code ≥ 95)
- USGS gage height above 8 ft
- E. coli at Caution (> 410) or Unsafe (> 1,000) levels at Fletcher's Boathouse

---

## Usage

Open the live URL in any modern browser — desktop or mobile. No login, no API keys, and no installation required.

**To add to your iPhone home screen:**
1. Open the URL in Safari
2. Tap the Share button → **Add to Home Screen**
3. The app will appear as a full-screen icon on your home screen

---

## Local Development

Since this is a single HTML file, there is no build process. To run locally, open the file directly in any modern browser — all API calls are made directly from the browser and no local server is needed.

```bash
git clone https://github.com/YOUR-USERNAME/alexs-boating-app.git
cd alexs-boating-app
start index.html   # Windows
open index.html    # macOS
```

---

## Background: The Potomac Interceptor Collapse

On January 19, 2026, a 72-inch sewer line known as the Potomac Interceptor collapsed near Clara Barton Parkway in Montgomery County, Maryland, releasing an estimated 243–300 million gallons of untreated sewage into the Potomac River — one of the largest sewage spills in U.S. history. Emergency repairs were completed March 14, 2026, and DC Water has continued daily water quality monitoring at ten sites, including Fletcher's Boathouse, throughout the summer to confirm bacteria levels have returned to normal. This app was built in part to track that recovery.

More information: [DC Water Potomac Interceptor Collapse](https://www.dcwater.com/about-dc-water/media/potomac-interceptor-collapse)

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

*Data is provided for informational purposes only. Always exercise good judgment on the water and consult official sources before boating.*
