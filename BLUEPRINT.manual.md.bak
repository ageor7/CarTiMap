# CarTiMap Engine Master Blueprint (v8.12.24)
### The Living Technical, Spatial-Temporal & Historiographical Specification

This living document contains the rigid engineering, mathematical, cartographic, and methodological specifications for **CarTiMap** and the **HGBB extracts database**. Standardized using the semantic anchor system `[REF: TAG-NAME]`, these rules are bidirectionally deep-linked between the active Preact/Leaflet codebase, the spreadsheet database schemas, and the physical postgraduate thesis (*Forensic Visualisation and Triangulation of Historical Narratives*, Georgiadis 2026) [REF: DOC-01].

---

## 1. Engineering Protocols & Coding Rules <a name="category-1"></a>

### [REF: DOC-01] Two-Tier Documentation (REF-TAGS) [UPDATED]
To prevent technical debt and ensure absolute cross-session consistency, the project documentation is bifurcated. The master repository `README.md` serves as the primary epistemic portal and developer-facing guide, detailing standard API behaviors, URL queries, and database schemas. The companion file `BLUEPRINT.md` houses the rigid architectural, physical, and mathematical parameters of the system. These tiers are permanently interlinked with the physical LaTeX/Word manuscript using the `[REF: TAG-NAME]` semantic taxonomy. Every blueprint entry must carry its specific chapter and section coordinates (e.g., Chapter 5.4, Section 5.4.1), ensuring complete referential traceability between the running code, the database paradata, and the academic defense text. Zero duplication.

### [REF: ARCH-01] Two-Stage Data Pipeline
To support dynamic on-the-fly re-rendering without network latency, the engine strictly separates raw data ingestion (`rawCsvRows`) from the compiled data state (`data`).

### [REF: DOC-02] Architectural Block Taxonomy [UPDATED]
To eliminate cascading errors and enable risk-free surgical patching, the codebase is strictly categorized into visual and logical boundaries:
*   **Major Blocks:** High-level modular components (e.g., AppOrchestrator, MapViewer, TimelineScrubber). Must carry explicit version numbers.
    *   *Syntax:* `// === [ MAJOR BLOCK: ComponentName vX.X.X ] ===`
*   **SubBlocks:** Discrete chunks of logic within a Major Block (e.g., resizers, event handlers).
    *   *Syntax:* `// --- [ SubBlock: LogicDescription ] ---`

### [REF: VER-01] Strict Semantic Versioning
Version numbers are manually tracked on both the global app and individual Major Blocks:
*   **Feature Directives:** Increment the MINOR version and reset the patch (e.g., `v6.0.15` ➔ `v6.1.0`).
*   **Debugging & Hotfixes:** Increment the PATCH version by one (e.g., `v6.0.15` ➔ `v6.0.16`).

### [REF: DOC-03] GitHub Artifact Generation
Every code alteration requires explicit Markdown artifacts prior to code delivery: Commits/Changelogs for history, and Master Blueprint updates for architecture.

### [REF: PROT-01] Documentation Supremacy & Strict MD Formatting
No code patch, architectural adjustment, or bug fix is considered complete without its corresponding Master Blueprint and Changelog updates. The developer AI must always provide these documentation updates strictly in isolated `.md` syntax blocks alongside every code delivery. This protocol guarantees zero architectural drift and prevents UI formatting corruption.

### [REF: PROT-02] Discuss First, Code Later
The developer AI is physically prohibited from generating or outputting code blocks without prior explicit authorization. The mechanical operational loop is strictly locked to: 1) Diagnose Physics. 2) Propose Architecture. 3) Await Explicit User "Go-Ahead".

### [REF: PROT-03] Safety & Functionality Verification
Every proposed architectural patch must be mathematically and structurally cross-referenced against the current active functionality. No update shall be executed if it risks destabilizing existing flexbox layouts, mobile touch-targets, or spatial synchronization engines.

### [REF: PROT-04] Architectural Pushback
The engine (AI) is explicitly authorized and required to challenge user suggestions or design decisions if they violate DOM physics, introduce structural fragility, or break mobile responsiveness. A logic-based case and safe counter-proposals must always be presented.

### [REF: PROT-05] Context Acquisition (The Block Gate)
If a diagnosis requires altering a component whose exact current state is not actively locked in the engine's immediate memory, the engine must explicitly request the user to paste the necessary component code block *alongside* the request for the execution "go-ahead". No blind overwriting is permitted.

### [REF: PROT-06] Touch Target Preservation (Fitts’s Law)
The engine refuses structural UI requests that compromise safe touch interactions on mobile. Primary interaction labels cannot be wholly enveloped in `<a href>` routing tags, as this conflates discrete actions and causes UX failure on smaller viewports.

### [REF: PROT-07] The Context Horizon & Rehydration Protocol
To preserve maximum computational bandwidth and prevent context-window saturation, the engine (AI) is instructed to memorize strictly the architectural taxonomy, DOM physics, and core directives of the platform. If a requested surgical patch requires mutating a specific code module that has fallen beyond the engine's active token horizon, the engine is strictly forbidden from hallucinating or guessing the codebase. The engine must instantly halt execution and trigger a "Context Rehydration" request, prompting the user to re-upload the specific file or block before proceeding.

### [REF: PROT-08] Structural Risk Assessment (SRA)
Prior to authorizing and generating any architectural code patch, the engine must calculate and present a Structural Risk Assessment. This estimation dictates the mathematical probability of the new code breaking or regressing existing application functionality, taking into account component coupling, state dependencies, and external API reliance.

### [REF: PROT-09] Unique Patch Delimiters
To eliminate search-and-replace collisions within the IDE, the engine will explicitly bound all code patches using unique, non-standard alphanumeric strings:
*   *Start Anchor:* `// 🔽🔽🔽 [ START_INJECT: ComponentName vX.X.X ] 🔽🔽🔽`
*   *End Anchor:* `// 🔼🔼🔼 [ END_INJECT: ComponentName ] 🔼🔼🔼`

### [REF: PROT-10] Absolute Blueprint Pathing
To prevent documentation drift, the engine is strictly prohibited from generating orphaned [REF] tags. Every Master Blueprint update provided by the engine must be prefaced with its exact parent chapter integer and title (e.g., *Category: 7. Timeline Physics & Chronological Mathematics*), ensuring the developer knows the exact destination for the text.

### [REF: PROT-11] Continuous Glossary Maintenance
The CarTiMap application utilizes custom terminology to describe its unique mathematical UI and GIS intersections. The engine must actively maintain the CarTiMap Glossary. Any newly invented architectural pattern, CSS methodology, or data pipeline concept generated during development must be formally classified and appended to the Glossary in the subsequent documentation delivery.

### [REF: PROT-13] The Anti-Bloat CDN Mandate
The engine strictly forbids hosting compiled 3rd-party dependencies or massive JavaScript binaries (e.g., >500KB AST parsers) directly within the GitHub repository. Serving raw executable code from version-control endpoints destroys Time-to-Interactive (TTI) metrics by inducing severe V8 Main Thread Blocking. Whenever 3rd-party dependencies exhibit grammatical or functional limitations, the architecture council must engineer lightweight (< 50 lines), native ECMAScript Decorator/Interceptor patterns (e.g., compileCartiMapAST) to mathematically correct the inputs/outputs, strictly maintaining the project's single-file, Zero-Build footprint and utilizing optimized esm.sh distribution.

### [REF: BOOT-CRASH-03] Regular Expression Literal Compilation [NEW]
Regular expression literals parsed natively by the browser must strictly utilize standard single-escaped backslash formatting —such as `\s`, `\d`, or `\(`. Double-escaping backslashes inside a regular expression literal compiles the first backslash as a literal character, leaving trailing formatting operators unescaped. This instantly violates browser-level abstract syntax tree validation, triggering a critical system syntax error that halts script tokenisation.

**[REF: PROT-15] The Regression Audit Gate:** Prior to compiling any client-side JavaScript or CSS alterations, the developer AI must execute a systematic, line-by-line audit comparing the proposed module state against the previous conformed version in /workspace/artifacts/. Any modification that drops previously validated features (such as CSS legend tables, scroll containment, or specific bibliographic details) must be halted immediately. No blind code simplification is permitted without an explicit Socratic explanation in the chat and explicit approval.

**[REF: PROT-16] Unified Delimiter Symmetries:** Semicolons (;) and Greek ano teleias (·) must be conformed as first-class delimiters across all multi-value string splitters (places, sublabels, tags, media) in both the Map and Timeline modules to ensure identical spatial-temporal tracking.

### ## 1. Engineering Protocols & Coding Rules / 2. Interface Geometry

*   **[REF: UI-164c] Symmetrical Status Cockpit [NEW]:** To maintain visual containment and support intuitive chronological scraping, all navigation controls must be clustered into a single, cohesive "Chronological Cockpit" at the absolute center of the viewport's status line. Grouping the incremental navigation triggers (Previous and Next) directly around the numeric record selector/counter prevents mouse-travel fatigue and locks the user's gaze to the active slide index. Telemetry and qualitative time span text must reside strictly to the right of the cockpit to prevent layout overlap on narrower mobile viewports.

[REF: BOOT-CRASH-04] Regular Expression Literal Boundary Escaping [NEW — 2026-08-27]:
Inside native JavaScript regular expression literals (/.../), the forward slash / acts as the absolute delimiter boundary. Even when nested within character classes [...] —where standard punctuation operators are evaluated as literal strings— a forward slash must be explicitly escaped with a leading backslash (\/). Omission of this escape causes the browser's lexical parser to evaluate the unescaped slash as the closing boundary of the regular expression, exposing the remaining character class characters as executable code and triggering an instant SyntaxError that aborts script tokenization on boot.

---

## 2. Data Schema & The Upstream ETL Pipeline <a name="category-2"></a>

### [REF: ETL-01] Purpose of the ETL Formula
The frontend JavaScript engine should *render* data, not *clean* it. The Google Sheets `LET()` formula intercepts messy human inputs, deduplicates tags, and natively compiles valid JSON/WKT before the frontend sees it.

### [REF: ETL-03] ISO 8601-2 Set Geometry Preservation
When aggregating complex chronological arrays, the Google Sheets `LET()` formula utilizes a temporary sanitization phase (stripping `[` and `]`) to safely merge and sort multiple rows without creating illegal nested arrays (e.g., `[[PT12H..PT15H], 1944-12-25]`). To ensure this sanitization does not permanently alter the meaning of a single valid range expansion (e.g., forcing `PT12H..PT15H` into `[PT12H..PT15H]`), a `has_brackets` boolean flag is captured *before* the stripping phase. If the final output is a single element, the formula defers to this flag to reconstruct the exact mathematical structure intended by the user.

### [REF: ETL-04] The Hard Boundary of the Presentation Layer (Zero Frontend Cleaning) [UPDATED]
The CarTiMap JavaScript frontend is strictly a rendering engine, not a sanitation utility. All algorithmic compensation for human data-entry errors or text formatting within the DOM is prohibited. The engine dictates that any complex typographic layout (such as CSS hanging indents or `<a href>` conditional routing) must be handled exclusively by the upstream Google Sheets ETL pipeline (e.g., `ExtractsCombinedV`). The frontend `ContentSlider` merely ingests and natively executes these strings via `dangerouslySetInnerHTML`, ensuring absolute structural parity between the raw database layout and the live application.

### [REF: ETL-05] Hyperlink Interpolation Offloading
The CarTiMap presentation layer actively strips string-quotes from native JSX routing parameters to prevent Virtual DOM compiler collisions. To maintain high performance and prevent Javascript string manipulation overhead, all dynamic Title hyperlinking is mathematically offloaded to the Google Sheets ETL. The spreadsheet utilizes a `MAP`/`LAMBDA` evaluation to test URL existence. If truthy, the Google Sheet natively compiles and exports the required safe anchor bypass string (including `z-index: 50` and `pointer-events: auto`), allowing the frontend to blindly render the validated HTML payload without secondary processing.

