# Changelog — CarTiMap Engine

All notable changes to this project will be documented in this file. Symmetrically, this project adheres to Semantic Versioning.

## [v8.13.69-b261] — 2026-09-15 — AppOrchestrator v3.7.154-b261, MapViewer v6.4.122-b261, ContentSlider v5.8.36-b253, MediaViewer v2.13.7-b228, TimelineScrubber v26.12.44-b260, ASTCompiler v1.2.74-b228, VibeMonitor v2.2.16-b228 [STABLE MONOLITH RELEASE]
### Cartographic Optics & Vector Z-Stacking
- **Option A Pure Pin Heads [REF: MAP-PIN-01]:** Refactored `createPinHtml` in `MapViewer` to render 100% solid pin heads with zero embedded text interference (`#28a745` for Active, `#ffb300` for VIP, `#007acc` for Inactive), ensuring maximum chrominance contrast across all zoom levels.
- **Floating Top-Right Shoulder Badges [REF: MAP-PIN-01]:** Co-located spatial items at identical coordinates render a floating dark pill badge (`+1`, `+2`) attached outside the pin head on the top-right shoulder (`top: -5px, right: -7px`).
- **Explicit FeatureGroup Vector Z-Stack [REF: MAP-ZSTACK-01]:** Established an explicit bottom-to-top FeatureGroup z-index stack: `polygonLayer` (bottom, `bringToBack()`) $\rightarrow$ `polylineLayer` (middle) $\rightarrow$ `clusterLayer` $\rightarrow$ `markerLayer` (pins, `zIndex = 10000`) $\rightarrow$ `chevronLayerRef` (topmost arrows). Guarantees lines and pins sit physically above polygon fills for 100% click-selectability across the stage.
- **DOM Style Sanitization [REF: MAP-02]:** Enforced DOM element sanitization on active marker promotion (`display = 'block'`, `opacity = '1'`, `zIndex = '10000'`), preventing Leaflet `MarkerClusterGroup` from hiding active markers (`Patra`, `Megara Airfield`, `Piraeus Port`).

## [v8.13.69-b260] — 2026-09-15 — AppOrchestrator v3.7.153-b260, MapViewer v6.4.121-b260, ContentSlider v5.8.36-b253, MediaViewer v2.13.7-b228, TimelineScrubber v26.12.44-b260, ASTCompiler v1.2.74-b228, VibeMonitor v2.2.16-b228
### GIS Layer Promotion & Duration Lane Isolation
- **State-Based Layer Swapping [REF: MAP-02]:** Promotes active slide non-VIP markers from `clusterLayer` (`L.markerClusterGroup`) to `markerLayer` (`L.featureGroup`) during slide transitions, unclustering active `MULTIPOINT` nodes.
- **Duration Lane Y-Offset Isolation [REF: TL-05b]:** Elevated swimlane grid lines (`.tag-lane`) and sticky swimlane label containers (`.tag-lane-label`) in `TimelineScrubber` to `bottom: 38px`, cleanly separating them from the 10px Duration Lane band (`28px` to `38px` from bottom).

## [v8.13.69-b259] — 2026-09-15 — AppOrchestrator v3.7.152-b257, MapViewer v6.4.120-b259, ContentSlider v5.8.36-b253, MediaViewer v2.13.7-b228, TimelineScrubber v26.12.43-b252, ASTCompiler v1.2.74-b228, VibeMonitor v2.2.16-b228
### GIS String Parsing & Compound Word Protection
- **Context-Aware Sub-Label Delimiter Engine [REF: MAP-GEOM-04b]:** Refactored `subLabels` and `places` string splitting in `MapViewer` using smart regex `/(?:\s+-\s+|[\r\n]+\s*-?\s*|\||·|;|·)/`. Correctly splits spaced list hyphens (`"Patra - Megara"`) and multiline bullet dashes (`"- Patra\n- Megara"`) while preserving compound proper nouns (`"Nea-Smyrni"`, `"Port-au-Prince"`) intact.

## [v8.13.69-b258] — 2026-09-15 — AppOrchestrator v3.7.152-b257, MapViewer v6.4.119-b258, ContentSlider v5.8.36-b253, MediaViewer v2.13.7-b228, TimelineScrubber v26.12.43-b252, ASTCompiler v1.2.74-b228, VibeMonitor v2.2.16-b228
### MULTIPOINT Node Individualization
- **Individualized MULTIPOINT GIS Tooltips [REF: MAP-04b]:** Mapped `subLabels` and `places` arrays 1:1 to spatial points across `MULTIPOINT` geometries, appending symmetrical `(i/N)` index fallback suffixes when sub-label counts are incomplete (`Patra (1/3)`, `Patra (2/3)`, `Patra (3/3)`).

