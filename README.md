# TC Asset Map
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An interactive map dashboard for managing and visualising Town Council assets in Singapore.
Built with Leaflet.js and Tailwind CSS. The dashboard includes KPI cards, a block-level map with status colouring, an asset-type filter, and a legend.

## Background and Motivation

On 29 July 2025, a fire at Block 229 Lorong 8, Toa Payoh exposed a failure of the building’s dry rising main (dry riser). According to official reports, the defect prevented water from being pumped to upper floors and firefighters had to lay hoses up the staircase to the 10th and 11th floors. Subsequent statements indicated the riser had passed an annual test in August 2024 and that a probable underground pipe leak may have caused the failure. This incident highlights the need for reliable asset inventories, maintenance tracking, and rapid visibility of asset health across estates—exactly what this project is designed to support.

Sources:
- Channel NewsAsia, 30 Jul 2025: Toa Payoh blaze: Faulty riser forced firefighters to haul hoses up 10 storeys; SCDF investigating  
  (https://www.channelnewsasia.com/singapore/toa-payoh-fire-faulty-dry-rising-main-scdf-5267751)
- Channel NewsAsia, 31 Jul 2025: Toa Payoh fire: Faulty dry riser could be due to underground pipe leak, says town council  
  (https://www.channelnewsasia.com/singapore/toa-payoh-fire-dry-riser-bishan-town-council-scdf-pipe-leak-5269131)
- The Straits Times, 30 Jul 2025: Water supply issues during Toa Payoh blaze affected firefighting operations; SCDF investigating  
  (https://www.straitstimes.com/singapore/water-supply-issues-during-toa-payoh-blaze-affected-firefighting-operations-scdf-investigating)

## Features
- Interactive map of HDB blocks (one marker per block for performance)
- KPI cards for at-a-glance totals
- Asset-type filtering (e.g., Dry Riser, Fire Hose Reel)
- Colour legend for block health status
- Sidebar with per-block asset breakdown
- Dark, high-tech theme

## Tech Stack
- HTML5 / CSS3 / JavaScript
- Tailwind CSS (CDN)
- Leaflet.js (CDN)
- OpenStreetMap tiles

## Getting Started

1) Clone the repository
```bash
git clone https://github.com/<your-username>/tc-asset-map.git
cd tc-asset-map
```

2) Open the project  
Choose one of the following:
- Direct open: double-click `index.html` to open it in your browser.
- Local web server (recommended):
  ```bash
  python -m http.server 8080
  ```
  Then visit: http://localhost:8080

## Project Structure
```
tc-asset-map/
├── index.html   # Main dashboard (HTML + inline JS, Tailwind via CDN)
└── README.md    # Project documentation
```

## Configuration

Demo data is defined inline in `index.html`:
```js
const blocks = [
  { id: "123A", lat: 1.3101, lng: 103.856, status: "ok",
    summary: { dry: 2, hose: 5, faulty: 0, due: 0 } },
  { id: "456B", lat: 1.3401, lng: 103.825, status: "warning",
    summary: { dry: 1, hose: 5, faulty: 1, due: 1 } },
  { id: "789C", lat: 1.3721, lng: 103.812, status: "faulty",
    summary: { dry: 2, hose: 4, faulty: 2, due: 1 } }
];
```
- `status`: `ok`, `warning`, `faulty` (controls marker colour)
- `summary`: counts per asset type, plus `faulty` and `due`

Marker colours are mapped here:
```js
const statusColors = { ok: 'green', warning: 'orange', faulty: 'red' };
```

To use real data, replace the inline `blocks` array with a `fetch` call to your API while keeping the same field names.

## Map and UI Behaviour
- Map shows one marker per block. Click a marker to load that block’s asset breakdown in the sidebar.
- Use the “Filter by Asset Type” selector to display only blocks that contain the selected asset type.
- Legend explains status colours:
  - Green: all assets OK
  - Orange: some assets due for maintenance
  - Red: faulty assets present

## Deployment

This is a static site and can be hosted on any static host.

GitHub Pages:
1) Push the repository to GitHub.
2) In Repository Settings → Pages, set Source to the `main` branch (root).
3) Open the published URL GitHub provides.

## Roadmap
- Additional asset types and multi-select filtering
- Integration with live asset data API and auth
- Marker clustering for large datasets
- Dark map tiles (e.g., Mapbox Dark, Carto Dark Matter)
- Basic role-based access controls

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