### [REF: ETL-08] The Native AST Compiler (Zero-Build Implementation) [UPDATED]
The engine strictly abandons external CDNs for spatial-temporal processing of broken ISO Level 2 Arrays. However, to maintain single-file portability and prevent a 1.2MB Nearley.js binary bloat, the architecture utilizes a Native ECMAScript AST Decorator (`compileCartiMapAST`). This recursive descent generator intercepts Choice Sets (`[]`), Inclusive Lists (`{}`), and Duration Expansions (`..`), mathematically deconstructs them, and forces the core `edtf.js` engine (running at Level 3 for Season/Summer compliance) to evaluate the pristine primitive nodes. It seamlessly reassembles the Abstract Syntax Tree prior to DOM injection, securing 100% mathematical ISO 8601-2 compliance without any build steps or runtime string-coercion.

### [REF: ETL-09] AST Hierarchical Evaluation
The `compileCartiMapAST` decorator strictly enforces mathematical order of operations to prevent array geometry collapse. It must always evaluate Sets `[]` and Lists `{}` via comma delimiter splitting *before* analyzing elements for Range Expansions. Attempting to split ranges before arrays mathematically orphans the array commas, feeding illegal string fragments into the native Nearley AST tree and causing catastrophic `SyntaxError` crashes. Furthermore, the decorator actively intercepts and strips uncertainty qualifiers (`~`, `?`) from explicit durations (`PT30~M`) prior to native evaluation, coercing the approximate boolean flag onto the final object to bypass `edtf.js` Level 2 duration limitations.


### [REF: ETL-12] Parallel Media, Caption, and Credit Sync [UPDATED]
To prevent index de-synchronization across multi-value media carousels in the presentation layer, all grouped timeline media columns must be sorted in perfect parallel with the description snippets. The upstream ETL compiler (`MAKEARRAY`) is strictly prohibited from running flat deduplication on Media (Col 6), Media Caption (Col 7), and Media Credit (Col 8). The compiler must construct an in-memory `HSTACK` table binding each column's vector to the parallel sort_data (Col IQ), execute a descending sort on the priority weight, extract the sorted values, filter out empty fields, and finally apply a stable `UNIQUE` deduplication before compiling the final cell string via `TEXTJOIN`. This mathematically guarantees that `mediaItems[i]` always maps to its true historical `captions[i]` and `credits[i]` on the Hero Stage. This protocol strictly respects all manual overrides defined in `v6.1.2b` (specifically target sheet `ExtractsT` and `first_record_cols, {5,39}`).


### [REF: DATA-02] The Cartographer's Dilemma
Humans use `[Lat, Lon]`. GIS standards (GeoJSON, WKT) demand Cartesian `[Lon, Lat]`. The spreadsheet translates this natively, ensuring export interoperability with QGIS/PostGIS.

### [REF: DATA-03] Spatial Deduplication
The ETL wraps arrays in `UNIQUE()`, purging redundant geographic nodes before casting them to prevent overlapping DOM elements and broken Z-indexes.

### [REF: DATA-05] Direct Key Mapping
Data is normalized via lowercase `norm` object mapping (`exactGet`). Legacy `fuzzy()` logic is deprecated to prevent column string collisions.

### [REF: DATA-06] Strict Euro-Date Logic
`parseEuroDate` forces `DD/MM/YYYY` parsing to prevent US-browser inversion.

### [REF: DATA-09] Media & Metadata Extraction
The `exactGet` ingestion loop explicitly extracts `media`, `caption`, and `credit` columns from the CSV payload. These strings are flattened using the `omniSplitRegex` (`/\||\r?\n/`) to guarantee parallel 1:1 array mapping.

### [REF: DATA-10] Place/SubLabel Convergence
Hover Tooltips are mathematically bound to the `Place` column, enforcing single-source-of-truth location labeling.

### [REF: DATE-11] Time Preservation
The parser decouples `HH:mm:ss` payloads from date strings using whitespace isolation to prevent `00:00:00` collision bugs in timeline zoom physics.

### [REF: SUB-01] Universal SubLabel Delimiters
RegEx parser `/[|\-·;]/` splits sublabels, capturing pipes, semicolons, dashes, and the Greek Ano Teleia (`·`).

### [REF: MED-08] Aggressive CRLF Sanitization
RegEx `/\||\r?\n/` identifies and strips invisible Windows-style carriage return `\r` ghosts, preventing them from fusing to URLs and causing HTTP 404s.

### [REF: MED-11] The Omni-Splitter Matrix
The engine utilizes a mathematically precise delimiter interceptor (`/[\r\n]+|\\n/`) during the CSV mapping phase to eliminate destructive parsing bugs where commas naturally occurring in filenames unintentionally fractured the URL strings.

### [REF: TL-17] Timeline Omni-Splitter
Intercepts incoming `item.tags` via `getParsedTags()`. Ensures horizontal swimlanes split properly during background generation, scaling vertical boundaries appropriately.

### [REF: DATA-15] String Storage Optimization [NEW]:
To prevent index fragmentation and optimize client-side data transfer, the HGBB database enforces strict string typing. Unbounded narrative fields and complex, multi-point WKT or GeoJSON strings must be typed as TEXT to trigger out-of-line database storage, keeping primary tables compact. Conversely, all relational join keys, standard URI links, and short metadata tags must be typed as bounded VARCHAR variables (e.g., VARCHAR(64) or VARCHAR(2048)) to allow standard B-Tree indexing and prevent hash collision slowdowns during data compilation.

### [REF: ETL-08b] AST Range Extraction Bounds [NEW]
During recursive chronological range expansions —such as those mapping `Date1..Date2` intervals— the compiler must explicitly target isolated string indices rather than passing raw parsed arrays to down-level parser iterations. Passing an array container into string-coercive loops triggers array-to-string serializations that produce illegible, comma-separated streams. This process violates standard Extended Date/Time Format parameters and breaks chronological timeline sorting.

[REF: ETL-14b] Symmetric Tag Ingestion Protocol [UPDATED - 2026-08-27]:
To prevent runtime data loss inside browser-side state-filtering loops, the Data Ingestion Phase must maintain absolute delimiter symmetry with the Tag Map Extraction Phase. The primary tags column parser must not rely on simple comma splitting (split(',')). It is strictly mandated to parse tags utilizing a conformed regex /[,\r\n|;·]+/ on initial load. This guarantees that any multi-value arrays compiled upstream via TEXTJOIN are instantly flattened into primitive strings prior to Virtual DOM diffing, completely neutralizing the activeTags intersection failure that previously culled un-split composite strings on boot. Semicolons (;) and Greek ano teleias (·) must be evaluated as primary splitting boundaries.

[REF: ETL-01] Upstream Horizontal Ingestion Compiler (v6.1.7) [UPDATED]
The horizontal consolidation formula (ExtractsCombinedV) must resolve spatial coordinate cell boundaries before running WKT keyword validation blocks. If a grouped coordinate cell contains multi-row inputs or inline HTML line breaks ((?i)<br\s*/?>), the formula splits them by clean newlines (CHAR(10)) and processes them as a vertical vector utilizing TOCOL(..., 1). To prevent Google Sheets from stripping leading zeroes or truncating coordinate decimals during splitting, the formula must wrap each element in temporary @-armor, stripping the character only after the transposition is complete. Furthermore, nested quotation marks inside compiled GeoJSON strings must be escaped using doubled double quotes ("") to satisfy the Sheets formula compiler.

### [REF: ETL-01b] Google Sheets Ingestion (gviz/tq vs export) [UPDATED - 2026-08-29]
To prevent client-side "Database Sync Failure" exceptions, the CarTiMap client rendering layer must exclusively fetch raw Google Sheet data utilizing Google's Visualization Query API endpoint (`/gviz/tq?tqx=out:csv&gid=...`). Developers are strictly prohibited from utilizing Google's raw file export endpoint (`/export?format=csv`). While both endpoints conceptually return CSV payloads, the `/export` endpoint does not support cross-origin queries and refuses to transmit Access-Control-Allow-Origin headers to anonymous user-agents. Reverting to `/gviz/tq` guarantees 100% CORS-compliance, permitting secure, serverless database synchronization directly inside the browser across all domains (including GitHub Pages, local files, and resource-constrained tablets).

#### [REF: ARCH-01b] Decoupled Data Pipeline (Ingestion vs. Parsing Telemetry) [NEW - 2026-08-30]
To secure robust client-side diagnostic transparency, the data synchronization lifecycle must be split into two isolated, sequential execution bounds:
- **Ingestion Zone:** Contains only the asynchronous promise network chains. Rejection here strictly indicates origin blocking (CORS), unreachability, or transport-layer timeouts, setting the UI state directly to `"Connection Timeout"`.
- **Compilation Zone:** Contains CSV parsing (`Papa.parse`), chronological normalization, and index mapping. Handled inside a local `try-catch` scope, any runtime or structural mapping exceptions caught here designate localized formatting or variable typing failures, setting the UI state directly to `"Dataset Parse Error"`.

---

## 3. Cartographic & Spatial Physics <a name="category-3"></a>

### [REF: MAP-01] WKT Engine
The engine natively parses Well-Known Text (WKT) via the `Wicket` library. Falls back safely to GeoJSON or standard Lat/Lon pairs.

### [REF: MAP-01b] WKT Axis Inversion Physics
WKT syntax natively formats coordinates as Cartesian `[Longitude, Latitude]`. Leaflet's mapping engine natively expects `[Latitude, Longitude]`. The Wicket library (`wkt.read().toObject()`) automatically performs this axis inversion. The engine must *never* double-invert Wicket outputs. However, if the engine falls back to manual Regex parsing for raw `POINT()` strings, it must explicitly invert the capture groups `[parseFloat(m[1]), parseFloat(m[2])]`. Basic comma-separated inputs (e.g., `37.98, 23.72`) are naturally `[Lat, Lon]` and require zero inversion.

### [REF: MAP-02] Spatial Decluttering (MarkerCluster)
The map utilizes an R-Tree spatial index (`MarkerCluster`) to group overlapping geographic elements into numbered bubbles based on a 40px screen radius.

### [REF: MAP-02b] Identical Coordinate Stacking (The "Stacked Pin") [UPDATED]
By default, Leaflet's `MarkerCluster` groups any proximate points into a generic circular bubble. To provide better visual narrative clarity for identical locations, the engine utilizes a custom `iconCreateFunction` interceptor. If a cluster contains markers that share the exact same `[Lat, Lon]` signature (e.g., multiple distinct historical events occurring inside the identical hotel), the engine renders a "Stacked Pin" (a standard marker adorned with a numeric depth badge) instead of a generic bubble. To mathematically evaluate this without crashing, the Javascript engine explicitly targets `children.getLatLng()` (and specifically utilizes `.at(0)` under [REF: MAP-02c]) to extract the physical Cartesian value from the cluster array before comparison. Clicking this pin triggers a native `spiderfy` animation, allowing the user to select the specific chronological event.

### [REF: MAP-02c] The Anti-Swallow Indexing Pattern
During clustering operations, the engine dynamically accesses the internal child markers of a cluster array. To prevent upstream compiler/parser loops from accidentally stripping integer brackets (e.g., mistaking `[0]` for a footnote citation), the engine exclusively utilizes the ES6 method `.at(0)` to read matrix indices safely (`const firstLatLng = children.at(0).getLatLng();`).

### [REF: MAP-02d] Smart Spiderfy Interceptor
Native `zoomToBoundsOnClick` behavior creates endless zooming loops for non-exact proximity clusters. The `MapViewer` disables this native logic and intercepts the `clusterclick` event. If the viewport depth is `>= 10z`, it forcefully executes `c.layer.spiderfy()`, breaking up the pins instantly without altering the camera. If `< 10z`, it executes a safety flight into the macro-bounds first to prevent drawing cross-continental spider legs.

### [REF: MAP-03] Dynamic VIP "Slide Focus"
The map utilizes a "State-Based Layer Swapping" architecture. It temporarily physically removes the active slide's markers from the cluster group, elevates them with high z-indexes and custom UI ("Fire Pins" / "Stacked Pin"), and then drops them back into the background when the user leaves the slide. To execute this in real-time without lagging the browser, the map builds a global dictionary (`markersRef`) on load. This provides an $O(1)$ instant lookup, preventing the browser from brute-force looping through thousands of markers on every slide change.

### [REF: MAP-04] Parallel Array (Sub-Labels)
Switched to a Strict Linear Map algorithm. If 3 geometries and 3 sub-labels are present, the engine mathematically locks them to prevent label duplication across LayerGroups.

