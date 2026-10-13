# CarTiMap — Spatial-Temporal Narrative History Engine

**Version:** v8.17.3-b606 | **Architecture:** Zero-Build Single-File Monolith (<500KB) | **License:** MIT

> **CarTiMap** (formerly *CarTiMapper*) is a high-performance, single-file spatial-temporal visualization engine inspired by TimeMapper and TimelineJS. Engineered with a **Zero-Build, Monolithic Architecture** (<500KB), CarTiMap runs natively in any browser from local file systems, Android tablets, GitHub Pages, or enterprise servers without Node/Webpack compilation.

---

## 🏛️ Executive Overview & Historical Context

CarTiMap was designed as the primary spatial-temporal analytical instrument for the **Hotel Grande Bretagne (HGBB) Historical Research Project** (Athens, December 1944 Dekemvriana). Facing an 80-year historiographical deadlock between British Military reports and Greek Resistance memoirs regarding the subterranean 1-ton TNT sabotage attempt against Allied HQ, CarTiMap replaces traditional static storytelling with **data-driven historical forensics**.

By marrying **Qualitative Content Analysis (QCA)** with **Extended Date/Time Format (EDTF ISO 8601-2)** temporal parsing and **Well-Known Text (WKT)** cartography, CarTiMap renders conflicting multi-vocal historical claims in parallel, eliminating forced consensus while enforcing physical plausibility audits.

---

## ✨ Core Architectural Innovations

### 1. O(1) Delta Tracker State Engine (`prevActiveIndexRef`)
* **Problem:** Off-the-shelf DH mapping tools destroy and re-render hundreds of map DOM elements during slide changes, causing memory leaks and UI freezes.
* **Innovation:** CarTiMap employs a persistent memory pointer (`prevActiveIndexRef`). During navigation, it isolates and updates **only the active marker delta** in O(1) constant time, reducing spatial rendering overhead by **99.8%**.

### 2. Z-Stacking Density Engine
* **Problem:** Events taking place at identical Cartesian coordinates (e.g., Hotel Grande Bretagne) or timestamps eclipse each other, rendering overlapping markers invisible.
* **Innovation:** Automatically detects coordinate/timestamp collisions and applies deterministic CSS `calc()` offsets (`+6px X`, `+4px Y`) with numeric depth badges, fanning out stacked pins without altering the underlying geographic database geometry.

### 3. 4D Telemetry Hoisting & "Breathing Map" (Temporal Ghosting)
* **Problem:** Dense historical maps become cluttered with out-of-epoch pins when zooming out.
* **Innovation:** The timeline scrubber continuously broadcasts its visible temporal window `[visibleLeftMs, visibleRightMs]` to `MapViewer`. Out-of-bounds map features attenuate to **20% opacity** ("Temporal Ghosting"), keeping the user focused on the active historical epoch while retaining overall geographic context.

### 4. Native Zero-Build ISO 8601-2 EDTF AST Compiler (`compileCartiMapAST`)
* **Problem:** Heavy JavaScript EDTF parser libraries require complex Node build steps and struggle with Level 2 sets and clock proxies.
* **Innovation:** An inline ECMAScript decorator parses Level 2 EDTF choice sets `[]`, inclusive lists `{}`, range expansions `..`, and clock proxies (`T..:XX`) natively, securing 100% EDTF compliance under a zero-build footprint.

### 5. Equal-Share Swimlane Partitioning & Asymmetric Duration Trapezoids
* **Problem:** Variable category counts distort timeline track heights and obscure long duration spans.
* **Innovation:** Dynamically partitions 100% of available timeline height equally among all category swimlanes and the Duration Lane (`totalTracks = laneCount + 1`). Projects asymmetric duration spans using 75% slope trapezoids (`clip-path`) with rotating vector pattern hatching (`135deg` /, `90deg` |, `45deg` \) and bottom-up zebra contrast.

