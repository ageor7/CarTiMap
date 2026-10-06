# CAR TIMAP ENGINE MASTER BLUEPRINT
**Version:** v8.17.1 | **Date:** 2026-10-06
**Architecture:** Zero-Build, Single-File ESM Monolithic Engine (<500KB)
**Repository:** ageor7/CarTiMap

---

## 1. ENGINEERING PROTOCOLS & CODING DIRECTIVES

1. **[REF: ARCH-01] Zero-Build Monolithic Footprint:** CarTiMap is distributed as a single HTML file containing inline ES modules (Preact, HTM, PapaParse, Leaflet, Wicket, edtf.js). The entire footprint must remain strictly under **500KB** uncompressed to run natively off local disks, Android tablets, GitHub Pages, or enterprise servers without Node/Webpack build steps.
2. **[REF: DOC-01] Two-Tier Documentation:** Master Blueprint contains the architectural "Why" and "What" (UI/UX, GIS physics, state engines), while inline comments contain component mechanics. Linked via `[REF: TAG-NAME]` semantic anchors.
3. **[REF: DOC-02] Major Block Boundaries:** All codebase updates must preserve indestructible block delimiters:
   ```javascript
   // === [ MAJOR BLOCK: ComponentName vX.X.X ] ===
   ```
4. **[REF: VER-01] Semantic Versioning:** Three-tier versioning format `X.Y.Z-bBUILD`. `X` = Architectural rewrite, `Y` = Feature release, `Z` = Patch vector, `bXXX` = Build iteration.
5. **[REF: QC-01] Pre-Compile Line Audit:** Prior to compiling client-side JavaScript or CSS alterations, a line-by-line audit comparing proposed module states against `/workspace/artifacts/` must be executed to prevent regression of validated features.

---

## 2. DATA SCHEMA & UPSTREAM ETL PIPELINE

1. **[REF: ETL-01] Single Source of Truth:** Google Sheets CSV export (`ExtractsGroupedV` tab) functions as the immutable database backend.
2. **[REF: ETL-04] Zero Frontend Sanitation:** The presentation layer is strictly a renderer. Data cleaning, sanitization, and array rollup are executed upstream in Google Sheets via `LET()` horizontal consolidation formulas.
3. **[REF: ETL-08] Native AST Compiler (`compileCartiMapAST`):** A zero-build ECMAScript decorator deconstructs complex ISO 8601-2 EDTF choice sets `[]`, inclusive lists `{}`, and duration ranges `..` into primitive nodes for the core parser, securing 100% Level 2 EDTF compliance.
4. **[REF: DATA-05] Exact Key Mapping:** Field normalization uses lowercase `norm` object mapping (`exactGet`), preventing string collision bugs.
5. **[REF: DATA-12] Primary Chronological Event Sorting:** `validData` is sorted chronologically by `startDate.min ASC` (primary key), duration `DESC` (secondary key), and `title ASC` (tie-breaker).

---

## 3. CARTOGRAPHIC & SPATIAL PHYSICS (GEO-ENGINE)

1. **[REF: MAP-01] Spatial Syntax Support:** Natively parses Well-Known Text (`WKT`), GeoJSON payloads (`GeometryCollection`, `MultiPoint`, `LineString`, `Polygon`), and raw `[Lat, Lon]` pairs.
2. **[REF: MAP-02] Spatial Indexing & Clustering:** Employs an R-Tree spatial index (`MarkerCluster`) to group proximate points within a 40px screen radius.
3. **[REF: MAP-02b] Stacked Pin Coordinate Engine:** Identical Cartesian coordinates `[Lat, Lon]` render a Stacked Pin with a numeric depth badge, triggering a spiderfy animation on click.
4. **[REF: MAP-03] O(1) Spatial State Architecture (Delta Tracker):** Uses `prevActiveIndexRef` memory pointer to target and promote/demote only the active marker delta during navigation, reducing spatial rendering overhead by 99.8%.
5. **[REF: MAP-08] Dynamic Minimap Radar:** A secondary Leaflet map instance tracks primary map bounds, dynamically adjusting zoom offset (-4z default) and reflowing via `ResizeObserver`.
6. **[REF: MAP-80 & 87] Multi-Provider Mapping Stack:** Supports XYZ raster tiles, Protomaps MVT vector tiles via MapLibre GL, WMS GeoServer enterprise services (Harvard Geospatial Library), and IIIF proxies (`allmaps.xyz`).

---

## 4. TEMPORAL PHYSICS & CHRONOLOGICAL MATHEMATICS (CHRONO-ENGINE)

1. **[REF: TL-30] Emerald Active Parity:** Active state tokens across Map pins, TOC indicators, event cards, and duration ribbons strictly use Emerald Active Green (`#28a745` / `#b3e2c2`).
2. **[REF: TL-32] Equal Height Track Partitioning:** The timeline height above the X-Axis is divided equally across all category swimlanes and the Duration Lane:
   $$	ext{totalTracks} = 	ext{laneCount} + 1$$
   $$	ext{laneHeight} = rac{	ext{containerHeight} - 28	ext{px}}{	ext{totalTracks}}$$
3. **[REF: TL-35] Asymmetric Duration Trapezoids:** Duration spans project an asymmetric ribbon using clip-path:
   $$	ext{clip-path}: 	ext{polygon}(0\%\ 0\%, 100\%\ 75\%, 100\%\ 100\%, 0\%\ 100\%)$$
   preserving a 25% height vertical end-cap marker.
4. **[REF: TL-28] Rotating Vector Pattern Hatching:** Inactive duration ribbons render repeating vector hatching (`135deg` /, `90deg` |, `45deg` \) with a 24px pattern cycle (1.2px stroke, 22.8px transparent gap).
5. **[REF: TL-19] 4D Telemetry Hoisting & Temporal Ghosting:** Timeline bounds `[visibleLeftMs, visibleRightMs]` are broadcast to `MapViewer`, attenuating out-of-bounds map feature opacity to 20%.

---

## 5. UI/UX & RESPONSIVE LAYOUT ENGINE

1. **[REF: UI-46] Solid Opaque Active Card Fill:** Active `.event-block` cards use solid opaque `#b3e2c2` fill with normal font weight (`500`) pure black text (`#111111`), securing 11.8:1 WCAG AAA contrast and blocking drop-line vector bleed-through.
2. **[REF: UI-51] Fluid Responsive Axis Rotation:** Viewports `<1024px` render a vertical column stack; viewports `>=1024px` rotate axis 90 degrees to a side-by-side reading room layout (50/50 split).
3. **[REF: UI-65] Micro-Scroll Ribbon Header:** Breaching 40px scroll in `ContentSlider` compresses header padding and shrinks title font size.
4. **[REF: UI-199] Universal 24px Button Topology:** Tier-2 utility toggles use a rigid `24x24px` bounding box with `::after` pseudo-element 8px invisible Phantom Hitboxes for touch target compliance.

---

## 6. DIAGNOSTICS & SYSTEM INTEGRITY (VIBE-MONITOR)

1. **[REF: DIAG-01] Floating Diagnostic HUD:** Draggable, resizable, fixed-position telemetry window (`#vibe-monitor`).
2. **[REF: DIAG-05] Multi-Segment Telemetry Layout:** Top unscrollable segment displays App/Module versions and dataset row counts; middle segment inspects active slide variables; bottom segment provides running error/warning log stream.
3. **[REF: DATA-12] Local Storage Persistence:** User settings, active tag filters, extract type switches, polygon opacities, date locale, and telemetry fields persist across sessions in `localStorage`.