### [REF: MAP-04b] Explicit SubLabel Parity
The map enforces a strict fallback hierarchy for multi-element geometries to prevent array out-of-bounds failures. If an event provides fewer SubLabels than geographic MultiPoints, the engine mathematically falls back to the local Place array, and ultimately to the root event Title.

### [REF: MAP-05] Linear Sub-Label Mapping
MultiPoint geometries are recursively flattened into a linear array to ensure 1:1 parity with the pipe-delimited sub-label string.

### [REF: MAP-06] The Breathing Map (Temporal Ghosting)
The Map layer natively tracks chronological telemetry (`visibleTimeBounds`) broadcasted by the Timeline Scrubber. Any coordinate failing to intersect the active visible chronological window is instantly degraded to 20% opacity. Furthermore, ghosted pins are surgically detached from the MarkerCluster bucket and pushed to a passive base layer, guaranteeing that cluster gravity numbers perfectly reflect only the active events of the current epoch.

### [REF: MAP-07] Tooltip Physics
Tooltips are anchored with a `-48px` vertical offset to provide aesthetic breathing room above the Map Pin head.

### [REF: MAP-07b] Semantic Tooltip Engine [UPDATED]
To maximize tactical awareness and prevent redundant data rendering, tooltips are semantically bifurcated. Individual pins explicitly focus on Geographic Context, broadcasting their `itemPlace` (or relevant SubLabel) since the Content Pane already provides the Event Title. Aggregated clusters execute a native `.getAllChildMarkers()` extraction loop, projecting a unified `itemPlace` as a bold structural header, followed by a bulleted list of the underlying event titles extracted from the node properties.

### [REF: MAP-08] Dynamic Radar Architecture (Secondary Map Sync)
The minimap dynamically tracks the main map's focal telemetry in real-time. By explicitly mapping the `zoomLevelOffset` to a global UI state variable (`minimapOffset`), the engine allows the user to dynamically adjust their geographic context "Radar" from `-2` to `-8` zoom levels out.

### [REF: MAP-08b] Bidirectional Radar Telemetry
The Minimap acts as an interactive depth-gauge. The engine utilizes an `isSyncingRef` clutch. If the user manipulates the radar directly (scroll-wheel/pinch zoom), the engine calculates the integer gap between the main and secondary cameras and broadcasts it back to the global React state. This mathematically guarantees that manual interactions permanently update the actual `minimapOffset` configuration value.

### [REF: MAP-08c] Radar DOM Expansion
The `.minimap-container` is decoupled from rigid sizes using `resize: both`. A secondary `ResizeObserver` monitors this specific node. When a user drags the container corner, it instantly fires `miniMap.invalidateSize()`, forcing the WebGL context to fill the newly claimed DOM space.

### [REF: MAP-10] Visual Projection Math (Minimum Viewport Clamp)
To circumvent the minimap aiming rectangle shrinking into an invisible dot at deep zoom levels, the engine overrides the true map bounds, projecting a synthetic, mathematically expanded set of `L.latLngBounds` to guarantee the reticle never visually shrinks below a 30-pixel readable limit.

### [REF: MAP-11] The Basemap Core Registry
Securely holds all required Leaflet construction data for a curated list of providers. When the user selects a new Basemap, the engine natively intercepts the telemetry and mathematically injects the new target layer into both the Main Map and the Minimap simultaneously to prevent z-index rendering collisions.

### [REF: MAP-80] Dynamic Web Map Service (WMS) Routing [UPDATED]
To support institutional academic mapping platforms, the Google Sheet registry actively parses the format and `wmsLayer` columns. When the `MapViewer` detects a `wms` format flag, it dynamically bypasses standard XYZ tile fetching. It routes the layer through `L.tileLayer.wms()`, requesting a custom, dynamically cropped PNG render directly from the institution's enterprise GeoServer. This architecture natively supports platforms like the Dipylon Society and the **Harvard Geospatial Library (HGL)** (e.g., using `https://geodata.lib.harvard.edu/mapimages_public/wms` for WMS server, and searching page source for `data-leaflet-viewer-layer-id-value` for layer ID, such as `mapimages_public:G6814_A9_1923_G4`), completely eliminating the need for third-party IIIF georeferencing proxies.
*   **Server-Side Compositing:** The engine natively supports multi-layer requests to reduce client-side overhead. By passing a comma-separated list of namespaces (without spaces) into the `wmsLayer` database column (e.g., `workspace:layer1,workspace:layer2`), the engine commands the target GeoServer to composite the layers server-side and transmit them as a single flattened image overlay.

### [REF: MAP-81] Overlay Severance [NEW]
The engine strictly refuses to render heavy historical overlays on the Minimap. By forcing the Minimap to run solely on the underlying Basemap, the engine slashes HTTP payloads to third-party IIIF servers by 50%.

### [REF: MAP-85] WebGL & Vector Tile Architecture
To support Protomaps vector data (`.mvt`/`.pbf`), the engine dynamically injects MapLibre GL JS and its Leaflet binding via asynchronous script loading. The WebGL engine is only spun up when a vector basemap is actively selected, preserving application performance.

### [REF: MAP-86] Layer Casing (Cartographic Styling)
Vector basemap aesthetics are controlled via a local `style.json`. To achieve high-end cartographic roads, the engine utilizes WebGL layer casing (a thicker casing layer underneath a thinner fill layer). The styling utilizes the `stops` array to dynamically scale `line-width` based on zoom level.

### [REF: MAP-87] The IIIF Spatial ETL Proxy (Allmaps Integration)
The CarTiMapper engine strictly refuses raw institutional front-end viewer URLs. To overlay un-georeferenced historical scans (e.g., from Harvard Library or Princeton), the data pipeline explicitly requires the extraction of the underlying IIIF `MANIFEST.json`. This manifest must be mathematically anchored to geographic coordinates using a proxy engine like `allmaps.xyz`. The resulting XYZ tile endpoint (`https://allmaps.xyz/images/{ID}/{z}/{x}/{y}@2x.png`) is the only valid payload permitted in the URL column of the `LayersT` database for this class of overlays.

### [REF: PERF-02] O(1) Spatial State Architecture (The Delta Tracker)
The engine uses a mathematically pure $O(1)$ index tracker (`prevActiveIndexRef`). During navigation, it explicitly targets and demotes *only* the old marker, and targets and promotes *only* the new marker, dropping rendering complexity by 99.8%.

### [REF: PERF-03] Spatial Animation Interpolation Brake
Injecting an absolute `map.stop()` instantly aborts the active physics frame during rapid keyboard navigation, freeing the thread to calculate the next flight path cleanly.

### [REF: PERF-03b] Kinetic HTTP Brakes (The Slow Proxy Armor) [UPDATED]
By default, Leaflet rapidly fetches tiles while the camera executes its 2.5-second `flyToBounds` path. However, when parsing historical overlays through live-warping IIIF proxies (like `allmaps.xyz`), this aggressive fetching creates a catastrophic backlog. The camera flies past the coordinates before the proxy can finish warping the image, causing the browser to violently terminate the requests (`NS_BINDING_ABORTED`). To mathematically armor the engine against this, all secondary Map Overlays are rigidly configured with `updateWhenZooming: false` AND `updateWhenIdle: true`. This entirely freezes the HTTP fetching queue while the camera is in motion, commanding the browser to only ping the slow IIIF servers the exact millisecond the camera comes to a dead stop.

### [REF: PERF-04] The Transmission Clutch (Map Debouncing)
To fully decouple the Map DOM from rapid user telemetry, a `debouncedIndex` transmission clutch suspends heavy spatial math until a `100ms` pause in keystrokes is detected.

### [REF: PERF-05] MarkerCluster Bulk Ingestion Engine
Geometries are collected into an invisible JavaScript array (`bulkClusterMarkers`). A singular `clusterLayer.addLayers()` command is executed post-loop, reducing geometric grid generation to a single millisecond execution phase.

### [REF: PERF-33] Synchronized Boot Camera
Map initialization forces a strict execution latency. The generic `fitBounds` payload executes first to paint geometry, immediately followed by the precise `activeIndex` marker `flyToBounds` command. This geometrically guarantees that the camera actively dives to the target upon boot at the precise user-defined `maxAutoZoom` depth.

### [REF: BOOT-CRASH-02b] Hardcoded Pin Dimensions [UPDATED]
Custom HTML CSS markers physically measure `24px` by `34px`. To insulate the geometry against documentation/markdown parsers inadvertently swallowing bracketed arrays, the engine mathematically enforces these pixel boundaries by declaring strict Leaflet constructor objects (`iconSize: new L.Point(24, 34)`, `iconAnchor: new L.Point(12, 34)`) instead of shorthand arrays.

*   **[REF: DOC-02] Sub-Block Surgical Landmarks [UPDATED]:** Logical sub-blocks within major components are strictly isolated using physical comment boundaries (START_SUBBLOCK and END_SUBBLOCK). Patching scripts must target these boundaries exclusively to preserve bracket parity.
*   **[REF: MAP-03b] Decoupled Kinetic Camera Flight [NEW]:** To eliminate camera jitter during timeline scrubs, marker opacities (Temporal Ghosting) are calculated within a lightweight effect, while heavy flyToBounds transitions are bound to an isolated effect triggered strictly when activeIndex mutates.
*   **[REF: BOOT-CRASH-03] Character Class Range Bounds [NEW]:** RegExp character classes containing literal dashes or backslashes must explicitly escape these tokens to prevent the compiler from evaluating ASCII ranges and throwing fatal SyntaxError halts on boot.

Update [REF: UI-164c] (Symmetrical Status Cockpit): We must codify the strict physics of the new tripartite status bar. This records the exact spatial layout bounds: .status-left locked to system utilities, .status-center containing the center-grouped Navigation Cockpit [Prev] [ 1 / 87 ] [Next] and dynamic timeline span telemetry, and .status-right housing context utilities (Filters, Search, Undo).
Update [REF: UI-164d] (Proportional Logo Constraints): Document the mathematical rules of the logo component. It must be strictly bounded to 24px height with automatic width scaling (width: auto;) inside the 32px status line wrapper, leaving a symmetrical 4px top/bottom padding buffer to protect its polygonal SVG aspect ratio from distortion.
Update [REF: ETL-08] (AST Compiler Recursion): Record the structural correction inside compileCartiMapAST. Specifically, document how the range expansion split (..) was stabilized by passing isolated string elements (parts[0] / parts[1]) into the recursive loop, resolving the array-passing compiler crash.

[REF: MAP-04] Type-Agnostic Sequential Index Coupling [UPDATED]
To prevent coordinate-label desynchronization across multi-geometry slides, the visualizer must decouple layer-label mapping from Leaflet's internal, auto-incremented object IDs (_leaflet_id). During the initial WKT tokenization loop inside parseGeometryCollection, each extracted sub-layer must be stamped with its original, raw WKT string index (_geometryIndex) and nested sub-coordinate sequence index (_childIndex) at the exact millisecond of creation. Symmetrically, the tooltip rendering engine evaluates the place labels by splitting strings by newlines first to isolate the parent block (_geometryIndex), and then by semicolons to retrieve the precise descriptor matching the active _childIndex position.
[REF: MAP-05] Fallback Axis Inversion Physics [UPDATED]
When a Well-Known Text (WKT) string fails to compile through Wicket and triggers a regex catch block fallback, the manual extractor must enforce standard WKT axis inversion. Because OGC standards dictate Cartesian POINT(Lon Lat) formatting while Leaflet expects L.LatLng(Lat, Lon), the fallback regular expression must explicitly swap the captured coordinate groups (parseFloat(m.at(2)) for Latitude, parseFloat(m.at(1)) for Longitude). Plain, non-WKT coordinate cells parsed from the database must bypass this inversion loop, ingesting raw Lat, Lon arrays directly.

#### [REF: MAP-01c] Multi-Line WKT Array Splitting [NEW - 2026-08-29]
When the horizontal LET() compiler aggregates deconstructed event rows, it frequently produces line-break separated lists of geographic shapes within a single cell. Attempting to parse these strings directly via the Wicket library triggers a fatal syntax crash. The `MapViewer` engine implements a pre-parser string interceptor: it splits the incoming `location` string by `<br>` tags and newlines (`\n`) into a flat array, processing each geometry node independently. This ensures that composite, multi-vocal coordinate matrices render perfectly as distinct, interactive spatial nodes without breaking the Leaflet cycle.