## [v8.13.69-b257] — 2026-09-15 — AppOrchestrator v3.7.152-b257, MapViewer v6.4.118-b256, ContentSlider v5.8.36-b253, MediaViewer v2.13.7-b228, TimelineScrubber v26.12.43-b252, ASTCompiler v1.2.74-b228, VibeMonitor v2.2.16-b228
### App Orchestration & Category Retention
- **Active-Slide Preserving Filter Intercept [REF: UI-66]:** Master category deselect retains categories associated with the currently active slide, displaying toast notification: `'To keep at least one category active, filtered to <category>'`.
- **Document Title Standardization [REF: UI-08]:** Standardized browser tab title: `document.title = 'CarTiMap - ' + APP_VERSION`.

## [v8.13.69-b230..b256] — 2026-09-13..14 — AppOrchestrator v3.7.120..150, MapViewer v6.4.102..117, TimelineScrubber v26.12.40..42
### Directional Vectors, Timeline Controls & Media Alignment
- **Polyline Directional Chevrons [REF: MAP-GEOM-03]:** Mounted directional arrow markers (`chevronLayerRef`) on polyline segment midpoints to visualize route vectors.
- **Timeline 7-Control Cluster [REF: TL-05b]:** Mounted top-right horizontal control cluster in `TimelineScrubber` exposing Zoom In, Zoom Scale Factor, Zoom Out, Center Active Event (`🎯`), Reset View (`↺`), Fullscreen Expand (`↕`), and Minimize (`-`).
- **Parallel Media Carousel Sync [REF: ETL-12]:** Aligned multi-value media arrays (`media`, `captions`, `credits`) in `ContentSlider` via `HSTACK` parallel sort weights.

## [v8.13.69-b180..b229] — 2026-09-12..13 — Global Release Baseline Expansion
### ISO 8601-2 AST Decorator, Bibliographic Engine & Mobile Flex Cages
- **Native AST Decorator Integration [REF: ETL-08, ETL-09]:** Embedded `compileCartiMapAST` recursive descent generator for Level 3 EDTF date evaluation without external build steps.
- **Multi-Author Bibliography & XML Generator [REF: ETL-10]:** Implemented MS Word XML bibliography generator and multi-author zip-mapping subroutines.
- **Android Flexbox Containment Cage [REF: UI-62, UI-136]:** Hardened viewport flex cages and reset rules to prevent layout ballooning on Android Chrome and mobile viewports.
- **VibeMonitor Telemetry Upgrade [REF: DIAG-04]:** Upgraded system telemetry dashboard (`VibeMonitor v2.2.16-b228`) for real-time DOM health, memory bounds, and spatial error logging.

## [v8.13.68-b174..b179] — 2026-09-12 — Pre-Parser WKT Splitting & Map HUD Topology
- **WKT Multi-Geometry Interceptor [REF: MAP-01c2]:** Pre-split spatial fields containing line breaks or `<br>` tags into flat arrays prior to WKT parsing, adding `L.featureGroup()` fail-safe fallbacks.
- **Per-Record WKT Layer Signature Scoping [REF: MAP-01g]:** Scoped `uniqueSignatures` per-record inside `data.forEach`, ensuring every event maintains discrete interactive map layers.
- **Map Control Cluster Topology [REF: MAP-HUD-01d]:** Anchored `.map-control-cluster` to top-right corner of `.map-pane` in uniform 30x30px card boxes.

## [v8.13.68-b173] — 2026-09-12 — AppOrchestrator v3.7.84-b173, MapViewer v6.4.71-b173, ContentSlider v5.8.8-b173, MediaViewer v2.13.6, TimelineScrubber v26.12.5-b173, ASTCompiler v1.2.45-b173, VibeMonitor v2.1.16 [STABLE MONOLITH RELEASE]
### Scope Integrity & Syntax
- **Variable Declaration Uniqueness [REF: SYNTAX-05]:** Stripped duplicate `const masterExtractTypes` variable assignment in `AppOrchestrator`, resolving `Uncaught SyntaxError: redeclaration of const masterExtractTypes` during component evaluation.

