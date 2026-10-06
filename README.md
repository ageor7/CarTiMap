# CarTiMap — Spatial-Temporal Narrative History Engine

[![Version](https://img.shields.io/badge/CarTiMap-v8.17.1--b591-28a745.svg)](https://github.com/ageor7/CarTiMap)
[![Architecture](https://img.shields.io/badge/Architecture-Zero--Build%20%7C%20Single--File-007acc.svg)](https://github.com/ageor7/CarTiMap)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

> **CarTiMap** (formerly *CarTiMapper*) is a high-performance, single-file spatial-temporal visualization engine inspired by TimeMapper and TimelineJS. Engineered with a **Zero-Build, Monolithic Architecture** (<500KB), CarTiMap runs natively in any browser from local file systems, Android tablets, GitHub Pages, or enterprise servers without Node/Webpack compilation.

---

## ✨ Key Architectural Highlights

- **🗺️ Hero Stage Viewport Synchronization:** Concurrent multi-pane HUD synchronizing interactive cartography (Leaflet Map), multi-format media carousels (Images, Videos, PDFs, YouTube, WebGL iframes), narrative text sliders with hanging indents, and high-density swimlane timelines.
- **⏱️ Equal-Share Swimlane Timeline:** Dynamically partitions timeline height equally among all tag category swimlanes and the Duration Lane. Features asymmetric 75% slope trapezoids, rotating vector pattern hatching (`/ | \`), and z-stacking density offsets.
- **🌐 GIS & WKT Spatial Physics:** Parses Well-Known Text (`WKT`), GeoJSON collections, and raw `[Lat, Lon]` coordinates. Supports CartoDB, Esri, OpenStreetMap, Protomaps MVT vector tiles, Harvard Geospatial WMS, and Allmaps IIIF georeferenced historical rasters.
- **🕒 ISO 8601-2 EDTF AST Compiler:** Native zero-build Abstract Syntax Tree parser (`compileCartiMapAST`) handling choice sets `[]`, inclusive lists `{}`, range expansions `..`, and temporal uncertainty (`~`, `?`).
- **⚡ $O(1)$ Delta Tracker State Engine:** Uses persistent memory pointers (`prevActiveIndexRef`) to target only active marker transitions during navigation, reducing spatial rendering overhead by 99.8%.
- **🛠️ Embedded Vibe-Monitor Diagnostic HUD:** Draggable, resizable telemetry console providing real-time data fetch logging, coordinate parsing validation, and active variable inspection.

---

## 🚀 Quick Start & Deployment

Because CarTiMap utilizes a **Zero-Build Architecture**, no installation, npm packages, or build tools are required.

### 1. Web Deployment
Host `cartimap.v8.html` on any static web server (GitHub Pages, Vercel, Netlify, Apache, Nginx) or open directly in your local browser:

```bash
# Clone repository
git clone https://github.com/ageor7/CarTiMap.git

# Open directly in browser
open cartimap.v8.html
```

### 2. URL Parameters & Dynamic Routing
Control dataset ingestion and engine behavior via URL parameters:

```text
https://your-domain.com/cartimap.v8.html?source=YOUR_GOOGLE_SHEET_ID&gid=0&bgid=BASEMAPS_TAB_ID&slide=1
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `?source=` | String | Google Sheets Base ID (defaults to Master DB if omitted) |
| `&gid=` | Integer | Sheet Tab GID for primary qualitative data (default: `0`) |
| `&bgid=` | Integer | Sheet Tab GID for custom `LayersT` basemaps and overlays |
| `&slide=` | Integer | Initial slide index override (e.g. `?slide=5`) |
| `&date=` | String | ISO date string anchor override (e.g. `?date=1944-12-25`) |
| `&mapzoom=` | Integer | Initial map zoom level override (1 to 20) |
| `&theme=` | String | CSS Custom Property theme override (`dark`, `light`) |

---

## 📊 Database Schema & Upstream ETL

CarTiMap treats Google Sheets as an immutable database backend. Upstream data consolidation is executed via a centralized `LET()` horizontal lookup formula in Google Sheets (`ExtractsGroupedV`), ensuring the frontend presentation layer receives pre-compiled, sanitized JSON/CSV payloads.

### Required Column Headers (Case-Insensitive)

| Column Header | Type | Description |
| :--- | :--- | :--- |
| **Title** | String | Event header and primary grouping key |
| **Start** | Date/String | Start date/time (Serial number, `DD/MM/YYYY HH:mm`, or ISO EDTF) |
| **End** | Date/String | End date/time for duration spans |
| **Start EDTF** | String | ISO 8601-2 Extended Date/Time Format string (e.g. `1944-12-25T07:00~`) |
| **End EDTF** | String | ISO 8601-2 EDTF end duration or choice set string |
| **Description** | HTML/String | Narrative body content supporting standard HTML tags (`<a>`, `<b>`, `<p>`) |
| **Place** | String | Location names; multi-places split via `\|`, `,`, `;`, or `·` |
| **Location** | Geo-Data | Cartesian WKT (`POINT(lon lat)`), GeoJSON, or `Lat, Lon` pairs |
| **Priority** | String | Set to `VIP` to break out of map clusters as a distinct pin |
| **Tags** | String | Category tags for swimlane layout and filtering |
| **Media** | URL | Image, Video, PDF, or iframe links (split via newline or `\|`) |
| **Media Caption** | String | Captions corresponding 1:1 to media links |
| **Media Credit** | String | Attributions corresponding 1:1 to media links |

---

## 🛠️ Project Structure & Module Taxonomy

```text
cartimap.v8.html
├── GlobalStyles (v6.1.0)        ← Structural & kinematic CSS, flexbox grid, animations
├── Imports & Globals            ← ESM dependencies (Preact, HTM, PapaParse, Wicket)
├── ErrorBoundary (v1.0.0)       ← React error boundary wrapper
├── VibeMonitor (v2.5.53)        ← Floating telemetry HUD & diagnostic logging
├── MediaViewer (v3.2.117)       ← Multi-asset media carousel (Image/Video/PDF/iFrame)
├── ContentSlider (v6.2.118)     ← Narrative text slider with micro-scroll ribbon
├── TimelineScrubber (v27.2.165) ← Swimlane timeline, duration ribbons & date ruler
├── MapViewer (v7.2.118)         ← Leaflet GIS map, MarkerCluster & WMS/IIIF layers
├── AppOrchestrator (v3.9.170)   ← Global state manager, resizers & status cockpit
└── ASTCompiler (v2.1.53)        ← Native ECMAScript EDTF AST parser
```

---

## 📄 License & Attribution

- **License:** MIT License — free for academic, personal, and commercial usage.
- **Author:** Alexandros Georgiadis (`ageor7`)
- **Built for:** HGBB Historical Research Project & Digital Humanities Spatial Analysis.