[REF: MAP-01c] Multi-Line WKT Array Splitting [NEW - 2026-08-29]
When the horizontal LET() compiler aggregates deconstructed event rows, it frequently produces line-break separated lists of geographic shapes within a single cell (e.g., POINT(...)<br>POINT(...)). Attempting to parse these strings directly via the Wicket library triggers a fatal syntax crash inside the rendering loop. The MapViewer engine implements a pre-parser string interceptor: it splits the incoming location string by <br> tags and newlines (\n) into a flat array, processing each geometry node independently. This ensures that composite, multi-vocal coordinate matrices render perfectly as distinct, interactive spatial nodes without breaking the Leaflet cycle.
[REF: MAP-02b] Identical Coordinate Stacking [UPDATED - 2026-08-29]
When multiple historical actions share mathematically identical coordinates, standard mapping libraries overlap and eclipse markers. To communicate chronological volume without visual bloat, the engine intercepts overlapping coordinates and groups them into a custom “Stacked Pin” featuring a numeric depth badge. For complex geometries, the tooltip rendering engine evaluates the place labels by splitting strings by newlines first to isolate the parent block, and then by semicolons to retrieve the precise descriptor matching the active sub-coordinate sequence.

#### [REF: MAP-01c] Multi-Line WKT Array Splitting [NEW - 2026-08-29]
When the horizontal LET() compiler aggregates deconstructed event rows, it frequently produces line-break separated lists of geographic shapes within a single cell (e.g., `POINT(...)<br>POINT(...)`). Attempting to parse these strings directly via the Wicket library triggers a fatal syntax crash inside the rendering loop. The `MapViewer` engine implements a pre-parser string interceptor: it splits the incoming `location` string by `<br>` tags and then flattens them by string-based newlines (`\n`) into a flat array, processing each geometry node independently. This string-based fallback bypasses regular expression escaping anomalies entirely, ensuring that composite, multi-vocal coordinate matrices render perfectly as distinct, interactive spatial nodes without breaking the Leaflet cycle.

#### [REF: MAP-01d] Fallback Coordinate Axis Realignment [NEW - 2026-08-29]
When the Leaflet MapViewer's primary WKT engine encounters nested geometries that trigger parser catch-blocks, it utilizes regular expression fallback mapping to capture decimal primitives. To prevent JavaScript array-to-string type coercion (where `parseFloat(match_array)` evaluates both Lat and Lon to the identical first index), coordinate extraction must explicitly target indexed group sequences: `parseFloat(match_array[2])` for Latitude, and `parseFloat(match_array[1])` for Longitude. Symmetrically, this maintains consistency with WKT’s Cartesian axis layout (`POINT(Lng Lat)`) and prevents collapsed flat diagonal geometries, ensuring 100% visual rendering accuracy.

#### [REF: UI-71b] Basemap Opacity Attenuation [NEW - 2026-08-29]
To allow qualitative researchers to visually attenuate high-contrast raster background details, the Layers dropdown incorporates inline `<input type="range">` opacity sliders dynamically nestled below active basemap radio buttons. Adjusting the slider binds the value directly to a reactive `basemapOpacity` state variable. Symmetrically, a React `useEffect` hook intercepts opacity mutations and directly executes `setOpacity()` on the active base and mini-base Leaflet tile-layers in constant time, avoiding expensive canvas re-creations.

#### [REF: MAP-01d] Fallback Coordinate Axis Realignment [NEW - 2026-08-29]
When the Leaflet MapViewer's primary WKT engine encounters nested geometries that trigger parser catch-blocks, it utilizes regular expression fallback mapping to capture decimal primitives. To prevent JavaScript array-to-string type coercion (where `parseFloat(match_array)` evaluates both Lat and Lon to the identical first index), coordinate extraction must explicitly target indexed group sequences: `parseFloat(match_array.at(2))` for Latitude, and `parseFloat(match_array.at(1))` for Longitude. Symmetrically, this maintains consistency with WKT’s Cartesian axis layout (`POINT(Lng Lat)`) and prevents collapsed flat diagonal geometries, ensuring 100% visual rendering accuracy.

#### [REF: UI-71b] Basemap Opacity Attenuation [NEW - 2026-08-29]
To allow qualitative researchers to visually attenuate high-contrast raster background details, the Layers dropdown incorporates inline `<input type="range">` opacity sliders dynamically nestled below active basemap radio buttons. Adjusting the slider binds the value directly to a reactive `basemapOpacity` state variable. Symmetrically, a React `useEffect` hook intercepts opacity mutations and directly executes `setOpacity()` on the active base and mini-base Leaflet tile-layers in constant time, avoiding expensive canvas re-creations.

#### [REF: MAP-05] Complete Separation of WKT and Standard Coordinate Parsers [UPDATED - 2026-08-29]
To satisfy the Zero-Frontend-Cleaning Mandate [REF: ETL-04] and secure epistemic data accuracy, the spatial engine must strictly separate Well-Known Text (WKT) from explicit Lat/Lon coordinate notation:
1. **WKT Integrity:** If a WKT string (e.g. POINT(...), LINESTRING(...), POLYGON(...)) is syntactically malformed and fails during Wicket compilation, the MapViewer must fail gracefully. It is strictly prohibited to execute manual regular expression extractions inside catch blocks to "rescue" or guess the coordinate parameters, as this masks upstream data-entry errors and generates invalid cartographic layers.
2. **Explicit Lat/Lon Support:** Symmetrically, standard geographic coordinates are fully supported but must be formatted explicitly matching /^\s*(-?\d+(?:\.\d+)?)[,\s]+(-?\d+(?:\.\d+)?)\s*$/. Standard coordinate parsing operates purely on its own conditional branch and must never serve as a catch-block fallback for failed WKT inputs.

#### [REF: MAP-01e] Multi-Line Geometry Preservation & Decoupling [NEW - 2026-08-29]
To satisfy the Zero-Frontend-Cleaning Mandate [REF: ETL-04] and prevent pre-parser geometry corruption, the location parser must split coordinate coordinates strictly by HTML break tags (`<br>`) and never by physical newline `\n` characters. Standard OGC WKT structures natively utilize internal carriage returns to span multiple lines. Splitting by physical newlines chops these structures into invalid grammatical fragments, triggering fatal catch-blocks inside Wicket. By preserving whole multi-line arrays and decoupling the parser, Wicket evaluates complex polygons, sewers, and polylines cleanly while point coordinate arrays remain isolated on their own numeric matching branches.

### [REF: MAP-02c] The Anti-Swallow Indexing Pattern [UPDATED - 2026-08-30]
During both Leaflet marker clustering and AppOrchestrator date parsing, the JavaScript engine dynamically accesses indices of array structures. To insulate the codebase from compiler filters, markdown engines, or Git tools that accidentally swallow or strip square brackets (e.g., mistaking `parts[0]` for a markdown footnote indicator), all array index mapping must explicitly use the safe ES6 `.at()` accessor prototype (e.g., `parts.at(0)`). This prevents syntax and runtime exceptions while guaranteeing strict data format alignment across all compiler channels.

---

## 4. UI/UX Elements & Design Solutions <a name="category-4"></a>

### [REF: UI-05] Visual Hierarchy (Map Pins)
Permanent geographical anchors (VIPs) = Gold stars / pins. Active elements = Oversized Green / Fire pins. Inactive clusters = Standard Blue / Red pins.

### [REF: UI-08] Multi-Context Branding [UPDATED]
The visual identity of CarTiMap is anchored by the Logo Hex-Frame Chrono-Compass. To completely sever branding dependencies from presentation-layer execution, the master vector geometry is maintained as a standalone, scale-free asset (`cartimap-logo.svg`). The asset explicitly preserves the #2c3e50 (Slate Blue) bracket base, #007acc (Sapphire Blue) primary needle, #28a745 (Active Green) secondary needle, and the sub-pixel `<filter id="dot-glow">` blur coordinates. This ensures a mathematically perfect, zero-distortion brand representation across all external documentation repositories, social preview cards, and web hosting platforms.

### [REF: UI-13] Metadata Hierarchy
The `📍 Place` badge utilizes a non-bold, pill-shaped aesthetic to distinguish metadata from narrative text.

### [REF: UI-40] Golden SVG Tag Identity
Semantic Tags abandon native OS Emojis in favor of a mathematically plotted inline `<svg>` path (`#ffc107`), universally rendering a flawless geometric identity across all browser engines.

### [REF: UI-42] InvalidateSize Base-Tile Forcing
The engine mechanically circumvents React Flexbox layout race conditions by delaying execution for 250ms and forcing `mapInstance.invalidateSize()`, commanding Leaflet to poll the true DOM dimensions and trigger the pending HTTP tile requests.

### [REF: UI-46] Left-Aligned Menu Dock
Secondary utility tools (Settings, Monitor) are condensed into a single popover menu. The `☰ Menu` button is rigidly anchored to the absolute far-left edge of the status bar.

### [REF: UI-47] The 75ch Readability Clamp
The narrative description block (`.slide-desc`) is mathematically clamped to `max-width: 75ch` and automatically centers itself, preserving the natural vertical scroll while maintaining an optimal typographical line-length.

### [REF: UI-48] Flex-Greed Typographic Capping
Desktop viewports default to a 50/50 primary split. However, the narrative text wrapper is strictly capped at `max-width: 95ch`. Once the boundary hits its absolute typographical readability limit on ultrawide monitors, the adjacent Visual Pane (Map & Media) automatically engages `flex: 1 1 0; width: auto;`, consuming 100% of the remaining horizontal space.

### [REF: UI-51] Fluid Axis Rotation & True 50/50 Baseline
The core engine defaults explicitly to a `--primary-split: 50%` CSS variable. When the view crosses the `1024px` threshold and geometric axis rotates, the narrative pane and the visual panes mathematically split the absolute screen real estate directly down the median, abandoning the legacy asymmetrical bias.

### [REF: UI-51b] Portrait Layout Protection
The Flex-Greed logic is strictly suspended inside the Mobile Matrix (max-width: 1023px). The system explicitly forces `--primary-split: 55%;` vertically, protecting the reading area on tablets and mobile phones.

### [REF: UI-52] Layout Boundary Mathematical Reset
The absolute instant the browser boundary crosses the `1024px` threshold, the app automatically zeroes structural variables back to baseline, ensuring perfect proportional integrity.

### [REF: UI-62] Strict Android Flexbox Containment Cage
The global stylesheet enforces an absolute CSS cage (`max-width: 150px !important; flex-shrink: 0 !important`) entirely forbidding the Android rendering engine from expanding the Minimap node.

### [REF: UI-65] The Micro-Scroll Ribbon (Dynamic Header)
Breaching the 40px scroll threshold initiates a CSS matrix transition: the header's padding compresses, the Title shrinks, and all metadata arrays merge into a single `white-space: nowrap` horizontal flex-row.

### [REF: UI-66] Omni-Search Engine & LocalStorage Persistence
A dedicated memory-layer React Modal simultaneously queries all dataset parameters. A secondary state hook captures executed query strings to present a clickable "Recent Searches" history pool.

### [REF: UI-67] Minimalist Icon-Only Mode
Text labels are mathematically stripped from the Bottom Navigation Bar and Map HUD, leaving only clean, universally recognizable SVGs.

### [REF: UI-69] Ribbon Alignment & Telemetry Keep-Out Zones [NEW]
A fluid CSS spacer (`margin-left: auto`) is injected into the first metadata badge, forcing the Date to anchor permanently to the left, while instantly pushing all Tags and Places to the far right. Symmetrically, the Master Envelope inherently preserves the `padding-right: 55px` keep-out zone across both the Ribbon and Title containers, preventing metadata from bleeding into the top-right floating Maximize DOM node regardless of viewport stretch.

### [REF: UI-70] Map HUD Typography & Interaction Matrix
The isolated zoom controls utilize a vertical "Sandwich" flexbox column (`[+]`, `[14z]`, `[-]`), anchoring the focal integer directly between the action triggers.

### [REF: UI-71] Real-Time Layer Opacity Engine
When an overlay is toggled `Active`, the Layers HUD mounts an HTML `<input type="range">` slider. This slider is structurally decoupled from the `<label>` parent, allowing users to scrub the `L.tileLayer.setOpacity()` WebGL rendering in real-time.