## [v8.13.68-b172] — 2026-09-12 — AppOrchestrator v3.7.83-b172, MapViewer v6.4.71-b172, ContentSlider v5.8.8-b172, MediaViewer v2.13.6, TimelineScrubber v26.12.5-b172, ASTCompiler v1.2.45-b172, VibeMonitor v2.1.16
### Syntax & Compiler Invariance
- **Regex Literal Escaping [REF: SYNTAX-04]:** Enforced raw string template escaping in assembly scripts, preventing raw line breaks inside regular expression delimiters (`/[\r\n]+/g`) and resolving `Uncaught SyntaxError: unterminated regular expression literal`.

## [v8.13.68-b171] — 2026-09-12 — AppOrchestrator v3.7.82-b171, MapViewer v6.4.70-b171, ContentSlider v5.8.7-b171, MediaViewer v2.13.6, TimelineScrubber v26.12.4-b171, ASTCompiler v1.2.44-b171
### Syntax & AST Integrity
- **MapViewer Block Closure & Fail-Safe [REF: SYNTAX-03b]:** Added explicit `else` fallback clause and closing brace to `if (window.L && window.L.markerClusterGroup)` in `MapViewer`, resolving AST brace imbalance and restoring clean `useEffect` dependency evaluation.

## [v8.13.68-b170] — 2026-09-12 — AppOrchestrator v3.7.81-b170, MapViewer v6.4.69-b170, ContentSlider v5.8.6-b170, MediaViewer v2.13.6, TimelineScrubber v26.12.3-b170, ASTCompiler v1.2.43-b170
### Syntax & AST Integrity
- **MapViewer Block Closure [REF: SYNTAX-03]:** Added missing closing brace and `else` fallback block to `if (window.L && window.L.markerClusterGroup)` inside `MapViewer`, resolving `Uncaught SyntaxError: expected expression, got ','` on `useEffect` terminal dependency array.

## [v8.13.68-b169] — 2026-09-12 — AppOrchestrator v3.7.80-b169, MapViewer v6.4.68-b169, ContentSlider v5.8.5-b169, MediaViewer v2.13.6, TimelineScrubber v26.12.2-b169, ASTCompiler v1.2.42-b169
### Syntax & Parser Portability
- **Array Elision Elimination [REF: SYNTAX-02]:** Replaced parameter destructuring array elisions (`[ , x, y ]`) with direct array indexing (`mItem`, `mItem`), resolving `Uncaught SyntaxError: expected expression, got ','` across strict browser JS engines.

## [v8.13.68-b168] — 2026-09-12 — AppOrchestrator v3.7.79-b168, MapViewer v6.4.67-b168, ContentSlider v5.8.4-b168, MediaViewer v2.13.6, TimelineScrubber v26.12.1-b168, ASTCompiler v1.2.41-b168
### GIS & Multi-Geometry WKT Physics
- **Multi-Geometry WKT Interceptor [REF: MAP-01c2]:** Pre-split `location` cell strings containing `<br>`, `
`, or `|` delimiters into flat arrays before invoking `window.Wkt.Wkt().read()`.
- **Cluster Layer Fail-Safe & Telemetry [REF: MAP-01g]:** Wrapped `L.markerClusterGroup` in fail-safe fallback to `L.featureGroup()` and bound WKT parse events directly to `VibeMonitor` Telemetry (`addLog`).

### UI / UX & Layout Realignment
- **Search Close Centering [REF: UI-12c]:** Replaced text entities with an SVG cross icon inside a circular 32x32px close button.
- **Status Cockpit Brand Frame [REF: UI-08e]:** Framed `aboutBtn` with a 32px border, scaling logo SVG to 28px height without left-edge clipping.
- **30px Map Toolbar & Maximize Button [REF: MAP-HUD-01c]:** Scaled Map toolbar buttons to 30x30px with centered icons and restored Maximize Map Pane button.
- **Horizontal Timeline HUD & Swimlane Alignment [REF: TL-02d, TL-05c]:** Re-architected timeline controls into a horizontal row and aligned hexagon blocks to exact vertical center of swimlane tracks (`topPos = laneIdx * laneHeight`).
- **Dynamic Filter Highlight [REF: UI-01f]:** Corrected filter button active evaluation to compare against `masterExtractTypes.length`.

## [v8.13.68-b166] — 2026-09-12 — AppOrchestrator v3.7.77-b166, MapViewer v6.4.65-b166, ContentSlider v5.8.2-b166, MediaViewer v2.13.6, TimelineScrubber v26.11.10, ASTCompiler v1.2.39-b166
### Map HUD & Controls
- **Top-Right Map Toolbar [REF: MAP-HUD-01]:** Repositioned `.map-control-cluster` and `layersMenuNode` to `top: 12px; right: 12px`, fulfilling the `CarTiMap - ToDo` specification for map button placement.