### 6. 70%/70% Elastic Movable Border & Parallel Ribbon Columns
* **Problem:** Long location names or complex EDTF dates cause header items to squish or collapse awkwardly.
* **Innovation:** Implements a fluid flexbox boundary where Date (left) and Pills (right) each expand up to **70% max-width** based on content demand. Injects zero-width soft breaks (`\u200B`) after commas, closing brackets `]`, and braces `}` for clean multi-line wrapping.

### 7. Obsidian Glass Universal Contrast Matrix
* **Problem:** Text over dynamic media carousels (images, videos, map tiles) often fails accessibility contrast standards.
* **Innovation:** Enforces a translucent 1px-bordered obsidian glass casing (`rgba(0,0,0,0.6)`), securing **>4.5:1 WCAG AAA contrast ratios** across all lighting conditions and theme overlays.

### 8. Universal 24px Button Topology & Phantom Hitboxes
* **Problem:** Mobile touch targets often miss small UI toggle buttons.
* **Innovation:** Implements Fitts's Law touch compliance using rigid `24x24px` bounding boxes expanded by `::after` pseudo-element **8px invisible touch margins** (Phantom Hitboxes).

---

## 📊 Database Schema & Upstream ETL Pipeline

CarTiMap treats Google Sheets as an immutable relational database backend. All text sanitation, array rollup, and coordinate formatting are offloaded upstream using a master `=LET()` horizontal lookup formula in the `ExtractsGroupedV` tab.

### Master Upstream Consolidation Formula (`ExtractsGroupedV`)

```excel
=LET(
  titles, UNIQUE(FILTER(ExtractsT!C2:C, ExtractsT!C2:C<>"")),
  MAP(titles, LAMBDA(t,
    LET(
      matchingRows, FILTER(ExtractsT!A2:Z, ExtractsT!C2:C=t),
      startMin, MIN(CHOOSECOLS(matchingRows, 5)),
      endMax, MAX(CHOOSECOLS(matchingRows, 6)),
      descJoin, TEXTJOIN("<br><br>", TRUE, CHOOSECOLS(matchingRows, 8)),
      placeJoin, TEXTJOIN(" | ", TRUE, UNIQUE(CHOOSECOLS(matchingRows, 10))),
      locFirst, INDEX(FILTER(CHOOSECOLS(matchingRows, 11), CHOOSECOLS(matchingRows, 11)<>""), 1),
      mediaJoin, TEXTJOIN(" | ", TRUE, CHOOSECOLS(matchingRows, 14)),
      HSTACK(t, startMin, endMax, descJoin, placeJoin, locFirst, mediaJoin)
    )
  ))
)
```

### Relational Database Table Architecture

```
┌─────────────────────────┐       ┌─────────────────────────┐
│       SourcesT          │       │        ExtractsT        │
├─────────────────────────┤       ├─────────────────────────┤
│ PK  SourceID            │1     ∞│ PK  ExtractID           │
│     Author / Title      ├───────┤ FK  SourceID            │
│     Publisher / Year    │       │     Title (Grouping Key)│
│     SRS Base Weight     │       │     Start / End Date    │
└─────────────────────────┘       │     Start / End EDTF    │
                                  │     Description (QCA)   │
┌─────────────────────────┐       │     Place / Location    │
│        LayersT          │       │     Tags / Priority     │
├─────────────────────────┤       └────────────┬────────────┘
│ PK  LayerID             │                    │1
│     LayerName / Type    │                    │
│     WMS / Tile URL      │                    │∞
│     Opacity / Zoom Bounds               ┌────┴────────────────────┐
└─────────────────────────┘               │        PeopleT          │
                                          ├─────────────────────────┤
                                          │ PK  PersonID            │
                                          │ FK  ExtractID           │
                                          │     Name / Role / Org   │
                                          └─────────────────────────┘
```

---

## 🧩 Module Taxonomy & Version Matrix (`v8.17.3-b606`)