### [REF: UI-72] Global Maximization Matrix
Utilizing global states (`maxPane` & `isTimelineExpanded`), the `AppOrchestrator` injects scoped CSS wrapper classes. This natively expands the active pane to `100% width/height` while safely unmounting sibling panes without destroying the virtual DOM.

### [REF: UI-86] The Drawer & FAB Synergy
Minimizing the timeline shrinks the container height to `0px`. To prevent Leaflet's WebGL context from crashing due to sudden container expansion, a CSS transition buffers the resize, giving the engine's `ResizeObserver` time to gracefully redraw the tiles. A Floating Action Button (FAB) dynamically mounts over the map to allow users to restore the timeline drawer.

### [REF: UI-87] The Android Bloat Fix (CSS Reset)
Mobile OS accessibility settings forcefully inflate typography, distorting UI buttons. To neutralize this, the app completely abandons Unicode emojis in favor of mathematically defined SVGs. Combined with `-webkit-appearance: none;` and hardcoded dimensions, the buttons are permanently immune to OS-level geometry distortion.

### [REF: UI-136] Absolute Pane Flex-Cages
To prevent high-resolution native imagery from forcing `.media-pane` bounds open and crushing the `.map-pane` to a `0x0` state, map wrappers are locked explicitly to `flex: 0 0 var(--secondary-split)` and hard-bounded with `min-height: 0; min-width: 0; flex-shrink: 0`.

### [REF: UI-139] The 270-Degree Back Vector
The Navigation Back button SVG arc relies on precise mathematical counter-clockwise tracing (`M 4 12 A 8 8 0 1 0 12 4`). This creates a mathematically perfect rewind visual queue, exposing only the top-right geometric quadrant.

### [REF: UI-142] Media Spotlight Casing
High-aspect ratio vertical media is decoupled from dark-mode black voids via a native CSS dot-matrix casing overlay (`radial-gradient(#333 1px, transparent 1px)`). An absolute-center soft white `radial-gradient` spotlight is applied to the image node container to separate media from the UI structure.

### [REF: UI-150] Layout Reset Engine
Prevents mobile users from structurally breaking the viewport. A core `Reset Layout` command executes a DOM override, instantly zero-stating all active pane variables back to the structural baseline (`55% / 50% / 10%`) and clearing active Maximize states.

### [REF: UI-156] Ascender/Descender Brand Typographic Locking
Inline `CarTiMapperLogo` SVGs are bound to an absolute vertical wrapper (`height: 22px`). This forces the `align-items: baseline` CSS directive to perfectly align the Logo ascender to the brand text descender.

### [REF: UI-159] Z-Index Layer Menu Liberation
Map and Visual panes explicitly utilize `overflow: visible; z-index: 30`, while Leaflet map tiles are isolated within a child node (`overflow: hidden; z-index: 1`). This architectural decoupling prevents Tablet viewports from clipping or decapitating the Map Overlay configuration menus.

### [REF: UI-177] Fluid Metadata Wrapping
Extinguished the restrictive `white-space: nowrap` horizontal cage on the `.metadata-ribbon`. Location strings displaying massive text values dynamically execute `flex-wrap: wrap`, gracefully stacking secondary labels (Tags) vertically to preserve absolute UX margins without horizontal clipping.

### [REF: UI-184] Pure CSS Legend Geometries
Cartographic legends must never rely on static image assets that drift out of sync with the application's CSS. The `AppOrchestrator` mathematically constructs the Legend Hub utilizing the exact same CSS geometries, clip-paths, and radial gradients used by the Leaflet engine and the Timeline Scrubber. This ensures the user's reference guide is a mathematically perfect reflection of the live DOM environment.

### [REF: UI-190] Semantic Cartographic Palette [NEW]
The engine strictly avoids using alert colors (Red) for baseline inactive data. The timeline adheres to a professional data-visualization palette:
*   **Active Focus:** Sapphire Blue (`#0066cc`) for primary focus and authority.
*   **Inactive Recession:** Slate Grey (`#78909C`) to enforce visual recession and reduce cognitive load.
*   **Temporal Approximations:** Burnt Amber (`#E65100`), guaranteeing >3:1 WCAG contrast against white backgrounds without requiring dark stroke casings.

### [REF: UI-193] White-Label Theme Expansion [NEW]
The engine strictly forbids hardcoded aesthetic opinions within the Virtual DOM. Auxiliary UI surfaces—specifically the Timeline Ribbon Floor, Tooltip Backgrounds, and Sub-pixel Heat-Shadows—are entirely decoupled into the `--tm-` CSS Custom Property matrix. This normalizes the architecture, allowing the ThemesT Database layer to control 100% of the application's visual footprint without requiring JavaScript recompilation.

### [REF: UI-195] Fluid Flex-Wrap Topology [NEW]
Rigid column percentages (e.g., a 70/30 split) violently fail when spatial parameters (multiple locations) exceed their container constraints. The `.metadata-ribbon` utilizes a Fluid Flex-Wrap architecture. The Date acts as the absolute left anchor (`flex-shrink: 0`). A `margin-left: auto` spacer propels the Places and Tags into a secondary right-aligned sub-container. This sub-container is authorized to `flex-wrap: wrap`, gracefully cascading multi-location pills downward without corrupting the primary header axis or forcing ugly string truncation.

### [REF: UI-199] Universal Button Topology & The Phantom Hitbox [NEW]
The engine strictly prohibits the use of invisible overlay divs for pagination, as they inherently battle the host OS's native scrollbars for Z-Index supremacy, resulting in Fitts's Law dead-zones. Instead, the UI enforces a Two-Tier Universal Button Topology:
*   **Tier 1 (Navigation/Pagination): 36x36px.** Deployed for critical, high-frequency actions (e.g., Content and Media carousel chevrons).
*   **Tier 2 (Utility/Toggles): 22x22px.** Deployed for secondary actions (Maximize, Settings) containing strictly mapped 14x14px SVG iconography. To preserve this compact 22px visual aesthetic without destroying mobile touch reliability, all Tier-2 `.status-btn` elements are wrapped in an invisible **Phantom Hitbox**. A CSS `::after` pseudo-element automatically projects an 8px invisible interactive bounding box beyond the visual perimeter of the button.

### [REF: MED-14] 404-Protected Clickable Metadata
To prevent relative-path 404 crashes, the Media Credit data payload is passed through an HTTP string-detector (`/^https?:\/\//i.test()`) before rendering. Valid external links are wrapped in target-blank anchor tags, while standard string attributions (e.g., "Public Domain") remain safely rendered as pure text. Media Captions are uniformly anchored to the active `currentCleanUrl`.

### [REF: MED-15] The Iframe Event-Swallow Failsafe (Chevron HUD)
Interactive media iframes (e.g., YouTube, PDFs, embedded WebGL maps) fundamentally swallow all touchstart and mousedown pointer events, neutralizing the application's native drag kinetics and scroll-snap features. To prevent users from becoming physically trapped on a slide, the MediaViewer deploys a Visible Chevron HUD. If an event contains an array of >1 media items, the engine explicitly mounts < and > navigation chevrons over the viewport at z-index: 1000. These buttons act as a structural escape hatch, executing `scrollTo()` coordinate jumps over the trapped context without deploying invisible "phantom dead zones" that would break the native interactivity of the iframe beneath.

### [REF: SEARCH-02] Advanced Normalization & Agnosticism (Search Engine)
To ensure a frictionless retrieval experience—especially critical for Polytonic Greek historical archives—the search indexer is explicitly decoupled from raw data strings. The AppOrchestrator utilizes a specialized `stripAndNormalize` regex closure. This engine sequentially: 1) Purges invisible HTML tags to prevent users from accidentally matching CSS classes or href attributes hidden in the dataset. 2) Executes NFD Unicode decomposition to mathematically separate base characters from their diacritics. 3) Strips the tonal markers (`/[̀-ͯ]/g`), enforcing a perfect case-and-accent-agnostic search matrix.

### [REF: UI-201c] Centered Click-Window Pattern [NEW - 2026-08-25] 
To bypass browser CORS/Clickjacking constraints when embedding third-party interactive media (such as YouTube iframes or PDF players), the media viewport swipe overlay must utilize a physical pass-through coordinate. Rather than using complex hover toggles, the system must deploy an absolute-centered window measuring 160px by 120px (top: 50%; left: 50%; transform: translate(-50%, -50%)) configured with pointer-events: none and carved out using a CSS clip-path polygon. This allows natural center clicks to fall through directly to the underlying media player, while the surrounding outer canvas boundaries retain pointer-events: auto to process swipe navigation gestures cleanly. Symmetrically, to prevent layout collisions, all media navigation chevrons are relocated to the bottom-left corner of the container (left: 16px; bottom: 12px;), and if a caption exists, a padding-left: 110px; is dynamically applied to the caption wrapper to prevent any visual overlapping.

**[REF: UI-164c] Symmetrical Status Cockpit [NEW]:** To maintain visual containment and support intuitive chronological scraping, all navigation controls must be clustered into a single, cohesive "Chronological Cockpit" at the absolute center of the viewport's status line. Grouping the incremental navigation triggers —Previous and Next— directly around the numeric record selector/counter prevents mouse-travel fatigue and locks the user's gaze to the active slide index. Telemetry and qualitative time span text must reside strictly to the right of the cockpit to prevent layout overlap on narrower mobile viewports.

### [REF: UI-46] Symmetrical Left Action Cluster & Standalone Taskbar Actions [UPDATED]
Secondary utility tools —Settings and Telemetry— are completely decoupled from popover navigation containers. Standalone action triggers reside directly within the left-hand status bar vector alongside the About logo. This flat visual layout optimizes Fitts’s Law on touch devices by eliminating nested click targets, securing rapid, zero-friction interface configuration.

### [REF: UI-164c] Symmetrical Status Cockpit [NEW]
To maintain visual containment and support intuitive chronological scraping, all navigation controls must be clustered into a single, cohesive “Chronological Cockpit” at the absolute center of the viewport's status line. Grouping the incremental navigation triggers —Previous and Next— directly around the numeric record selector/counter prevents mouse-travel fatigue and locks the user's gaze to the active slide index. Telemetry and qualitative time span text must reside strictly to the right of the cockpit to prevent layout overlap on narrower mobile viewports.

### [REF: UI-164d] Proportional Logo Constraints [NEW]
To preserve brand geometry across variable screen sizes, inline logo assets are strictly scaled using proportional height boundaries. Inside the 32px global status bar wrapper, the compass icon is locked to a physical height of 24px with the width calculated automatically. This structural layout choice establishes a symmetrical 4px top and bottom margin, keeping the logo nested cleanly within the taskbar while preventing geometric aspect ratio distortion.

**[REF: UI-164c] Symmetrical Status Cockpit [UPDATED]:**
To maintain visual containment and support intuitive chronological scraping, all navigation controls must be clustered into a single, cohesive "Chronological Cockpit" at the absolute center of the viewport's status line. Grouping the incremental navigation triggers —Previous and Next— directly around the numeric record selector/counter prevents mouse-travel fatigue and locks the user's gaze to the active slide index. Telemetry and qualitative time span text must reside strictly to the right of the cockpit to prevent layout overlap on narrower mobile viewports.

**[REF: UI-164d] Proportional Logo Constraints [NEW]:**
To preserve brand geometry across variable screen sizes, inline logo assets are strictly scaled using proportional height boundaries. Inside the 32px global status bar wrapper, the compass icon is locked to a physical height of 24px with the width calculated automatically. This structural layout choice establishes a symmetrical 4px top and bottom margin, keeping the logo nested cleanly within the taskbar while preventing geometric aspect ratio distortion.

**[REF: UI-164c] Symmetrical Status Cockpit [UPDATED]:** To maintain visual containment and support intuitive chronological scraping, all navigation controls must be clustered into a single, cohesive "Chronological Cockpit" at the absolute center of the viewport's status line. Grouping the incremental navigation triggers —Previous and Next— directly around the numeric record selector/counter prevents mouse-travel fatigue and locks the user's gaze to the active slide index. Telemetry and qualitative time span text must reside strictly to the right of the cockpit to prevent layout overlap on narrower mobile viewports.