### Modals & Usability
- **Search Modal Close & Escape Key [REF: SEARCH-02c]:** Updated `.modal-close` button target on `#search-modal` and injected a global `Escape` key listener (`if (e.key === 'Escape')`) across all modals.
- **Logo Button Scaling [REF: UI-08c]:** Enforced double height and width (`48x28px`) on the `CarTiMapperLogo` status bar button.

### GIS & WKT Spatial Physics
- **Robust WKT Engine & Fallback [REF: MAP-01h]:** Validated Wicket WKT parser and added regex fallback parsing for complex geometries with Greece coordinate auto-detection.

## [v8.13.68-b165] — 2026-09-12 — AppOrchestrator v3.7.76-b165, MapViewer v6.4.64-b165, ContentSlider v5.8.1-b165, MediaViewer v2.13.6, TimelineScrubber v26.11.10, ASTCompiler v1.2.38-b165
### Search & Data Ingestion
- **Live Search Direct Execution [REF: SEARCH-01c]:** Re-bound `executeSearch()` directly to active `searchQuery` state and expanded the search target pool to `unfilteredData` (95 records), restoring real-time search filtering.

### GIS & Cartographic Physics
- **Per-Record WKT Signature Scoping [REF: MAP-01g]:** Scoped `uniqueSignatures` per-record inside `MapViewer`, ensuring that distinct historical events sharing geographic coordinates generate individual Leaflet markers, polyline highlights, and camera anchors.
- **Coordinate Swap Auto-Detection [REF: MAP-02]:** Added intelligent lat/lng detection for Greece coordinates (`lat` ~ 34..42, `lng` ~ 18..30) to parse swapped raw coordinate strings cleanly.

### Styling & Layout
- **Status Bar CSS Class Alignment [REF: STY-01c]:** Unified `.status-bar` and `.global-status-bar` CSS selectors in `<style id="global-styles">` (18,547 bytes).

## [v8.13.68-b164] — 2026-09-12 — AppOrchestrator v3.7.75-b164, MapViewer v6.4.63-b164, ContentSlider v5.8.0-b164, MediaViewer v2.13.6, TimelineScrubber v26.11.10, ASTCompiler v1.2.37-b164
### Database Serial IDs & Search Precision
- **1-Based Serial ID Invariance [REF: UI-01f]:** Aligned CSV row mapping to 1-based database IDs (`id: index + 1`), guaranteeing exact 1:1 slide targeting when querying title numbers (e.g., `'74.'` jumps directly to Card 74).
- **Search Modal Auto-Focus [REF: SEARCH-02b]:** Bound `searchInputRef` to focus the search input field automatically upon modal mount.

### Navigation & Content Formatting
- **Title Hyperlinking Engine [REF: ETL-05b]:** Wrapped `ContentSlider` titles in clickable `<a href="${slide.webPage}">` links when valid web URLs exist.
- **Dual-Axis Keyboard Listener [REF: PERF-01c]:** Assigned Up/Down arrow keys to vertical `.content-slider-pane` scrolling, reserving Left/Right arrow keys for slide navigation.

## [v8.13.68-b163] — 2026-09-12 — AppOrchestrator v3.7.74-b163, MapViewer v6.4.62-b163, ContentSlider v5.7.0, MediaViewer v2.13.6, TimelineScrubber v26.11.10, ASTCompiler v1.2.36-b163
### Timeline Physics & Layout
- **Swimlane Gravity Matrix Restoration [REF: TL-02]:** Re-embedded full `TimelineScrubber` v26.11.10, restoring `orderedTags` extraction, dynamic `laneHeight`, and `topPos = (laneIdx * laneHeight) + 5` vertical placement math.
- **Sticky Labels & Track Stripes [REF: TL-12]:** Restored background `.tag-lane` tracks and sticky left `.tag-lane-label` headers, resolving single Y-coordinate mid-height line collapse.
- **Z-Stacking Density Engine [REF: TL-18]:** Re-enabled `stackRegistry` timestamp clustering with `+6px X / +4px Y` offsets to prevent marker eclipsing during concurrent historical events.

