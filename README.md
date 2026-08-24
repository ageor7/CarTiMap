<<<<<<< HEAD
# CarTiMap (v8.11.37)
### A Zero-Build, High-Performance Spatial-Temporal Storytelling Engine for Qualitative Humanities

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Engine Size](https://img.shields.io/badge/Size-%3C500KB-success)](https://github.com/ageor7/CarTiMap)
[![Preact](https://img.shields.io/badge/Framework-Preact--ESM-orange)](https://preactjs.com/)
[![Leaflet](https://img.shields.io/badge/GIS-Leaflet.js-green)](https://leafletjs.com/)
=======
CarTiMap (v8.x)
A Zero-Build, High-Performance Spatial-Temporal Storytelling Engine for Qualitative Humanities

--Image of: --License: MIT --Image of: --Engine Size --Image of: --Preact --Image of: --Leaflet
🗺️ System Overview

CarTiMap (Cartographic, Carousel-enabled Time Mapper) is a lightweight (<500KB), future-proof, client-side visualization application designed to synchronize complex narrative data with interactive georeferenced maps and chronological timelines. Built entirely without a build step (no Webpack, npm, or Node compilation), CarTiMap executes natively in the browser utilizing Preact, HTM, and Vanilla JavaScript (ESM).
>>>>>>> 0fd59bff4a295449c5d2b57d45003de664071717

The application is engineered to consume dynamic datasets published directly as CSV feeds from Google Sheets, which serves as the "Source of Truth" [REF: ETL-04]. CarTiMap orchestrates these inputs into three responsive, resizable viewport panels (the "Hero Stage"):

<<<<<<< HEAD
## 🗺️ System Overview <a name="overview"></a>

**CarTiMap** (Cartographic, Carousel-enabled Time Mapper) is a lightweight (<500KB), future-proof, client-side visualization application designed to synchronize complex narrative data with interactive georeferenced maps and chronological timelines. Built entirely without a build step (no Webpack, npm, or Node compilation), CarTiMap executes natively in the browser utilizing **Preact**, **HTM**, and **Vanilla JavaScript (ESM)**. 

The application is engineered to consume dynamic datasets published directly as CSV feeds from **Google Sheets**, which serves as the "Source of Truth" `[REF: ETL-04]`. CarTiMap orchestrates these inputs into three responsive, resizable viewport panels (the **"Hero Stage"**):
1. **The Leaflet Map Pane** (35% top-left, resizable): Incorporates dynamic WKT/GeoJSON rendering, MarkerCluster spatial indexing, and custom overlapping coordinate fanning.
2. **The Media Carousel Pane** (35% top-right, resizable): Supports multi-asset carousel swiping, auto-fitting aspect ratios, and clickable attributions.
3. **The Content Panel** (55% middle band, resizable): Renders fluid, HTML-enriched narrative descriptions with auto-minimizing Micro-Scroll headers.
4. **The Navigation Timeline Scrubber** (10% bottom band, resizable): Features multi-lane tag swimlanes, custom zoom locks, and a high-density chronological Z-Stacking engine.
=======
    The Leaflet Map Pane (35% top-left, resizable): Incorporates dynamic WKT/GeoJSON rendering, MarkerCluster spatial indexing, and custom overlapping coordinate fanning.
    The Media Carousel Pane (35% top-right, resizable): Supports multi-asset carousel swiping, auto-fitting aspect ratios, and clickable attributions.
    The Content Panel (55% middle band, resizable): Renders fluid, HTML-enriched narrative descriptions with auto-minimizing Micro-Scroll headers.
    The Navigation Timeline Scrubber (10% bottom band, resizable): Features multi-lane tag swimlanes, custom zoom locks, and a high-density chronological Z-Stacking engine.

🚀 Autonomous Quick Start (No Academic Background Required)

If you are a developer looking to deploy or customize CarTiMap purely as a technical tool, follow this zero-dependency workflow:
1. Deployment & Hosting

Since CarTiMap is a monolithic, single-file browser application, you do not need to configure an application server:

    Simply clone the repository and open index.html locally in any modern browser, or host it on a static server (e.g., GitHub Pages, Netlify, Vercel).
    The engine loads Preact and Leaflet asynchronously from optimized edge CDNs (esm.sh and unpkg.com), bypassing CORS constraints and securing rapid Time-to-Interactive (TTI).
>>>>>>> 0fd59bff4a295449c5d2b57d45003de664071717

2. Analytical URL Parameters

<<<<<<< HEAD
## 🚀 Autonomous Quick Start (No Academic Background Required) <a name="quickstart"></a>

If you are a developer looking to deploy or customize CarTiMap purely as a technical tool, follow this zero-dependency workflow:

### 1. Deployment & Hosting
Since CarTiMap is a monolithic, single-file browser application, you do not need to configure an application server:
* Simply clone the repository and open `index.html` locally in any modern browser, or host it on a static server (e.g., GitHub Pages, Netlify, Vercel).
* The engine loads Preact and Leaflet asynchronously from optimized edge CDNs (`esm.sh` and `unpkg.com`), bypassing CORS constraints and securing rapid Time-to-Interactive (TTI).

### 2. Analytical URL Parameters
You can programmatically control the boot-state and active dataset of the application directly through URL query strings:

| Parameter | Accepted Input | Action |
| :--- | :--- | :--- |
| `?source=` | `String` (e.g., `1K9kZynV...`) | The unique ID of the target Google Sheet containing the dataset. |
| `&gid=` | `Integer` (e.g., `1652171772`) | The specific tab GID of your compiled event ledger (`ExtractsGroupedV`). |
| `&bgid=` | `Integer` | The tab GID of the `LayersT` sheet containing basemaps and overlays. |
| `&slide=` | `Integer` | Bypasses chronological sorting to force-mount a specific slide index. |
| `&mapzoom=` | `Integer` (1 - 22) | Overrides Leaflet auto-zoom calculations to lock a fixed camera depth. |
| `&date=` | `ISO-8601 String` | Conducts a binary search to anchor the map/timeline to the nearest chronological node. |
| `&theme=` | `String` (e.g., `dark`, `classic`)| Dynamically overwrites root CSS custom properties prior to DOM render. |

*Example URL:*
`https://ageor7.github.io/CarTiMap/index.html?source=1K9kZynV-IGUd-yT6GiGsIabfjF-k-sn5qAeEONzNIE&bgid=1652171772&slide=1&mapzoom=11`
=======
You can programmatically control the boot-state and active dataset of the application directly through URL query strings:
Parameter	Accepted Input	Action
?source=	String (e.g., 1K9kZynV...)	The unique ID of the target Google Sheet containing the dataset.
&gid=	Integer (e.g., 1652171772)	The specific tab GID of your compiled event ledger (ExtractsGroupedV).
&bgid=	Integer	The tab GID of the LayersT sheet containing basemaps and overlays.
&slide=	Integer	Bypasses chronological sorting to force-mount a specific slide index.
&mapzoom=	Integer (1 - 22)	Overrides Leaflet auto-zoom calculations to lock a fixed camera depth.
&date=	ISO-8601 String	Conducts a binary search to anchor the map/timeline to the nearest chronological node.
&theme=	String (e.g., dark, classic)	Dynamically overwrites root CSS custom properties prior to DOM render.

Example URL: https://ageor7.github.io/CarTiMap/index.html?source=1K9kZynV-IGUd-yT6GiGsIabfjF-k-sn5qAeEONzNIE&bgid=1652171772&slide=1&mapzoom=11
📊 Database Schema (The Google Sheet Structure)

CarTiMap expects a flat CSV input exported from your Google Sheet. The spreadsheet headers are case-insensitive and map directly to the presentation layers:
Column Header	Data Type	Structural Behavior
Title	HTML / String	The main header of the narrative slide. Supports inline HTML formatting (e.g., <b>, <i>).
Start	Date / Time	Format: DD/MM/YYYY HH:MM:SS.sss or standard ISO 8601-2 EDTF. Required.
End	Date / Time	Format: DD/MM/YYYY HH:MM:SS.sss or EDTF. Optional. Marks duration spans.
Description	HTML / String	The primary narrative payload. Supports links, text blocks, and embedded markup.
Place	String	Semantic locations. Multi-places separated by pipe (`\
Location	Geo-Data	Accepts standard Lat, Lon pairs, valid GeoJSON syntax, or Well-Known Text (WKT).
Priority	String	Setting to VIP forces markers to break out of clusters and render as distinct pins on the map.
Tags	String	Comma or newline-delimited categorizations. Routes events into vertical swimlanes on the timeline.
Media	URI	Media URLs (images, YouTube links, PDFs, iframes). Multiple assets can be split via \n or `\
Media Caption	String	Captions mapped 1:1 to your Media URLs (concatenated and aligned).
Media Credit	String	Attributions and copyrights mapped 1:1 to Media URLs.
SubLabels	String	Custom hover tooltip overrides for multi-point or polyline geometries.
🔗 Bidirectional Academic Traceability Map

For researchers and thesis evaluators, this matrix maps the theoretical, methodological, and historical arguments presented in the Master's Thesis (Subterranean Stratigraphy and the Fog of War: Reconstructing the December 1944 Sabotage of the Hotel Grande Bretagne, Georgiadis 2026) directly to the engineering specs and live code blocks within this repository:
Academic Thesis Target	Methodological Concept	System Architecture Anchor	Code / DB Reference Identifier
Chapter 4.3, Page 35	Action Snippet Decomposition (QCA)	BLUEPRINT.md#meth-01	[REF: METH-01] Triangulation & Reliability
Chapter 4.4, Page 37	Relational Ingestion & Flattening	BLUEPRINT.md#etl-01	[REF: ETL-01] Google Sheets Consolidation
Chapter 4.6, Page 41	Source Reliability scoring	BLUEPRINT.md#etl-10	[REF: METH-01] 12-Tier Reliability Matrix
Chapter 5.1, Page 45	Zero-Frontend-Cleaning Mandate	BLUEPRINT.md#etl-04	[REF: ETL-04] Hard Presentation Boundaries
Chapter 5.3, Page 51	Kinematic GPU Hardware Offloading	BLUEPRINT.md#ui-197	[REF: UI-197] Morphological Header Scaling
Chapter 5.4, Page 51	Well-Known Text Axis Inversion	BLUEPRINT.md#map-01b	[REF: MAP-01b] WKT Coordinate Translation
Chapter 5.4, Page 51	Visual Geometry Eclipsing	BLUEPRINT.md#tl-18	[REF: TL-18] Z-Stacking Density Engine
Chapter 5.5, Page 52	ISO 8601-2 Temporal Uncertainty	BLUEPRINT.md#etl-08	[REF: ETL-08] Native AST Compiler
Chapter 5.5, Page 52	Opacity Attenuation (Aura Filter)	BLUEPRINT.md#map-06	[REF: MAP-06] Temporal Ghosting
Chapter 5.6, Page 53	Constant Time DOM Reconciliation	BLUEPRINT.md#perf-02	[REF: PERF-02] O(1) Pointer-Based Delta Tracker
Chapter 6.5, Page 61	Plausibility Triangulation	BLUEPRINT.md#map-02b	[REF: MAP-02b] Identical Coordinate Stacking
📐 Core Engineering Highlights & Algorithms

CarTiMap's reputation as a top-tier digital humanities platform rests on its computational solutions to the visual and relational bottlenecks of historical GIS:
1. Constant-Time Transition Optimization (The Delta Tracker) [REF: PERF-02]

Standard visualization tools redraw the entire canvas upon slide changes, operating in $O(N)$ linear complexity. To secure smooth, high-velocity scrubbing, the CarTiMap state-machine utilizes a persistent memory pointer (prevActiveIndexRef). During transitions, the engine calculates the delta and updates exactly two DOM elements: it demotes the previously active pin and promotes the new target. The remaining map layers are untouched, keeping performance stable even on lower-end tablets.
2. Z-Stacking Density Engine & "Stacked Pin" [REF: TL-18 / MAP-02b]

When multiple historical actions share mathematically identical coordinates (e.g., multiple diplomatic, political, and subterranean events occurring inside the Hotel Grande Bretagne), standard mapping libraries overlap and eclipse markers.
>>>>>>> 0fd59bff4a295449c5d2b57d45003de664071717

    On the Map: CarTiMap intercepts overlapping points and groups them into a custom "Stacked Pin" featuring a numeric depth badge. Clicking this pin triggers a native spiderfy animation, fanning the markers out on the map.
    On the Timeline: Concurrent timeline events are automatically detected via an $O(1)$ stack registry (stackRegistry). They are fanned out along the Z-axis utilizing precise, incremental CSS calc() offsets (+6px X, +4px Y) combined with high-contrast depth badges, communicating chronological volume without vertical swimlane bloat.

<<<<<<< HEAD
## 📊 Database Schema (The Google Sheet Structure) <a name="schema"></a>

CarTiMap expects a flat CSV input exported from your Google Sheet. The spreadsheet headers are case-insensitive and map directly to the presentation layers:

| Column Header | Data Type | Structural Behavior |
| :--- | :--- | :--- |
| **Title** | `HTML / String` | The main header of the narrative slide. Supports inline HTML formatting (e.g., `<b>`, `<i>`). |
| **Start** | `Date / Time` | Format: `DD/MM/YYYY HH:MM:SS.sss` or standard ISO 8601-2 EDTF. Required. |
| **End** | `Date / Time` | Format: `DD/MM/YYYY HH:MM:SS.sss` or EDTF. Optional. Marks duration spans. |
| **Description** | `HTML / String` | The primary narrative payload. Supports links, text blocks, and embedded markup. |
| **Place** | `String` | Semantic locations. Multi-places separated by pipe (`\|`) will compile. Truncates at first comma on HUD. |
| **Location** | `Geo-Data` | Accepts standard `Lat, Lon` pairs, valid GeoJSON syntax, or Well-Known Text (`WKT`). |
| **Priority** | `String` | Setting to `VIP` forces markers to break out of clusters and render as distinct pins on the map. |
| **Tags** | `String` | Comma or newline-delimited categorizations. Routes events into vertical swimlanes on the timeline. |
| **Media** | `URI` | Media URLs (images, YouTube links, PDFs, iframes). Multiple assets can be split via `\n` or `\|`. |
| **Media Caption**| `String` | Captions mapped 1:1 to your Media URLs (concatenated and aligned). |
| **Media Credit** | `String` | Attributions and copyrights mapped 1:1 to Media URLs. |
| **SubLabels** | `String` | Custom hover tooltip overrides for multi-point or polyline geometries. |
=======
3. 4D Telemetry Hoisting & Temporal Ghosting [REF: TL-19 / MAP-06]

The TimelineScrubber passively calculates and broadcasts its active horizontal viewport boundaries ([visibleLeftMs, visibleRightMs]) back to the global orchestrator. The map layer actively monitors this broadcast; any georeferenced marker that falls outside the active epoch is degraded to 20% opacity. This "Temporal Ghosting" visually isolates the active chronological chapter while preserving historical context at the margins.
4. Zero-Build Native AST Compiler [REF: ETL-08]

Standard browser engines cannot parse extended historical date-time intervals (such as ISO 8601-2 Level 2 Choice Sets [1944-12-25, 1944-12-26] or approximate years 194X). To resolve this without introducing massive, 1MB Nearley.js parser binaries, CarTiMap incorporates a lightweight, recursive-descent Native AST Compiler (compileCartiMapAST). This compiler deconstructs extended strings into primitive, integer-compliant nodes, allowing the lightweight parser to evaluate timeline coordinates safely without runtime string-coercion.
🛠️ Technology Stack & Library Integrations
>>>>>>> 0fd59bff4a295449c5d2b57d45003de664071717

To maintain its strict "Anti-Bloat CDN Mandate" [REF: PROT-13], the engine operates strictly under a <500KB footprint using modern, un-transpiled web standards:

<<<<<<< HEAD
## 🔗 Bidirectional Academic Traceability Map <a name="traceability"></a>

For researchers and thesis evaluators, this matrix maps the theoretical, methodological, and historical arguments presented in the Master's Thesis (*Subterranean Stratigraphy and the Fog of War: Reconstructing the December 1944 Sabotage of the Hotel Grande Bretagne*, Georgiadis 2026) directly to the engineering specs and live code blocks within this repository:

| Academic Thesis Target | Methodological Concept | System Architecture Anchor | Code / DB Reference Identifier |
| :--- | :--- | :--- | :--- |
| **Chapter 4.3, Page 35** | Action Snippet Decomposition (QCA) | [BLUEPRINT.md#meth-01](BLUEPRINT.md#meth-01) | `[REF: METH-01]` Triangulation & Reliability |
| **Chapter 4.4, Page 37** | Relational Ingestion & Flattening | [BLUEPRINT.md#etl-01](BLUEPRINT.md#etl-01) | `[REF: ETL-01]` Google Sheets Consolidation |
| **Chapter 4.6, Page 41** | Source Reliability scoring | [BLUEPRINT.md#etl-10](BLUEPRINT.md#etl-10) | `[REF: METH-01]` 12-Tier Reliability Matrix |
| **Chapter 5.1, Page 45** | Zero-Frontend-Cleaning Mandate | [BLUEPRINT.md#etl-04](BLUEPRINT.md#etl-04) | `[REF: ETL-04]` Hard Presentation Boundaries |
| **Chapter 5.3, Page 51** | Kinematic GPU Hardware Offloading | [BLUEPRINT.md#ui-197](BLUEPRINT.md#ui-197) | `[REF: UI-197]` Morphological Header Scaling |
| **Chapter 5.4, Page 51** | Well-Known Text Axis Inversion | [BLUEPRINT.md#map-01b](BLUEPRINT.md#map-01b) | `[REF: MAP-01b]` WKT Coordinate Translation |
| **Chapter 5.4, Page 51** | Visual Geometry Eclipsing | [BLUEPRINT.md#tl-18](BLUEPRINT.md#tl-18) | `[REF: TL-18]` Z-Stacking Density Engine |
| **Chapter 5.5, Page 52** | ISO 8601-2 Temporal Uncertainty | [BLUEPRINT.md#etl-08](BLUEPRINT.md#etl-08) | `[REF: ETL-08]` Native AST Compiler |
| **Chapter 5.5, Page 52** | Opacity Attenuation (Aura Filter) | [BLUEPRINT.md#map-06](BLUEPRINT.md#map-06) | `[REF: MAP-06]` Temporal Ghosting |
| **Chapter 5.6, Page 53** | Constant Time DOM Reconciliation | [BLUEPRINT.md#perf-02](BLUEPRINT.md#perf-02) | `[REF: PERF-02]` O(1) Pointer-Based Delta Tracker |
| **Chapter 6.5, Page 61** | Plausibility Triangulation | [BLUEPRINT.md#map-02b](BLUEPRINT.md#map-02b) | `[REF: MAP-02b]` Identical Coordinate Stacking |

---

## 📐 Core Engineering Highlights & Algorithms <a name="algorithms"></a>

CarTiMap's reputation as a top-tier digital humanities platform rests on its computational solutions to the visual and relational bottlenecks of historical GIS:

### 1. Constant-Time Transition Optimization (The Delta Tracker) `[REF: PERF-02]`
Standard visualization tools redraw the entire canvas upon slide changes, operating in $O(N)$ linear complexity. To secure smooth, high-velocity scrubbing, the CarTiMap state-machine utilizes a persistent memory pointer (`prevActiveIndexRef`). During transitions, the engine calculates the delta and updates exactly two DOM elements: it demotes the previously active pin and promotes the new target. The remaining map layers are untouched, keeping performance stable even on lower-end tablets.

### 2. Z-Stacking Density Engine & "Stacked Pin" `[REF: TL-18 / MAP-02b]`
When multiple historical actions share mathematically identical coordinates (e.g., multiple diplomatic, political, and subterranean events occurring inside the Hotel Grande Bretagne), standard mapping libraries overlap and eclipse markers.
* **On the Map:** CarTiMap intercepts overlapping points and groups them into a custom "Stacked Pin" featuring a numeric depth badge. Clicking this pin triggers a native `spiderfy` animation, fanning the markers out on the map.
* **On the Timeline:** Concurrent timeline events are automatically detected via an $O(1)$ stack registry (`stackRegistry`). They are fanned out along the Z-axis utilizing precise, incremental CSS `calc()` offsets (+6px X, +4px Y) combined with high-contrast depth badges, communicating chronological volume without vertical swimlane bloat.

### 3. 4D Telemetry Hoisting & Temporal Ghosting `[REF: TL-19 / MAP-06]`
The `TimelineScrubber` passively calculates and broadcasts its active horizontal viewport boundaries (`[visibleLeftMs, visibleRightMs]`) back to the global orchestrator. The map layer actively monitors this broadcast; any georeferenced marker that falls outside the active epoch is degraded to 20% opacity. This "Temporal Ghosting" visually isolates the active chronological chapter while preserving historical context at the margins.

### 4. Zero-Build Native AST Compiler `[REF: ETL-08]`
Standard browser engines cannot parse extended historical date-time intervals (such as ISO 8601-2 Level 2 Choice Sets `[1944-12-25, 1944-12-26]` or approximate years `194X`). To resolve this without introducing massive, 1MB Nearley.js parser binaries, CarTiMap incorporates a lightweight, recursive-descent **Native AST Compiler** (`compileCartiMapAST`). This compiler deconstructs extended strings into primitive, integer-compliant nodes, allowing the lightweight parser to evaluate timeline coordinates safely without runtime string-coercion.

---

## 🛠️ Technology Stack & Library Integrations <a name="techstack"></a>

To maintain its strict "Anti-Bloat CDN Mandate" `[REF: PROT-13]`, the engine operates strictly under a **<500KB footprint** using modern, un-transpiled web standards:

*   **Preact & HTM (via esm.sh):** Serves as the reactive UI layer. HTM enables JSX-like syntax natively in the browser without requiring a Babel compilation step.
*   **Leaflet (v1.9.4):** Orchestrates georeferenced spatial coordinates.
*   **Wicket (v1.3.8):** Natively parses OGC Well-Known Text (WKT) geometries (Point, MultiPoint, LineString, Polygon) into Leaflet vector paths.
*   **PapaParse (v5.4.1):** Drives the high-speed local CSV parsing pipeline.
*   **MarkerCluster:** Manages R-Tree spatial indexing and coordinate decluttering.
*   **MapLibre GL JS & Leaflet Integration:** Dynamically initialized *only* when a Vector Tile basemap (`.mvt` / `.pbf`) is requested, preserving resources on standard raster platforms.

---

## 📝 License & Attribution <a name="license"></a>

This software is released under the **MIT License**.
Designed and developed by **Alexandros Georgiadis** (2026) as part of the Master's of Arts Dissertation in Digital Humanities.

*For detailed architectural specifications, please refer directly to the companion file:* `BLUEPRINT.md`.
=======
    Preact & HTM (via esm.sh): Serves as the reactive UI layer. HTM enables JSX-like syntax natively in the browser without requiring a Babel compilation step.
    Leaflet (v1.9.4): Orchestrates georeferenced spatial coordinates.
    Wicket (v1.3.8): Natively parses OGC Well-Known Text (WKT) geometries (Point, MultiPoint, LineString, Polygon) into Leaflet vector paths.
    PapaParse (v5.4.1): Drives the high-speed local CSV parsing pipeline.
    MarkerCluster: Manages R-Tree spatial indexing and coordinate decluttering.
    MapLibre GL JS & Leaflet Integration: Dynamically initialized only when a Vector Tile basemap (.mvt / .pbf) is requested, preserving resources on standard raster platforms.

📝 License & Attribution

This software is released under the MIT License. Designed and developed by Alexandros Georgiadis (2026) as part of the Master's of Arts Dissertation in Digital Humanities.

For detailed architectural specifications, please refer directly to the companion file: BLUEPRINT.md.CarTiMap (v8.x)
A Zero-Build, High-Performance Spatial-Temporal Storytelling Engine for Qualitative Humanities

--Image of: --License: MIT --Image of: --Engine Size --Image of: --Preact --Image of: --Leaflet
🗺️ System Overview

CarTiMap (Cartographic, Carousel-enabled Time Mapper) is a lightweight (<500KB), future-proof, client-side visualization application designed to synchronize complex narrative data with interactive georeferenced maps and chronological timelines. Built entirely without a build step (no Webpack, npm, or Node compilation), CarTiMap executes natively in the browser utilizing Preact, HTM, and Vanilla JavaScript (ESM).

The application is engineered to consume dynamic datasets published directly as CSV feeds from Google Sheets, which serves as the "Source of Truth" [REF: ETL-04]. CarTiMap orchestrates these inputs into three responsive, resizable viewport panels (the "Hero Stage"):

    The Leaflet Map Pane (35% top-left, resizable): Incorporates dynamic WKT/GeoJSON rendering, MarkerCluster spatial indexing, and custom overlapping coordinate fanning.
    The Media Carousel Pane (35% top-right, resizable): Supports multi-asset carousel swiping, auto-fitting aspect ratios, and clickable attributions.
    The Content Panel (55% middle band, resizable): Renders fluid, HTML-enriched narrative descriptions with auto-minimizing Micro-Scroll headers.
    The Navigation Timeline Scrubber (10% bottom band, resizable): Features multi-lane tag swimlanes, custom zoom locks, and a high-density chronological Z-Stacking engine.

🚀 Autonomous Quick Start (No Academic Background Required)

If you are a developer looking to deploy or customize CarTiMap purely as a technical tool, follow this zero-dependency workflow:
1. Deployment & Hosting

Since CarTiMap is a monolithic, single-file browser application, you do not need to configure an application server:

    Simply clone the repository and open index.html locally in any modern browser, or host it on a static server (e.g., GitHub Pages, Netlify, Vercel).
    The engine loads Preact and Leaflet asynchronously from optimized edge CDNs (esm.sh and unpkg.com), bypassing CORS constraints and securing rapid Time-to-Interactive (TTI).

2. Analytical URL Parameters

You can programmatically control the boot-state and active dataset of the application directly through URL query strings:
Parameter	Accepted Input	Action
?source=	String (e.g., 1K9kZynV...)	The unique ID of the target Google Sheet containing the dataset.
&gid=	Integer (e.g., 1652171772)	The specific tab GID of your compiled event ledger (ExtractsGroupedV).
&bgid=	Integer	The tab GID of the LayersT sheet containing basemaps and overlays.
&slide=	Integer	Bypasses chronological sorting to force-mount a specific slide index.
&mapzoom=	Integer (1 - 22)	Overrides Leaflet auto-zoom calculations to lock a fixed camera depth.
&date=	ISO-8601 String	Conducts a binary search to anchor the map/timeline to the nearest chronological node.
&theme=	String (e.g., dark, classic)	Dynamically overwrites root CSS custom properties prior to DOM render.

Example URL: https://ageor7.github.io/CarTiMap/index.html?source=1K9kZynV-IGUd-yT6GiGsIabfjF-k-sn5qAeEONzNIE&bgid=1652171772&slide=1&mapzoom=11
📊 Database Schema (The Google Sheet Structure)

CarTiMap expects a flat CSV input exported from your Google Sheet. The spreadsheet headers are case-insensitive and map directly to the presentation layers:
Column Header	Data Type	Structural Behavior
Title	HTML / String	The main header of the narrative slide. Supports inline HTML formatting (e.g., <b>, <i>).
Start	Date / Time	Format: DD/MM/YYYY HH:MM:SS.sss or standard ISO 8601-2 EDTF. Required.
End	Date / Time	Format: DD/MM/YYYY HH:MM:SS.sss or EDTF. Optional. Marks duration spans.
Description	HTML / String	The primary narrative payload. Supports links, text blocks, and embedded markup.
Place	String	Semantic locations. Multi-places separated by pipe (`\
Location	Geo-Data	Accepts standard Lat, Lon pairs, valid GeoJSON syntax, or Well-Known Text (WKT).
Priority	String	Setting to VIP forces markers to break out of clusters and render as distinct pins on the map.
Tags	String	Comma or newline-delimited categorizations. Routes events into vertical swimlanes on the timeline.
Media	URI	Media URLs (images, YouTube links, PDFs, iframes). Multiple assets can be split via \n or `\
Media Caption	String	Captions mapped 1:1 to your Media URLs (concatenated and aligned).
Media Credit	String	Attributions and copyrights mapped 1:1 to Media URLs.
SubLabels	String	Custom hover tooltip overrides for multi-point or polyline geometries.
🔗 Bidirectional Academic Traceability Map

For researchers and thesis evaluators, this matrix maps the theoretical, methodological, and historical arguments presented in the Master's Thesis (Subterranean Stratigraphy and the Fog of War: Reconstructing the December 1944 Sabotage of the Hotel Grande Bretagne, Georgiadis 2026) directly to the engineering specs and live code blocks within this repository:
Academic Thesis Target	Methodological Concept	System Architecture Anchor	Code / DB Reference Identifier
Chapter 4.3, Page 35	Action Snippet Decomposition (QCA)	BLUEPRINT.md#meth-01	[REF: METH-01] Triangulation & Reliability
Chapter 4.4, Page 37	Relational Ingestion & Flattening	BLUEPRINT.md#etl-01	[REF: ETL-01] Google Sheets Consolidation
Chapter 4.6, Page 41	Source Reliability scoring	BLUEPRINT.md#etl-10	[REF: METH-01] 12-Tier Reliability Matrix
Chapter 5.1, Page 45	Zero-Frontend-Cleaning Mandate	BLUEPRINT.md#etl-04	[REF: ETL-04] Hard Presentation Boundaries
Chapter 5.3, Page 51	Kinematic GPU Hardware Offloading	BLUEPRINT.md#ui-197	[REF: UI-197] Morphological Header Scaling
Chapter 5.4, Page 51	Well-Known Text Axis Inversion	BLUEPRINT.md#map-01b	[REF: MAP-01b] WKT Coordinate Translation
Chapter 5.4, Page 51	Visual Geometry Eclipsing	BLUEPRINT.md#tl-18	[REF: TL-18] Z-Stacking Density Engine
Chapter 5.5, Page 52	ISO 8601-2 Temporal Uncertainty	BLUEPRINT.md#etl-08	[REF: ETL-08] Native AST Compiler
Chapter 5.5, Page 52	Opacity Attenuation (Aura Filter)	BLUEPRINT.md#map-06	[REF: MAP-06] Temporal Ghosting
Chapter 5.6, Page 53	Constant Time DOM Reconciliation	BLUEPRINT.md#perf-02	[REF: PERF-02] O(1) Pointer-Based Delta Tracker
Chapter 6.5, Page 61	Plausibility Triangulation	BLUEPRINT.md#map-02b	[REF: MAP-02b] Identical Coordinate Stacking
📐 Core Engineering Highlights & Algorithms

CarTiMap's reputation as a top-tier digital humanities platform rests on its computational solutions to the visual and relational bottlenecks of historical GIS:
1. Constant-Time Transition Optimization (The Delta Tracker) [REF: PERF-02]

Standard visualization tools redraw the entire canvas upon slide changes, operating in $O(N)$ linear complexity. To secure smooth, high-velocity scrubbing, the CarTiMap state-machine utilizes a persistent memory pointer (prevActiveIndexRef). During transitions, the engine calculates the delta and updates exactly two DOM elements: it demotes the previously active pin and promotes the new target. The remaining map layers are untouched, keeping performance stable even on lower-end tablets.
2. Z-Stacking Density Engine & "Stacked Pin" [REF: TL-18 / MAP-02b]

When multiple historical actions share mathematically identical coordinates (e.g., multiple diplomatic, political, and subterranean events occurring inside the Hotel Grande Bretagne), standard mapping libraries overlap and eclipse markers.

    On the Map: CarTiMap intercepts overlapping points and groups them into a custom "Stacked Pin" featuring a numeric depth badge. Clicking this pin triggers a native spiderfy animation, fanning the markers out on the map.
    On the Timeline: Concurrent timeline events are automatically detected via an $O(1)$ stack registry (stackRegistry). They are fanned out along the Z-axis utilizing precise, incremental CSS calc() offsets (+6px X, +4px Y) combined with high-contrast depth badges, communicating chronological volume without vertical swimlane bloat.

3. 4D Telemetry Hoisting & Temporal Ghosting [REF: TL-19 / MAP-06]

The TimelineScrubber passively calculates and broadcasts its active horizontal viewport boundaries ([visibleLeftMs, visibleRightMs]) back to the global orchestrator. The map layer actively monitors this broadcast; any georeferenced marker that falls outside the active epoch is degraded to 20% opacity. This "Temporal Ghosting" visually isolates the active chronological chapter while preserving historical context at the margins.
4. Zero-Build Native AST Compiler [REF: ETL-08]

Standard browser engines cannot parse extended historical date-time intervals (such as ISO 8601-2 Level 2 Choice Sets [1944-12-25, 1944-12-26] or approximate years 194X). To resolve this without introducing massive, 1MB Nearley.js parser binaries, CarTiMap incorporates a lightweight, recursive-descent Native AST Compiler (compileCartiMapAST). This compiler deconstructs extended strings into primitive, integer-compliant nodes, allowing the lightweight parser to evaluate timeline coordinates safely without runtime string-coercion.
🛠️ Technology Stack & Library Integrations

To maintain its strict "Anti-Bloat CDN Mandate" [REF: PROT-13], the engine operates strictly under a <500KB footprint using modern, un-transpiled web standards:

    Preact & HTM (via esm.sh): Serves as the reactive UI layer. HTM enables JSX-like syntax natively in the browser without requiring a Babel compilation step.
    Leaflet (v1.9.4): Orchestrates georeferenced spatial coordinates.
    Wicket (v1.3.8): Natively parses OGC Well-Known Text (WKT) geometries (Point, MultiPoint, LineString, Polygon) into Leaflet vector paths.
    PapaParse (v5.4.1): Drives the high-speed local CSV parsing pipeline.
    MarkerCluster: Manages R-Tree spatial indexing and coordinate decluttering.
    MapLibre GL JS & Leaflet Integration: Dynamically initialized only when a Vector Tile basemap (.mvt / .pbf) is requested, preserving resources on standard raster platforms.

📝 License & Attribution

This software is released under the MIT License. Designed and developed by Alexandros Georgiadis (2026) as part of the Master's of Arts Dissertation in Digital Humanities.

For detailed architectural specifications, please refer directly to the companion file: BLUEPRINT.md.
>>>>>>> 0fd59bff4a295449c5d2b57d45003de664071717