**[REF: UI-164d] Proportional Logo Constraints [NEW]:** To preserve brand geometry across variable screen sizes, inline logo assets are strictly scaled using proportional height boundaries. Inside the 32px global status bar wrapper, the compass icon is locked to a physical height of 24px with the width calculated automatically. This structural layout choice establishes a symmetrical 4px top and bottom margin, keeping the logo nested cleanly within the taskbar while preventing geometric aspect ratio distortion.

    [REF: DATE-12] Strict Serial date containment: Prevents string dates with leading digits from being parsed as serial float numbers, protecting Gregorian fallbacks.
    [REF: UI-199c] Center Cockpit Navigation: Centers Prev, Input, and Next buttons, locking pagination coordinates.
    [REF: UI-201b] Minimap Gutter Scale Clearance: Sets minimap coordinates to bottom: 55px, freeing up the Leaflet bottom-left scale bar vertical clearance.

---

## 5. Timeline Physics & Chronological Mathematics <a name="category-5"></a>

### [REF: TL-01] Intelligent Time Rendering Range
The timeline automatically buffers raw dataset time edges with a 5% chronological margin (`padMs = rawTimeRange * 0.05`), generating aesthetically pleasing spatial breathing room for the first and last graphical event nodes.

### [REF: TL-02] Dynamic Timeline Swimlane Math
The timeline iterates through dataset tags to generate a mathematical constant `laneCount`. It binds `orderedTags.indexOf(tag)` to dynamically calculate specific Y-axis placement constraints, enforcing pure chronological collision prevention.

### [REF: TL-13] Hexagon Arrow Typographic Envelope
Event geometry eschews standard square nodes for an absolute CSS geometric `clip-path` (`polygon(0 calc(50% - 12px), ...)`). This allows the block to expand infinitely downward to accept 3-line text wrapping while structurally guaranteeing the left-facing directional chevron remains perfectly aligned and never shears into a parallelogram.

### [REF: TL-14] Drop-Line Vertical Pinning
Volatile JavaScript vertical pixel tracking is deprecated. The `.event-group` parent is anchored securely above the X-Axis track via `bottom: 28px`. The active indicator line simply utilizes `height: ${containerHeight - 28 - topPos - (blockHeight / 2)}px;`, tracing an indestructible line straight down from the geometric center of the active hexagon node to the X-Axis plane.

### [REF: TL-15] Semantic Timeline Spans
Active UI span counters auto-convert abstract millisecond variables to human-readable strings (Minutes, Hours, Days, Years) based on real-time scroll zoom coefficients.

### [REF: TL-16] Smart Chronology Formatting
To optimize spatial density, labels employ real-time string deduplication arrays: rendering Year for multi-year spans, `DD/MM/YYYY` strings for intermediate spans, and `HH:mm` clock arrays for intra-day zooms.

### [REF: TL-18] Z-Stacking Density Engine
The rendering loop utilizes an $O(1)$ memory registry (`stackRegistry`) to intercept concurrent chronological events. It generates a strict mathematically bound key (`${timestamp}_${laneIndex}`). When multiple geometries attempt to render on the exact same `X, Y` coordinates, the engine mathematically fans them out via sequential CSS `calc()` offsets (`+6px` horizontally, `+4px` vertically). This prevents geometric eclipsing and immediately communicates deep historical density at granular zoom levels.

### [REF: TL-19] 4D Telemetry Hoisting
The Timeline Scrubber passively calculates and broadcasts its absolute chronological viewport boundaries (`[visibleLeftMs, visibleRightMs]`) back to the global AppOrchestrator state. This telemetry pipeline forms the backbone of the Map's temporal intersection algorithms.

### [REF: TL-20] The 8px/4px Stepped Trapezoid (Duration Overlaps) [UPDATED]
To solve the physical overlapping of event duration spans, the timeline `xAxisMarker` utilizes a Stepped Orthogonal Trapezoid (`clip-path: polygon(0 0, 100% 4px, 100% 100%, 0 100%)`). All spans deploy a sharp `border-left: 2px solid`. When Event B physically overlays Event A, Event B's 8px leading border completely eclipses Event A's 4px tail, creating a distinct geometric "step" that demarcates the new event without incurring any vertical `laneHeight` penalty. The engine applies `mix-blend-mode: multiply` to these markers, generating a unified, high-contrast heat-map band along the bottom 4px track.
*   **EDTF Integration:** If the chronological start or end boundaries are flagged as approximate via the EDTF engine, the corresponding geometric edge overrides the standard boundary and renders a rigid 3px solid #ffb300 (Gold) line paired with a native OS cursor: zoom-in. This geometrically flags the uncertainty while signaling the user to trigger the [REF: PERF-33] auto-zoom camera behavior.

### [REF: TL-22] Full-Matrix Tag Adjacency Algorithm [NEW]
To prevent `.event-block` wrappers from vertically ballooning across unassociated lanes, the `orderedTags` generator rejects linear parsing in favor of full-matrix combinatorial extraction. During ingest, the engine executes a nested for-in-for loop across every event's tag array. This registers every possible intra-event relationship (e.g., A-B, A-C, B-C), enabling the sorting graph to perfectly cluster related `laneHeight` blocks and minimize vertical rendering waste.

### [REF: TL-24] Interaction-Time Intersection (Lazy Tooltips) [NEW]
To solve the Identity Crisis of long, overlapping ribbons without calculating $O(N^2)$ matrices on render, the engine utilizes Lazy Evaluation. A hover-bridge-hitbox initiates a 400ms `setTimeout`. If the pointer lingers, the engine intercepts the active ID, maps its `startDate.min` and `endDate.max`, and filters the entire dataset for temporal collisions. It then natively renders a custom UI tooltip detailing the hovered event and listing all intersecting titles.

### [REF: TL-26] The Modulo-Pattern Matrix [NEW]
To preserve distinct visual identities when multiple Ghost Calipers stack vertically, the engine applies a mathematical Modulo array index against the stackDepth coefficient (`stackDepth % 3`). This loop maps styling directives asynchronously, forcing stacked ribbons to automatically rotate through `['solid', 'dashed', 'dotted']` border properties and `['45deg', '-45deg', '90deg']` geometric repeating gradients.

### [REF: TL-27] The Spatial Anchor Pattern [NEW]
To eliminate the `xOffset` "Chronological Drift" bug, the `.event-group` wrapper acts as a rigid, unmoving Cartesian anchor (`left: ${startPct}%`). All mathematical intersection geometry (the 2px drop-line, the duration trapezoid, the hover bridge) are declared at `left: 0`, guaranteeing absolute alignment with the X-Axis ruler. Only the typographic child node (`.event-block`) receives the `xOffset` CSS displacement, preventing narrative collisions without corrupting the underlying physics.

### [REF: TL-28] Floorless Woven Matrix & Segmented Rhythm [NEW]
To eliminate the jagged DOM intersections of "Mini-Lanes", all inactive ribbons are permanently anchored to `bottom: 0` and stripped of their horizontal `border-bottom`. Styling relies entirely on a deterministic `startDate` Modulo index. The engine scans `validData` to build an ordered `uniqueStarts` array. The chronological index dictates the `hatchAngles` array, ensuring perfectly synchronous events receive identical styling. To prevent solid geometry from overwhelming the `mix-blend-mode` layer, the engine injects a fixed-pixel `-webkit-mask-image: repeating-linear-gradient` over the element. This instructs the GPU to render a strict geometric rhythm (70px painted, 30px erased) across the X-Axis, preserving visual clarity regardless of extreme variations in zoom level or total duration length.

### [REF: TL-30] Weighted Gravity Swimlane Matrix [NEW]
To prevent typographic crowding near the X-Axis and intelligently cluster adjacent event types, the timeline swimlanes utilize an $O(N^2)$ Weighted Gravity Sort. The ingestion loop computes a `tagFreq` tally and a `pairFreq` associative dictionary. The algorithm places the absolute most frequent tag at the top of the container (`laneIdx = 0`), ensuring its highly-trafficked drop-lines receive maximum vertical runway. The loop calculates the strongest paired connection (`(pairWeight * 1000) + baseFreq`) to map subsequent adjacent lanes. This deterministic algorithm inherently pushes orphaned or isolated tags to the lowest `laneIdx`. Because the bottom lane rests just 14px above the X-Axis, populating it with the rarest elements mathematically minimizes visual stutter and prevents line collisions.

### [REF: TL-31] True Cartesian Anchoring [NEW]
To eliminate the "Barcode Effect" caused by the `stackDepth` integer pushing the entire `.event-group` off its absolute chronological point, the timeline enforces strict geometric decoupling. The `.event-group` wrapper acts as an immutable Cartesian anchor (`left: ${startPct}%`). All mathematical intersection geometry (the 2px drop-line, the duration trapezoid) are declared at `left: 0`, guaranteeing absolute alignment with the X-Axis ruler. Only the typographic child node (`.event-block`) receives the `labelXOffset` CSS displacement, ensuring narrative collision prevention without corrupting the underlying physics.

### [REF: TL-35] Luminous Shadow Matrix (Anti-Mud) [NEW]
Applying a sub-pixel box-shadow (Matte Glow) using the exact identical base color of an element creates "mud," thickening the line optically rather than simulating light radiation. The Timeline's Chronological Heat-Glow explicitly utilizes a *Luminous Shadow Matrix* (a distinct CSS RGB array with a higher luminosity counterpart, e.g., Soft Cyan for Sapphire Blue). This preserves the razor-sharp 2px core line while generating a correct, soft sub-pixel bloom where events cluster.

### [REF: MAP-12] EDTF Quantum Evaluation
Map native chronological intersections explicitly bypass linear start/end duration checks if an EDTF `Set` or `List` object is detected. Instead, the engine dynamically loops through the disjointed dates within the `edtf.values` array and checks if the visible timeline intersects *any* discrete temporal node. This allows quantum (flashing) marker visibility over highly fragmented historical timelines without requiring the spreadsheet to hardcode separate database rows.

### [REF: PERF-28] Axes Density Throttle [NEW]
Limits maximum Major Tick visual density to 6-12 occurrences per screen width (anchoring standard ticks roughly every 120 pixels). Scale-down triggers are defined explicitly via `minorCount`, strictly enforcing 5-12 minor ticks within every active chronological block.

### [REF: PERF-29] One-Indexed Monthly Drift Protection [NEW]
Forces Javascript chronological math strings to operate on `getDate() - 1` architecture. This geometrically bounds date stepping limits, eliminating zero-indexed drift anomalies and securely forcing monthly and yearly Major Ticks to render flawlessly on the '1st' of their respective calendar periods.

### [REF: PERF-34] Concurrent Priority Sorting
Sub-second accuracy is strictly parsed. Concurrent events sharing the exact same millisecond start time utilize a secondary fallback to their original Spreadsheet Row ID, guaranteeing stable, non-volatile natural order rendering.

### [REF: PERF-41] Kinetic Camera Orchestrator (Time-to-Pixel Binding) [UPDATED]
To solve "Layout Thrashing" and erratic bounce during timeline magnification shifts, the camera physics strictly decouple the mathematical domain (Time) from the physical range (Pixels). The `activeIndex` loop utilizes a `scrollTargetPayloadRef` to cache the target absolute global index or a custom manual-zoom payload. The engine calculates and applies the new `zoomLevel`, forcing the Virtual DOM to morph the container width. An intercepting `useLayoutEffect` detects the width change and invokes [REF: PERF-42] Exact Node Geometry Sub-Pixel Math to mathematically convert Time into Pixels and instantly snap the scroll-bar synchronously to center-mass *before* the browser is allowed to paint the frame.

### [REF: PERF-42] Exact Node Geometry Sub-Pixel Math [NEW]
To prevent "Concurrent Chronology" targeting errors (where multiple events share an identical timestamp and push each other horizontally via the [REF: TL-18] Z-Stacking Engine), the timeline camera never relies on raw timestamps. The `getExactNodeScrollPos()` algorithm specifically intercepts the target Node ID, mathematically re-calculates the local Z-Stack sequence to obtain the exact `xOffset`, extracts the exact `pxWidth` of the string label, and computes the absolute Cartesian pixel coordinate of the node's geometric center. This guarantees flawless camera tracking and prevents the [REF: PERF-40] DOM culler from accidentally deleting off-center active elements during extreme auto-zooms.