## [v8.13.68-b160..b162] — 2026-09-12 — AppOrchestrator v3.7.73-b162, MapViewer v6.4.61-b162, ContentSlider v5.7.0, MediaViewer v2.13.6, TimelineScrubber v26.11.10, ASTCompiler v1.2.35-b162
### Core Component Architecture
- **Monolithic Single-File HTML Architecture [REF: COMP-02]:** Rebuilt application architecture into zero-build, self-contained monolithic single-file HTML distributions.
- **Viewport Sub-Component Restoration [REF: ARCH-01]:** Re-embedded `const MediaViewer` (v2.13.6), `const ContentSlider` (v5.7.0), `const TimelineScrubber` (v26.11.10), `const TelemetryMonitor` (v2.1.16), and `ErrorBoundary` in global script scope.
- **Topological Integrity Verification [REF: DOC-02]:** Validated full 8-component scope tree (`ErrorBoundary`, `TelemetryMonitor`, `MediaViewer`, `ContentSlider`, `TimelineScrubber`, `MapViewer`, `compileCartiMapAST`, `AppOrchestrator`) prior to publication.

## [v8.13.23] — 2026-09-02 — AppOrchestrator v3.7.21, MapViewer v6.4.25, TimelineScrubber v26.11.12 [CONFORMED]
### Fixed
- **WKT Spatial Ingestion Integrity [REF: MAP-01b]:** Resolved map-rendering breakdowns where Well-Known Text coordinate blocks failed to draw. Purged loose manual regex point fallbacks that generated "ghost" markers in out-of-bounds oceanic locations, ensuring invalid geometries cleanly log to Telemetry and skip rendering.
- **Multiline WKT Processing [REF: MAP-01c]:** Implemented a parenthetical-depth cell tokenizer to protect multiline WKT coordinate cells from being fractured by newline-splitting rules.
- **Search and Help Indexing [REF: SEARCH-02]:** Restored full contains-matching search capabilities over raw slide parameters. This corrects the indexing regression which stripped HTML tags, restoring searchability for the "Help" card.
- **Sticky Close Buttons [REF: UI-176b]:** Restructured the spatial design of modals (About, Search) using flexbox geometry. Lock close `[X]` buttons in a stationary position while delegating scrolling to nested scrollable child elements.
- **Viewport Layout White Space:** Restored vertical flexcolumn flow to the parent viewport. Minimizing the timeline pane now causes viewports to scale downward smoothly without leaving blank voids.
- **Resizer Stack Overlaps:** Resolved timeline sizer bleed-through by lowering the `.resizer-dyn-timeline` layer weight to `z-index: 90`, ensuring it rests cleanly below overlay dialogs.

### Added
- **Extract Type Stream Filtering [REF: ETL-14c]:** Added native database ingestion for the `Extract Type` parameter (Column 18). Configured global states to split the event timeline dynamically across four streams: `Storyline` (default), `Context` (Συνδεόμενα Στοιχεία), `Related history` (Ιστορικό Υπόβαθρο), and `Presentation` (Παρουσίαση).
- **Interactive Stream Toggles:** Implemented stream-filtering checkbox controls inside the status cockpit filter drawer, allowing users to toggle entire narrative and historical data layers dynamically.

## [v8.12.85] — 2026-08-29 - AppOrchestrator v3.6.2, MapViewer v6.4.20 [CONFORMED]
### Fixed
- **Nested Template Literal Crash:** Decoupled and refactored the About Modal download link out of the nested JSX template literal by binding it to an independent variable (`downloadBtn`) outside the main render stream. This completely eradicates nested browser-level `SyntaxError` crashes caused by backtick lexical collisions `[REF: CRASH-05b]`.
- **Search Slide Drift:** Upgraded the search click-handler `handleResultClick` to perform `data.findIndex(d => d.id === id)` inside the chronologically-sorted data array, resolving nearby slide displacement regressions `[REF: UI-340]`.
- **Multi-Line WKT Polygon Splitting:** Purged `.flatMap(p => p.split('\n'))` pre-parser operations from the coordinate splitter `[REF: MAP-01e]`. Splits are now restricted to `<br>` tags to prevent the engine from fragmentation-destroying raw multi-line WKT polygons from Google Sheets before they compile.
- **Search Focus Latency:** Appended a 150ms setTimeout hook inside a React `useEffect` linked to `isSearchOpen` to ensure the input text box autofocuses cleanly on high-latency browser viewports without thread-blocking.

### Added
- **Ten-Subblock Architecture:** Structured the entire `AppOrchestrator` block into ten standardized code sectors with high-contrast comments for future edits, eliminating any risk of code drift `[REF: COMP-01]`.
- **Pure CSS Legend Panel:** Constructed a fully scalable, pure CSS Map and Timeline Symbology panel embedded inside the About Modal to satisfy UWK thesis validation constraints without relying on external raster files `[REF: UI-184]`.
- **System Architecture Accordion:** Injected a collapsible `<details>` panel breaking down native URL parameter routing configurations.