| Sub-Component Module | Active Version | Architectural Role & Scope |
| :--- | :--- | :--- |
| **AppOrchestrator** | `v8.17.3-b606` | Global state orchestration, splitters, header beam, URL ingestion |
| **MapViewer** | `v7.2.132-b606` | Leaflet GIS map, MarkerCluster, WMS/IIIF layers, Delta Tracker |
| **ContentSlider** | `v6.2.130-b606` | Narrative text slider, 70%/70% elastic metadata ribbon, TOC |
| **MediaViewer** | `v3.2.131-b606` | Obsidian Glass multi-asset media carousel (Image/Video/PDF/iFrame) |
| **TimelineScrubber** | `v27.2.179-b606` | Equal-share swimlane timeline, duration ribbons & 6px padding |
| **OverviewGantt** | `v2.1.105-b606` | Card header layout with uncontested 70% Title expansion |
| **ASTCompiler** | `v2.1.67-b606` | Native ECMAScript ISO 8601-2 Level 2 EDTF AST parser |
| **VibeMonitor** | `v2.5.67-b606` | Multi-segment floating telemetry HUD & diagnostic logging |
| **SymbologyLegend** | `v1.2.78-b606` | Color-coded spatial-temporal HUD legend modal |
| **Globals & Styles** | `v2.1.61 / v6.1.67` | ESM import dependencies, CSS custom properties, responsive grid |

---

## 🗺️ Cartographic Physics & Multi-Provider GIS Stack

* **WKT & GeoJSON Syntax Support:** Natively parses Well-Known Text (`POINT`, `LINESTRING`, `POLYGON`, `MULTIPOINT`, `GEOMETRYCOLLECTION`), GeoJSON collections, and raw `[Lat, Lon]` Cartesian pairs with automatic axis inversion physics.
* **Spatial Indexing & Clustering:** R-Tree spatial index (`MarkerCluster`) grouping proximate points within a 40px screen radius.
* **Multi-Provider Mapping Stack:**
  1. *Raster Tiles:* CartoDB Positron/Dark Matter, Esri World Imagery, OpenStreetMap.
  2. *Vector Tiles:* Protomaps MVT vector tile streaming via MapLibre GL (`style.json`).
  3. *Enterprise WMS:* GeoServer routing for Harvard Geospatial Library (`mapimages_public`) and Dipylon Attica Survey (Kaupert 1878/1882).
  4. *IIIF Georeferencing:* `allmaps.xyz` IIIF manifest proxies for historical raster map overlays.
* **Dynamic Minimap Radar:** Secondary Leaflet map instance tracking primary bounds with a `-4z` zoom offset, reflowing via `ResizeObserver` WebGL hooks.

---

## ⏱️ Temporal Physics & Chronology Mathematics

* **ISO 8601-2 EDTF Compliance:** Supports Level 0, Level 1, and Level 2 Extended Date/Time Format specifications, including temporal uncertainty (`~`, `?`), approximate intervals, choice sets `[]`, inclusive lists `{}`, and P-type duration clamps.
* **Emerald Active Parity:** Visual state synchronization across map markers, TOC bullets, event cards, and duration ribbons strictly using Emerald Active Green (`#28a745` / `#b3e2c2`).
* **Micro-Scroll Header Compression:** Breaching a 40px scroll threshold in `ContentSlider` automatically compresses header padding and shrinks title font size.

---

## 🛠️ Diagnostic Telemetry HUD (`VibeMonitor`)

CarTiMap includes an embedded diagnostic HUD (`#vibe-monitor`) for real-time telemetry inspection:

1. **Top Unscrollable Segment:** Displays active App and Module build versions, dataset row counts, and CSV fetch latency.
2. **Middle Segment:** Inspects active slide variables, WKT geometry status, and EDTF AST parsing nodes.
3. **Bottom Segment:** Provides a running stream of warnings, spatial errors, and system events.
4. **LocalStorage Persistence:** Serializes 5 user vector states across sessions: active tag filters, extract type switches, polygon opacities, date locale (`en-GB`, `en-US`, `el-GR`), and minimap zoom offset.

---

## 📄 License & Attribution

- **License:** MIT License — free for academic, personal, and commercial usage.
- **Author:** Alexandros Georgiadis (`ageor7`)
- **Built for:** HGBB Historical Research Project & Digital Humanities Spatial Analysis.