### [REF: PERF-43] Active-Only Duration Clamp [NEW]
The 5-Node Kinetic Camera radar is bifurcated to prevent peripheral "Duration Bleed." While evaluating the 5-node cluster, the `[i]` iteration loop strictly observes `startDate.min` to build the required horizontal graphical padding. The engine explicitly reads the `endDate.max` exclusively for the `activeDataIndex` target node. This guarantees that clicking a 10-minute micro-event nested within a 1-month macro-event forces the camera to snap deep into the 10-minute topology.

### [REF: UI-154] Intelligent Contextual Maximize
The Maximize trigger explicitly rejects rigid viewport-takeovers. It evaluates the exact data footprint (`timelineRequiredHeight = (laneCount * 24) + 40`). Engaging Maximize snaps the drawer height strictly to this pixel matrix, structurally revealing all active swimlanes with zero pixel waste.

### [REF: UI-164] Two-Pass Center-Mass Overlap Suppression (Updated)
1.  *Pass 1:* Isolates raw plotting coordinates.
2.  *Pass 2:* Identifies the single Major Tick mathematically closest to the absolute center of the viewport and assigns the Full Date label. A `65px` keepout radius suppresses adjacent label strings, generating a geometric typography void that guarantees zero overlap.

### [REF: UI-165] Declutter Modulo Masks
Physical minor tick geometry rendering (the 1px indicator line) runs unconditionally, while semantic text values execute heavily restricted Modulo arrays. Even density scales use `% 2 === 0` loops to alternating text tags, while odd scale counts limit text rendering explicitly to the absolute median array instance.

### [REF: UI-167] Contextual Truncation Math (Updated)
Decoupled physical sub-ticks (`1px` width) from typography. Minute scales dynamically truncate leading hours (`:15`, `:30`), and contextual overrides ensure daily context (e.g., `12 May`) forces replacement of `00h` markers when zooming out horizontally past a 24-hour span.

### [REF: UI-185] Magnetic Hover Text (Pure CSS)
To circumvent the CPU cost of mathematically recalculating long-string widths during viewport scaling, the engine utilizes a pure CSS override state (`.event-block:hover { width: max-content !important; z-index: 40 !important; }`). When a user hovers over an elided string (e.g. *The British and...*), the hexagon block temporarily breaks its structural cage, magnetically snapping open to its full width and casting a shadow over adjacent sibling nodes.

### [REF: UI-188] Asymmetrical Hit-Boxes [NEW]
To protect Fitts's Law on touch devices, the CSS `clip-path` bounding the Ghost Calipers is decoupled from interactive listeners. An invisible sibling node (`.hover-bridge-hitbox`) handles the `onMouseEnter` logic. This node is uniquely biased downwards (`bottom: -15px`), pushing the interaction target safely past the `.event-block` typography and directly into the dead-space of the 28px X-Axis timeline track.

### [REF: TL-18b] Viewport-Center HUD Button Fallback [NEW - 2026-08-25]: 
To prevent vertical axis and layout scroll-snapping errors during timeline scaling shifts, the timeline scroll system must distinguish between slide-initiated autofocus events and manual scale modifications. Manual zoom triggers (mouse wheel, touchpad pinches, or HUD zoom buttons) must explicitly reject snapping to the active slide index. For cursor wheel zooms (onWheel), the exact timeline time under the cursor (eventX) must be captured and centered in the viewport post-zoom. For manual HUD buttons (center zooms), the current visual midpoint of the screen (containerW / 2) serves as the mathematical anchor, applying the scale transform, and adjusting scrollLeft to snap the identical time coordinate back to the center of the viewport, preserving the user's focus.

### [REF: MAP-12b] Granular Wave-Date Dimming (Quantum Sets) [NEW - 2026-08-25]: 
To support micro-chronological geographic modeling—such as military or diplomatic forces arriving in distinct waves inside an inclusive EDTF Set or List {}—the mapping engine must decouple coordinate highlights from slide-level states. During data ingestion, the engine maps the individual elements of a Set/List of dates 1:1 to the individual features in the coordinate geometry, caching the specific date limit onto each Leaflet layer object as layerDate. During active timeline scrubbing, the temporal filter loops through each layer of the active slide. Any layer whose cached layerDate intersects the scrubber viewport bounds receives 100% opacity, while layers representing future or past dates are attenuated to 20% opacity (Temporal Ghosting), allowing the map to physically animate strategic spatial expansions on the fly.

**[REF: BOOT-CRASH-03b] Character Class Escaping and Hyphen Bounds:**
To isolate the regular expression engine from unexpected system encodings or polytonic Greek character overlaps, all hyphens (-) utilized inside active split arrays (places, sublabels, dates) must be explicitly escaped as \- or anchored to the absolute far-right boundary of the bracket. Ingesting unescaped hyphens in the middle of character classes (e.g., [\\/\\\\-.]) forces the browser to evaluate character ranges based on ASCII codes. If the character preceding the hyphen holds a higher decimal value than the trailing character, the JS compiler immediately throws a fatal "invalid range in character class" SyntaxError, blocking the Preact boot sequence.

#### [REF: CRASH-05b] Nested Template Literal Syntax Guard [UPDATED - 2026-08-30]
Dynamic rendering variables passed to hoisted Preact layouts (`appLayout`) must strictly avoid nested backtick structures (e.g., `` `\${height}px` `` inside `html` tag literals). Lexical parsers in standard browser V8 engines interpret inner backticks as template closures, prematurely terminating the parent literal and triggering fatal syntax errors. All variable property calculations must utilize standard JavaScript string concatenation (e.g., `height + 'px'`) to maintain single-file compilation integrity.

---

## 6. Algorithms, Analytics & Methodologies <a name="category-6"></a>

### 1. Spatial Indexing (The R-Tree Engine)
`MarkerCluster` uses `RBush` to divide the map into nested rectangular grids. It measures point-to-grid, allowing instant, $O(\log n)$ collision detection.

### 2. State-Based Layer Swapping & The O(1) Dictionary
To bypass Leaflet's internal `_leaflet_id` amnesia, the engine builds a global dictionary (`markersRef`). Slide changes execute an $O(1)$ instant lookup to swap layers in and out of the cluster group seamlessly.

### 3. The Dual-Heuristic Density Math (Timeline Auto-Zoom)
Evaluates two vectors: `collisionZoom` (The 10px Rule for preventing overlap on the same lane) and `contextZoom` (The 150px Rule for keeping the nearest event visible). Executes `Math.max()` to adopt the safest zoom.

### 4. The URL Routing Engine [REF: URL-01]
Intercepts CLI/URL parameters. `?date=` executes a mathematical distance calculation across the array to locate the closest absolute time-node. `?slide=X` overrides chronology. `?theme=dark` manipulates root CSS properties prior to physical DOM render. `getOmniParam()` sanitizes `amp;` corruptions natively and falls back to Hash Routing ensuring 100% deep-link execution parity.

### 5. The Visual-Center Scrolling Algorithm
Calculates `blockPixelWidth` dynamically. Plots the geometric center (`StartPx + Width/2`). Commands the scrollbar to target `visualCenterPx - (Screen Width / 2)` to perfectly center wide text blocks.

### 6. HTML Filter Bifurcation
Timeline Hexagons are processed through `stripHTML()` to guarantee layout breaks (`<br>`) do not physically break geometric rendering. Content Pane Titles are processed through `dangerouslySetInnerHTML` to permit manual formatting.

---

## 7. System Stability & Error Boundaries <a name="category-7"></a>

### [REF: BOOT-CRASH-01] Boot Safety Validation
To prevent fatal unrecoverable blank screens, all Native JS constructors (`new URLSearchParams`) must be strictly validated against syntax typos prior to React's first render hook.

### [REF: BOOT-CRASH-02] Spatial Array Integrity & The 't is null' Loop
Leaflet's camera (`setView`) and boundary calculations (`fitBounds`, `getCenter()`) are mathematically brittle. If fed a truncated integer, `NaN`, or an empty value instead of a strict `[Lat, Lon]` array, the engine returns `null`. This instantly triggers a fatal `TypeError: can't access property "lat", t is null` when the Minimap attempts to synchronize its camera to the Main Map. All spatial configurations (`iconSize`, `iconAnchor`, `offset`, `padding`) must permanently maintain rigid `[x, y]` pixel array structures to prevent cascading DOM failure.

### [REF: TL-CLAMP-01] Span Geometry Clamp
The Timeline Scrubber must strictly enforce a minimum temporal visual width of 24 hours (`86400000` ms) to prevent `0px` layout collapse in single-event datasets.

### [REF: TL-CLAMP-02] Infinity Geometry Clamp
The Timeline Scrubber's automatic scaling math must enforce a strict `60000` ms floor on event time gaps to mathematically ensure the engine never divides by zero.

### [REF: DIAG-01] Active Sensor Telemetry
The Vibe Monitor passively exposes the application version manifest and the raw location string of the currently active dataset row.

### [REF: DIAG-03] Exact Millisecond Diagnostics
Abolished string sanitization inside the diagnostic readout. Telemetry for `startDate` and `endDate` fields yields strict, high-fidelity ISO payloads (`val.toISOString()`), empowering precise validation of chronological offsets and millisecond-level Standardised Chronological Increments (SCIs) to diagnose slide de-synchronization.

### [REF: DIAG-04] Omni-Directional Telemetry Scaling & DOM State Anchoring
Telemetry windows natively support manual fluid scaling (`resize: both; overflow: hidden;`) via OS-level border dragging. To prevent the Virtual DOM from resetting manual user dimensions during coordinate translation, the `onMouseDown` drag event polls the physical DOM via `getBoundingClientRect()`. It locks the exact physical dimensions into a React `size` state, rendering the window immune to layout collapse during drag-and-drop. Intercepts timeline geometry states to mathematically drop the monitor exactly `15px` above the global status bar on the left flank, avoiding center-screen occlusion.

### [REF: CRASH-01] Library Polyfill Injection
The `MapViewer` implements a native string-interception polyfill that explicitly deconstructs `GEOMETRYCOLLECTION` wrappers and passes isolated internal primitives through the parser.

### [REF: CRASH-02] React Prop Continuity
Cross-component navigational functions (e.g., `jumpToSlide`) must be explicitly passed via React component props to prevent fatal unrecoverable `ReferenceError`s inside isolated Modals.

### [REF: CRASH-03] HTM/Preact Parser Collision Prevention
The engine strictly forbids the use of standard React pseudo-comments (`{/* comment */}`) inside HTM template literals (`html\``). The parser misinterprets these as literal text nodes, generating invisible DOM elements that shatter layout geometry and create phantom background overflow.

### [REF: CRASH-06] The TouchList Prototype Trap [NEW]
When intercepting mobile hardware telemetry (touch events), the engine must never utilize modern Array prototype methods (like `.at()`) on `e.touches` or `e.changedTouches`. These properties return a `TouchList` DOM interface, not an Array. Attempting to use `.at()` will trigger a fatal `TypeError`, instantly paralyzing mobile interactivity. All touch coordinate extractions must rely exclusively on raw bracket notation (e.g., `e.changedTouches[0].screenX` or standard DOM properties).

### [REF: CRASH-07] Bracket Stripping Immunity [NEW]
During string parsing and extraction loops inside the Virtual DOM, the engine must actively avoid utilizing static numeric bracket accessors (like `[0]`) to retrieve first-elements from arrays or DOM nodes. To guarantee the code physically survives text-stripping transmission pipelines (where `[0]` may be mistaken for a citation or markdown tag), the engine must utilize native traversal methods: `.shift()` for extracting the first string from an Array, and `.item(0)` for extracting the primary Cartesian object from a DOM `TouchList`.

[REF: PROT-15] Semantic Version Gating & Compiler Escape Armor [NEW]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Furthermore, to prevent unescaped regular expressions or backslashes nested within the Javascript codeblocks from crashing the compiler, all string substitutions inside the Python regex engine must run through a callable replacement function to be parsed as raw text.

[REF: PROT-15] Semantic Version Gating & Compiler Escape Armor (v1.1.4) [UPDATED]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Symmetrically, to prevent unescaped regular expressions or backslashes nested within the Javascript codeblocks from crashing the compiler, all string substitutions inside the Python regex engine must run through a callable replacement function to be parsed as raw text. To ensure complete immunity against carriage returns, variable spaces, or custom alpha/beta version tags (e.g. v6.4.5_live or v11α5) inside the monolithic HTML template, the compiler searches for component boundaries using a space-and-bracket-insensitive wildcard block (([^\s\]]+)), mapping the files symmetrically regardless of typographical drift.

