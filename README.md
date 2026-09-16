# CarTiMap — Spatial-Temporal Historical Reconstruction Engine

> **Version:** `v8.13.69-b261` (Conformed Production Baseline)  
> **Identity:** CarTiMap (formerly CarTiMapper) — A zero-build, high-performance TimeMapper on steroids  
> **Core Objective:** Forensic spatial-temporal visualization, historical triangulation, and multimodal narrative storytelling  
> **Primary Case Study:** *Forensic Visualisation and Triangulation of Historical Narratives: The 1944 Hotel Grande Bretagne Sabotage Operation* (Alexandros Georgiadis, 2026)

**CarTiMap** is a high-performance, single-file application that seamlessly integrates interactive cartography (Leaflet) with a high-fidelity, data-dense swimlane timeline and a synchronized media carousel. Built entirely without a build step (Webpack/Node), this engine runs natively in the browser using Preact (`htm`), Vanilla JavaScript, and CSS.

It is designed to consume published Google Sheets (CSVs) and dynamically orchestrate a cinematic, data-driven narrative across three responsive panes: Map, Media, and Narrative Content Slider.

---

### ✨ Architectural Highlights & Core Features

#### 🗺 Cinematic Geo-Engine (`MapViewer v6.4.122-b261`)
*   **WKT & GeoJSON Architecture:** Natively parses Well-Known Text (`POINT`, `LINESTRING`, `POLYGON`, `MULTIPOINT`, `MULTILINESTRING`, `MULTIPOLYGON`, `GEOMETRYCOLLECTION`) and valid GeoJSON.
*   **Option A Pure Pin Heads & Floating Shoulder Badges (`[REF: MAP-PIN-01]`):** Pin heads render 100% solid color without text clutter (Active Green `#28a745`, VIP Gold `#ffb300`, Inactive Blue `#007acc`). Overlapping co-located items render a floating dark pill badge (`+1`, `+2`) on the top-right shoulder (`top: -5px, right: -7px`).
*   **Explicit Vector Layer Z-Stack (`[REF: MAP-ZSTACK-01]`):** FeatureGroups mount in strict vertical order: `polygonLayer` (bottom, `bringToBack()`) $\rightarrow$ `polylineLayer` (middle) $\rightarrow$ `clusterLayer` $\rightarrow$ `markerLayer` (pins, `zIndex = 10000`) $\rightarrow$ `chevronLayerRef` (topmost arrows), ensuring lines and pins sit physically above polygons for 100% click-selectability.
*   **State-Based Layer Swapping (`[REF: MAP-02]`):** Active non-VIP markers dynamically promote out of `MarkerClusterGroup` into `markerLayer` with DOM style sanitization (`display: 'block'`, `zIndex = '10000'`), preventing multi-point nodes (`Patra`, `Megara Airfield`, `Piraeus Port`) from being swallowed by cluster bubbles regardless of zoom level.
*   **Context-Aware Sub-Label Delimiter Engine (`[REF: MAP-GEOM-04b]`):** Smart regex `/(?:\s+-\s+|[\r\n]+\s*-?\s*|\||·|;|·)/` splits list dashes and bullet breaks while preserving compound proper nouns (`Nea-Smyrni`, `Port-au-Prince`).
*   **Dynamic Radar Minimap:** Secondary Leaflet projection matrix tracking main map focal depth with user-adjustable zoom offsets (`-2` to `-8`).

#### ⏱ Multi-Lane Swimlane Scrubber (`TimelineScrubber v26.12.44-b260`)
*   **Duration Lane Isolation (`[REF: TL-05b]`):** Swimlane grid lines and sticky labels elevate to `bottom: 38px`, cleanly separating them from the 10px Duration Lane band (`28px` to `38px` from bottom).
*   **Tag Gravity Matrix:** Weighted combinatorial sorting algorithm grouping co-occurring topic swimlanes on the Y-axis.
*   **ISO 8601-2 / EDTF Precision:** Hatched pattern fills for approximate durations, sub-dot indicators for Set/List dates, and drop lines for pinpoint timestamps.

#### 📽 Synchronized Media Carousel & Content Slider (`ContentSlider v5.8.36-b253`, `MediaViewer v2.13.7-b228`)
*   **Omni-Splitter Matrix Ingestion:** Synchronizes parallel media arrays (`Media`, `Media Caption`, `Media Credit`) split by newlines (`CHAR(10)` / `\n`) or pipes (`|`).
*   **Multi-Format Carousel:** Supports high-res photos, YouTube videos with start timestamps (`t=...`), PDF archival documents, and interactive map iframes.
*   **Sticky Header & Master Typographic Envelope:** 85ch Master Envelope flushing Date strings, Tags, and Places cleanly to the margins.

#### 🎛 System Identity & Telemetry (`AppOrchestrator v3.7.154-b261`, `VibeMonitor v2.2.16-b228`)
*   **Vibe-Monitor Developer HUD:** Draggable, resizable diagnostic console tracking real-time data ingestion, row validation, coordinate success rates, and module manifests.
*   **Active-Slide Preserving Filter Intercept:** Master category deselect retains active slide items, displaying toast notifications.

---

### 📦 Conformed Production Module Matrix (`v8.13.69-b261`)