[REF: PROT-15] Semantic Version Gating & Compiler Escape Armor (v1.1.5) [UPDATED]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Symmetrically, the script replaces component payloads using a callable replacement callback that preserves the closing END_INJECT comment via the fourth matched group (m_match.group(4)), preventing duplicate blocks or orphaned characters. To ensure complete immunity against carriage returns, variable spaces, or custom alpha/beta version tags (e.g. v6.4.5_live or v11α5) inside the monolithic HTML template, the compiler searches for component boundaries using a space-and-bracket-insensitive wildcard block (([^\s\]]+)), mapping the files symmetrically regardless of typographical drift.

[REF: PROT-15] Boundary Self-Healing & Compiler Escape Armor (v1.1.7) [UPDATED]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Symmetrically, the script replaces component payloads using a callable replacement callback that preserves the closing END_INJECT comment via the fourth matched group (m_match.group(4)), preventing duplicate blocks or orphaned characters. To recover from corrupt target files, the compiler runs a pre-flight self-healing routine: if a component possesses a start anchor but is missing a closing anchor, the script scans forward, locates the next component's starting boundary or closing </script> tag, and reconstructs the missing END_INJECT comment block in-place on the user's filesystem prior to compilation.

[REF: PROT-15] Boundary Self-Healing & Compiler Escape Armor (v1.1.7) [UPDATED]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Symmetrically, the script replaces component payloads using a callable replacement callback that preserves the closing END_INJECT comment via the fourth matched group (m_match.group(4)), preventing duplicate blocks or orphaned characters. To recover from corrupt target files, the compiler runs a pre-flight self-healing routine: if a component possesses a start anchor but is missing a closing anchor, the script scans forward, locates the next component's starting boundary or closing </script> tag, and reconstructs the missing END_INJECT comment block in-place on the user's filesystem prior to compilation.

[REF: PROT-15] Boundary Self-Healing & Compiler Escape Armor [UPDATED - 2026-08-29]
The local Dev/Ops compilation script (compile_cartimap.py) must protect git repository history by executing minimal delta-only updates. The compiler extracts semantic version strings from component injection headers (START_INJECT) and converts them to integer tuples. Overwriting a target component is strictly prohibited unless the patch's version is mathematically greater than the version inside the target HTML. Symmetrically, the script replaces component payloads using a callable replacement callback that preserves the closing END_INJECT comment via the fourth matched group (m_match.group(4)), preventing duplicate blocks or orphaned characters. To recover from corrupt target files, the compiler runs a pre-flight self-healing routine: if a component possesses a start anchor but is missing a closing anchor, the script scans forward, locates the next component's starting boundary or closing </script> tag, and reconstructs the missing END_INJECT comment block in-place on the user's filesystem prior to compilation.

---

## 8. Grid Topology & Stacking Domination <a name="category-8"></a>

### [REF: UI-175] Global Beam Architecture
Extracted the Nav/Status UI (`.unified-status-bar`) from the nested narrative pane. Re-engineered it as a static 32px horizontal structural beam (`#app-layout > .global-status-bar`) separating the Core Viewports from the Timeline Scrubber. This guarantees the UI floor permanently survives visual pane maximizations.

*   **[REF: UI-83] Absolute Utility Margin Offsets [UPDATED]:** The floating control toolbar (`Maximize` and `Open Source File [↗]`) inside the Media Viewer is absolute-positioned at `top: 60px; right: 60px`. This horizontal translation provides a strict 60px safe margin that isolates our UI elements from native browser scrollbars and inline iframe toolbars.
*   **[REF: UI-84] Bottom-Center Navigation HUD [NEW]:** To eliminate vertical side-edge clutter over maps and images, multiple-media slides display a consolidated, central navigation bubble absolute-positioned at `bottom: 65px; left: 50%; transform: translateX(-50%)`. This groups chevrons and counter indicators into a compact tap zone while clearing bottom-aligned iframe menu overlays.

#### [REF: UI-340] Sorted Search State Inversion [NEW - 2026-08-29]
When the user queries the database index via the Search Modal, the action list returns matching records based on original row indexes (`res.id`). Symmetrically, because the active viewport stage presents a chronologically sorted and tag-filtered subset of records, directly jumping to an absolute index `id` creates an index-drift regression. To eliminate this drift, the modal click handler must execute a mathematical state inversion inside the active state registry: `data.findIndex(d => d.id === id)`. This retrieves the correct sorted target position, guaranteeing that the Stage, Map, and Scrubber focus on the exact intended historical node.

#### [REF: CRASH-05b] Template Literal Decoupling & Isolation [NEW - 2026-08-29]
To prevent fatal browser-level parsing errors (SyntaxError: unexpected token: identifier), any complex conditional HTML element containing template strings must be decoupled from the core JSX template rendering stream. Tagged template expressions (e.g., `html\`...\``) nested deeply within larger template interpolation blocks (`\${...}`) can trigger lexical collisions in browser engines when interpreted in a single-file environment. By compiling the sub-component into an independent state variable (such as `downloadBtn`) before the core JSX return declaration, the parsing contexts are strictly separated, securing 100% engine stability and cross-viewport compatibility.

#### [REF: CRASH-05b] Hoisted Variable Isolation & Escaping [UPDATED - 2026-08-29]
To completely insulate the Preact Virtual DOM from browser-level lexer crashes (e.g., SyntaxError: unexpected token: identifier), nesting conditional template strings (such as html`...`) inside the main return block's JSX placeholders is strictly deprecated. Deep-nesting triggers catastrophic compiler collisions when parsed client-side in a monolithic file. All conditional or complex HTML elements must be extracted and declared as independent JS constants (e.g., downloadBtn, backBtn, prevBtn) *above* the core JSX render stream. This physical decoupling isolates the string parsing contexts, securing 100% engine stability and maintaining a deterministic constant-time render frame.

---

### ## 9. System Stability & Error Boundaries ↓↓

*   **[REF: BOOT-CRASH-03] Character Class Range Bounds & Escaping [NEW]:** All regular expression character classes ([...]) containing literal dashes (-) or backslashes (\) must strictly escape these tokens to isolate them from range operators. Slashes (/) inside RegExp literals must be escaped as \/. Literal dashes must be positioned at the absolute end of the class (e.g., /[\/\\.-]/) or escaped as \- to prevent the JavaScript engine from evaluating ASCII character ranges and throwing fatal SyntaxError exceptions on boot.

*   **[REF: BOOT-CRASH-03] Character Class Escape Parity [NEW]:** To maintain strict-mode execution compliance inside ES module runtimes, all literal string-splitting regular expressions containing forward slashes (/) or backslashes (\) must explicitly escape these characters (e.g., `[\/\\.-]`). Failure to escape forward slashes inside bracket classes causes the lexical engine to interpret the token as a closing delimiter, dumping naked escape sequences into the global execution thread and triggering fatal compiler-level halts.

**[REF: BOOT-CRASH-03] State Initializer Syntax Isolation:**
To prevent fatal compilation exceptions —(κατάρρευση μεταγλώττισης)— during 
automated code serialization, pipeline template merges, or human code styling, 
all JavaScript state initialization code sitting outside string or template 
literals must pass a strict lexical validation gate. Developers and generator 
scripts are strictly prohibited from utilizing raw backslashes or unquoted 
escape sequences —such as literal "\n" characters— in active execution lanes. 
All physical carriage returns must rely on native, hardware-level line breaks 
to preserve absolute cross-browser portability and ensure offline Preact 
reconciliation stability.

#### [REF: CRASH-05b] Zero-Nesting Decoupled Architecture [UPDATED - 2026-08-29]
To permanently insulate the Preact Virtual DOM from browser-level lexer crashes (such as `unexpected token: identifier`), deep-nesting conditional template strings (`html`...`) inside the main return block's JSX placeholders is strictly prohibited. Low-spec browser engines frequently fail to balance backticks nested within placeholders. Symmetrically, all conditional blocks, modals, loops, and button text segments must be hoisted and resolved into independent JavaScript constants *prior* to the main return statement. The final JSX stream must only interpolate flat variables (e.g., `${loadingScreen}`, `${appLayout}`), securing 100% engine stability and ensuring clean execution across restricted mobile devices and field tablets.

#### [REF: CRASH-05b] Nested Template Literal Escaping [NEW - 2026-08-29]
To prevent fatal browser compilation crashes (SyntaxError: unexpected token: identifier), any secondary Preact html template string nested inside the main App component's return literal must explicitly escape its backticks using backslashes (\`). If unescaped, the browser's parser interprets the first nested backtick as the termination of the outer template literal, forcing the following HTML markup to parse as raw JavaScript execution code. This instantly breaks the document thread, preventing the Virtual DOM from mounting. Escaping nested backticks isolates the inner arrays, securing 100% rendering stability.

### ## 9. System Stability & Error Boundaries / 2. Initialization Safety

*   **[REF: CRASH-08b] Structural Tag Alignment [NEW]:** To guarantee the integrity of zero-build Virtual DOM engines executing in standalone HTML viewports, any global component renaming (e.g., VibeMonitor to TelemetryMonitor) must be applied synchronously across all layout constructor tags. Discrepancies between element definitions and Virtual DOM rendering templates bypass the standard Preact ErrorBoundary and trigger fatal, unhandled ReferenceError interrupts during the initial DOM paint cycle, trapping the client's progress bar at the 10% boot-strap step.

#### ## 9. Core System Stability / 2. Parser Error Boundaries ↓↓

*   **[REF: BOOT-CRASH-03] Character Class Escape Parity [UPDATED]:** Regular expression literals inside utility components must open with an unescaped forward slash (/) and escape any literal slashes within bracket classes (e.g., `[\/\\.-]`). If a leading slash is escaped or an inner slash is left unescaped, compile-time syntax errors cascade down the DOM tree.
*   **[REF: CRASH-07] Bracket Stripping Immunity [ENFORCED]:** Accessing first-elements inside array split loops must utilize `.at(0)` or `.shift()`. Standard bracket accessors (like ``) are banned within the core ingestion hooks to insulate strings against automatic bracket-stripping in markdown-based translation pipelines.

*   **[REF: BOOT-CRASH-03] Character Class Escape Parity [DEPRECATED]:** The string-splitting regex validation sequence in `parseChronoNode` is officially deprecated in favor of strict-schema float parsing.
*   **[REF: DATA-16] Native Float-to-Epoch Ingestion [NEW]:** To maintain low boot latency and eliminate strict-mode lexical parser collisions, the chronological engine reads legacy dates strictly as native Double-Precision Floats (`FLOAT8`). The parser casts the incoming PapaParse CSV tokens directly via `parseFloat` and converts the Google Sheets epoch offset (`25569`) to UNIX millisecond timestamps in a single constant-time \\(O(1)\\) computational step, safely discarding all string allocation overhead.

## ## 9. Core System Stability / Failsafes ↓↓

*   **[REF: BOOT-CRASH-03] Character Class Escape Parity [UPDATED]:** Regular expression literals inside utility components must open with an unescaped forward slash (/) and escape any literal slashes within bracket classes (e.g., `[\/\\.-]`). If a leading slash is escaped or an inner slash is left unescaped, compile-time syntax errors cascade down the DOM tree.
*   **[REF: CRASH-07] Bracket Stripping Immunity [ENFORCED]:** Accessing first-elements inside array split loops must utilize `.at(0)` or `.shift()`. Standard bracket accessors (like ``) are banned within the core ingestion hooks to insulate strings against automatic bracket-stripping in markdown-based translation pipelines.



## 11. Media Playback & Camera Focus Controls ↓↓

*   **[REF: MED-11] Asynchronous video pausing [UPDATED]:** Rather than destroying iframe contexts on carousel sliding, inactive `<iframe>` elements configured with `?enablejsapi=1` are sent an asynchronous postMessage post with "pauseVideo" command. Native video targets execute a synchronous `.pause()` to ensure background audio is terminated without resetting buffering pipelines.
*   **[REF: UI-221] Color Synchronicity [NEW]:** Action states representing rigid binary locks (Map Grid and Timeline Zoom Lock) utilize synchronized color markers. Engaging Timeline Zoom Lock forces its SVG path and border to transition to Sapphire Blue (#007acc).