| Module | Version | Core Function & Responsibility |
| :--- | :--- | :--- |
| **AppOrchestrator** | `v3.7.154-b261` | Global state orchestration, URL hash/query routing, filter intercepts, status bar, and viewport layout physics. |
| **MapViewer** | `v6.4.122-b261` | Leaflet GIS stage, WKT parsing, Option A pin heads, vector z-stacking, state-based layer swapping. |
| **ContentSlider** | `v5.8.36-b253` | Hero narrative carousel, HTML/JSX execution, media gallery sync, multi-author bibliography parsing. |
| **MediaViewer** | `v2.13.7-b228` | Modal media stage for high-res maps, YouTube videos, audio tracks, and PDF archival documents. |
| **TimelineScrubber** | `v26.12.44-b260` | Multi-lane swimlane scrubber, EDTF date rendering, duration bands, zoom locking engine. |
| **ASTCompiler** | `v1.2.74-b228` | Native ECMAScript AST decorator (`compileCartiMapAST`) for ISO 8601-2 Level 3 EDTF date parsing. |
| **VibeMonitor** | `v2.2.16-b228` | Real-time telemetry dashboard monitoring DOM health, memory bounds, and spatial-temporal errors. |

---

### 🚀 Usage & Deployment

Because CarTiMap utilizes a **Zero-Build Architecture**, there is nothing to install, compile, or bundle.

#### 1. Deployment Steps
1. Format a Google Sheet with the standard schema (`HGBB Extracts DB`).
2. Publish the sheet to the web as a CSV.
3. Open `cartimap.v8.13.69-b261.html.js` in any browser or deploy to a static host (GitHub Pages, Vercel, Netlify, or local file system).
4. Append your Google Sheet ID to the URL syntax:
   ```text
   https://ageor7.github.io/CarTiMap/?source=YOUR_GOOGLE_SHEET_ID
   ```

#### 2. 📊 Spreadsheet Schema
The engine parses the first row of your CSV as headers (case-insensitive):

| Column Header | Type | Description |
| :--- | :--- | :--- |
| **Title** | String | Main event header rendered on timeline and content slider. |
| **Start** | Date/Time | ISO 8601-2 / EDTF string or `DD/MM/YYYY HH:MM:SS`. Required. |
| **End** | Date/Time | ISO 8601-2 / EDTF string or `DD/MM/YYYY HH:MM:SS`. Optional duration boundary. |
| **Description** | HTML/String | Narrative body text. Supports standard HTML formatting (`<b>`, `<i>`, `<a>`, `<p>`). |
| **Place** | String | Human-readable location names (`Patra; Megara Airfield; Piraeus Port`). |
| **Location** | Geo-Data | Accepts `Lat, Lon`, WKT strings (`POINT`, `LINESTRING`, `POLYGON`, `GEOMETRYCOLLECTION`), or GeoJSON. |
| **Priority** | String | Set to `VIP` to force markers to break out of clusters and render as gold pins. |
| **Tags** | String | Comma or line-break separated tags for categorization and swimlane routing. |
| **Media** | URL | Links to images, YouTube videos, or PDFs. Multiple links split by `CHAR(10)` or `\|`. |
| **Media Caption** | String | Captions corresponding to the media URLs (1:1 index mapped). |
| **Media Credit** | String | Attributions corresponding to the media URLs (1:1 index mapped). |
| **SubLabels** | String | Custom map tooltip overrides for specific multi-geometry layers. |

#### 3. 📈 Multi-Media & Single-Line WKT Conventions
* **CHAR(10) Array Synchronization:** To attach multiple media items to a slide, separate entries in Google Sheets using newlines (`Alt+Enter`). The engine synchronizes `Media`, `Caption`, and `Credit` arrays by their relative index.
* **Single-Line WKT Geometries:** All WKT strings (`LINESTRING`, `POLYGON`, `GEOMETRYCOLLECTION`) must be stored as **single, contiguous lines without internal newlines (`CHAR(10)`)** to prevent fracture during upstream ETL `SPLIT` operations.

---

### 🎛 URL Query & Parameter API

Control the application initialization state by appending query parameters (`?param1=val1&param2=val2`):

| Parameter | Type | Example | Description |
| :--- | :--- | :--- | :--- |
| `source` | String | `?source=1K9kZynV...` | Targets a specific Google Sheet ID. |
| `gid` | Integer | `&gid=0` | Targets a specific tab within the Google Sheet. |
| `bgid` | Integer | `&bgid=1652171772` | Targets a specific `LayersT` tab for basemaps and overlays. |
| `slide` | Integer/String | `&slide=14` | Forces the engine to initialize on a specific slide index or item ID. |
| `date` | Date String | `&date=1944-12-25` | Anchors the camera to the event closest to the requested date. |
| `mapzoom` | Integer | `&mapzoom=12` | Overrides initial Leaflet map zoom level. |
| `categories` | CSV String | `&categories=Storyline` | Active category filters on load. |
| `zoomlock` | Enum | `&zoomlock=auto` | Timeline scrubber zoom lock mode (`off`, `soft`, `auto`, `hard`). |

---

### 📚 Two-Tier Documentation Architecture (`[REF: DOC-01]`)

To eliminate technical debt and prevent architectural drift, the documentation is strictly bifurcated:

*   **`README.md` (This File):** Epistemic portal, project overview, visual features, spreadsheet schemas, URL API, and developer onboarding.
*   **`Blueprint.md` (formerly `BLUEPRINT.md`):** Rigid architectural, physical, mathematical, and spatial specifications indexed via the `[REF: TAG-NAME]` semantic anchor taxonomy interlinked with thesis chapter/section coordinates (*Forensic Visualisation and Triangulation of Historical Narratives*, Georgiadis 2026).
