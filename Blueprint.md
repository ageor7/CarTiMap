# CAR TIMAP ENGINE MASTER BLUEPRINT (EXHAUSTIVE REF CATALOG)
**Version:** v8.17.3-b606 | **Date:** 2026-10-12
**Architecture:** Zero-Build, Single-File ESM Monolithic Engine (<500KB)
**Repository:** ageor7/CarTiMap
**Specification Standard:** Complete 100% REF Tag Registry (Latest Versions & Specifications)

---

## CHAPTER 1: ENGINEERING PROTOCOLS & CODING DIRECTIVES (DSSMP v3.0)

1. **[REF: ARCH-01] Zero-Build Monolithic Footprint & Two-Stage Pipeline:**
   CarTiMap is distributed as a single HTML file containing inline ES modules (Preact, HTM, PapaParse, Leaflet, Wicket, edtf.js). The entire footprint must remain strictly under **500KB** uncompressed to run natively off local disks, Android tablets, GitHub Pages, or enterprise servers without Node/Webpack build steps. The engine strictly separates raw data ingestion (`rawCsvRows`) from compiled data state (`data`) to allow dynamic on-the-fly re-rendering without network latency.

2. **[REF: DOC-01] Two-Tier Documentation (REF-TAGS):**
   Documentation is strictly bifurcated. The Master Blueprint contains the architectural "Why" and "What" (Architecture, UI/UX Rules, Physics), while inline code comments contain the "How" (Mechanics, Loops, Variables). They are permanently interlinked using `[REF: TAG-NAME]` semantic anchors with zero duplication.

3. **[REF: DOC-02] Architectural Block & SubBlock Taxonomy:**
   To eliminate cascading errors and enable risk-free surgical patching, the codebase is strictly categorized into visual and logical boundaries:
   - **Major Blocks:** High-level components (e.g. `AppOrchestrator`, `GlobalStyles`). Syntax: `// === [ MAJOR BLOCK: ComponentName vX.X.X ] ===`
   - **SubBlocks:** Discrete chunks of logic within a Major Block (e.g. `// --- [ SubBlock: LogicDescription ] ---`). Isolate algorithmic vectors from Virtual DOM iterations.

4. **[REF: DOC-03] GitHub Artifact Generation:**
   Every code alteration requires explicit Markdown artifacts prior to code delivery: Commits/Changelogs for history, and Master Blueprint updates for architecture.

5. **[REF: DOC-05] Semantic Bifurcation of Release Notes:**
   - **Commit Descriptions:** Inherently mechanical, documenting exact Virtual DOM manipulations, algorithm adjustments, and architectural physics.
   - **Changelog Entries:** Inherently experiential, documenting functional, user-facing value stripped of developer jargon.

6. **[REF: VER-01] Strict Semantic Versioning Standard:**
   Three-tier semantic versioning `X.Y.Z-bBUILD`:
   - `X` = Architectural rewrite / breaking state-engine redesign.
   - `Y` = Feature release (non-breaking feature addition).
   - `Z` = Bug fixes, patch vectors, or spatial coordinate alignments.
   - `bXXX` = Build iteration counter.

7. **[REF: QC-01] Pre-Compile Line-by-Line Audit:**
   Prior to compiling client-side JavaScript or CSS alterations, a systematic line-by-line audit comparing proposed module states against `/workspace/artifacts/` must be executed to prevent regression of validated features.

8. **[REF: PROT-01] Documentation Supremacy & Strict MD Formatting:**
   No code patch, architectural adjustment, or bug fix is complete without corresponding Master Blueprint and Changelog updates provided in isolated `.md` syntax blocks.

9. **[REF: PROT-02] Discuss First, Implement Later:**
   All bugs, physics, and UI/UX behaviors must be mathematically diagnosed and agreed upon before any code is generated. The developer AI is physically prohibited from generating code without explicit authorization.

10. **[REF: PROT-03] Safety & Functionality Verification:**
    Every proposed architectural patch must be mathematically cross-referenced against current active functionality to protect flexbox layouts, touch targets, and spatial synchronization.

11. **[REF: PROT-04] Architectural Pushback:**
    The developer AI is required to challenge user suggestions if they violate DOM physics, introduce structural fragility, or break mobile responsiveness, offering safe counter-proposals.

12. **[REF: PROT-05] Context Acquisition (The Block Gate):**
    If a diagnosis requires altering a component whose exact current state is not actively locked in memory, the engine must request the specific code block before proceeding.

13. **[REF: PROT-06] Touch Target Preservation (Fitts's Law):**
    Refuses structural UI requests that compromise safe touch interactions on mobile. Primary interaction labels cannot be wholly enveloped in `<a href>` routing tags.

14. **[REF: PROT-07] Context Horizon & Rehydration Protocol:**
    When surgical patches mutate modules beyond the active token horizon, the engine must halt execution and trigger a Context Rehydration request rather than guessing codebase details.

15. **[REF: PROT-08] Structural Risk Assessment (SRA):**
    Calculates the mathematical probability of new code breaking or regressing existing functionality prior to authorizing code patches.

16. **[REF: PROT-09] Unique Patch Delimiters:**
    Bounds all code patches using unique alphanumeric strings (`// 🔽🔽🔽 [ START_INJECT: ComponentName vX.X.X ] 🔽🔽🔽` / `// 🔼🔼🔼 [ END_INJECT: ComponentName ] 🔼🔼🔼`) to eliminate search-and-replace collisions.

17. **[REF: PROT-10] Absolute Blueprint Pathing:**
    Every Master Blueprint update must be prefaced with its exact parent chapter integer and title.

18. **[REF: PROT-11] Continuous Glossary Maintenance:**
    New architectural patterns, CSS methodologies, or data pipeline concepts must be formally classified and appended to the CarTiMap Glossary in subsequent documentation deliveries.

19. **[REF: PROT-12] The Ghost-Code Documentation Protocol:**
    When versioned code is retracted or vetoed prior to deployment: burn the code, keep the version number. The version is permanently spent; Changelog records a "Void" entry; Master Blueprint and Git Commits are bypassed entirely.

20. **[REF: PROT-13] The Anti-Bloat CDN Mandate:**
    Forbids hosting compiled 3rd-party binaries or massive JS dependencies (>500KB AST parsers) directly in the repository. Native ECMAScript Decorators/Interceptors (`compileCartiMapAST`) under 50 lines must be engineered to maintain single-file, zero-build goals.

---

## CHAPTER 2: DATA SCHEMA & UPSTREAM ETL PIPELINE (THE SOURCE OF TRUTH)

1. **[REF: ETL-01] Purpose of Upstream ETL Ingestion:**
   The frontend JavaScript engine is strictly a *renderer*, not a *sanitizer*. Google Sheets `LET()` horizontal consolidation formulas (`ExtractsGroupedV` tab) intercept raw qualitative inputs, deduplicate tags, concatenate descriptions, and natively compile valid JSON/WKT before the frontend receives the payload.

2. **[REF: ETL-02] Cross-Workbook URL Frequency Tracker:**
   Executes cross-workbook frequency analysis to count URL occurrences across `ExtractsDB` and `SourcesDB` tabs, populating the `Used` metric for bibliometric validation.

3. **[REF: ETL-02c] High-Performance String-Aggregation Tokenizer:**
   Consolidates vertical multi-row ranges into a singular string via `TEXTJOIN(CHAR(10), TRUE, range)`, executes horizontal splitting, and translocates elements to a vertical vector using `TOCOL(..., 1)` to prevent 2D matrix calculation collapses.

4. **[REF: ETL-03] ISO 8601-2 Set Geometry Preservation:**
   Captures a `has_brackets` boolean flag prior to sanitization when merging chronological arrays, ensuring single valid range expansions (e.g. `PT12H..PT15H`) retain proper bracket structure.

5. **[REF: ETL-04] The Hard Boundary of the Presentation Layer (Zero Frontend Cleaning):**
   All algorithmic compensation for human data-entry errors, text formatting, hanging indents, or conditional routing is prohibited in client JavaScript. Front-end `ContentSlider` natively renders pre-sanitized strings via `dangerouslySetInnerHTML`.

6. **[REF: ETL-05] Hyperlink Interpolation Offloading:**
   Strips string-quotes from native JSX routing parameters to prevent Virtual DOM compiler collisions. Dynamic title hyperlinking is offloaded to Google Sheets `MAP/LAMBDA` evaluations, exporting safe anchor bypass strings (`z-index: 50; pointer-events: auto`).

7. **[REF: ETL-05b] Title Hyperlinking Engine:**
   Wraps `ContentSlider` titles in clickable `<a href="${slide.webPage}" target="_blank">` elements when valid web page links exist in the dataset.

8. **[REF: ETL-06] Strict EDTF Zero-Padding & Null-Space Armor:**
   Conditional `MID` functions in the ETL formula pad single-digit hours (converting `9:00` to `09:00`) and apply global `SUBSTITUTE` space-stripping prior to CSV export, ensuring flawless Level 2 ISO 8601-2 parsing.

9. **[REF: ETL-08] Native Zero-Build AST Compiler (`compileCartiMapAST`):**
   Replaces heavy 1.2MB Nearley.js binaries with a lightweight (<50 lines) ECMAScript AST Decorator. Recursively deconstructs Choice Sets `[]`, Inclusive Lists `{}`, and Duration Expansions `..` into primitive nodes for core parsing, securing 100% Level 2 EDTF compliance.

10. **[REF: ETL-09] EDTF Choice Set & List Execution Sequence:**
    Choice Sets `[...]` are evaluated FIRST during AST compilation, isolating inner comma-delimited candidates before processing inclusive lists `{...}` and duration ranges `..`.

11. **[REF: ETL-10] MS Word XML Bibliography Generator:**
    Multi-author zip-mapping subroutine residing as a localized closure inside the primary XML MAP loop, splitting newline-delimited (`CHAR(10)`) name strings via `SEQUENCE` and returning concatenated `<b:Person>` objects.

12. **[REF: ETL-11] Parallel Sub-Matrix Ingestion & Sorting:**
    `MAKEARRAY` grouped aggregation maintains a strict 1×17 output column footprint. Parallel sorting vectors (e.g. `ExtractsT!AQ2:AQ`) are imported independently, aligned in memory via `HSTACK`, sorted (`SORT`), and parsed via relative indices to synchronize descriptions with media metadata.

13. **[REF: ETL-12] Parallel Media, Caption, and Credit Sync:**
    Upstream compiler (`MAKEARRAY`) constructs an in-memory `HSTACK` table binding Media (Col 6), Caption (Col 7), and Credit (Col 8) to `sort_data` (Col AQ), executing a descending sort before applying stable `UNIQUE` deduplication. Guarantees `mediaItems[i]` always maps to its true historical `captions[i]` and `credits[i]`.

14. **[REF: ETL-13] Numeric Coercion & Zero-Fill Sorting:**
    Sort vectors remapped to Column AQ (`SRR Total`) process raw inputs through `IFERROR(VALUE(val), 0)` to force integer conversion, coercing empty string cells to `0` so unrated historical snippets recede to the bottom of slide containers.

15. **[REF: ETL-14] Relational ERD & Normalization Mapping:**
    Primary bibliography data (`SourcesT`) is isolated from the spatial-temporal event ledger (`ExtractsT`) and joined dynamically via URL string keys. Unstructured geographic coordinates are extracted, georeferenced in QGIS, and returned to `GeoLU` under shared `Shape_ID` keys.

16. **[REF: ETL-14c] Dynamic Storyline Swimlane Filtering:**
    Filters datasets upstream and downstream by active tag swimlanes and extract types (`Storyline`, `Context`, `Related history`, `Presentation`).

17. **[REF: DATA-02] The Cartographer's Dilemma:**
    Translates human `[Lat, Lon]` inputs to OGC Cartesian `[Lon, Lat]` standards in Google Sheets, securing export interoperability with QGIS/PostGIS.

18. **[REF: DATA-03] Spatial Deduplication:**
    Wraps coordinate arrays in `UNIQUE()`, purging redundant geographic nodes before casting to prevent overlapping DOM elements and broken Z-indexes.

19. **[REF: DATA-05] Direct Key Mapping:**
    Field normalization uses lowercase `norm` object mapping (`exactGet`). Legacy `fuzzy()` logic is deprecated to prevent column string collisions.

20. **[REF: DATA-06] Strict Euro-Date Logic:**
    `parseEuroDate` forces `DD/MM/YYYY` parsing to prevent US-browser month/day inversion.

21. **[REF: DATA-09] Media & Metadata Extraction:**
    `exactGet` ingestion loop extracts `media`, `caption`, and `credit` columns from CSV payloads, flattening strings via `omniSplitRegex` (`/\||?
/`) to guarantee parallel 1:1 array mapping.

22. **[REF: DATA-10] Place/SubLabel Convergence:**
    Hover Tooltips are mathematically bound to the `Place` column, enforcing single-source-of-truth location labeling.

23. **[REF: DATA-12] Primary Chronological Event Sorting & Persistence:**
    `validData` is sorted chronologically by `startDate.min ASC` (primary key), duration `DESC` (secondary key), and `title ASC` (tie-breaker). Serializes user filter states, polygon opacity, date locale, auto-zoom depth, and minimap zoom offset to `localStorage`.

24. **[REF: DATE-02] EDTF Sets Aggregator:**
    Aggregates raw string date inputs in Columns 16 & 17 using `TO_TEXT` to capture visible cell strings, formatting multi-date entries into valid EDTF sets (`[...]`).

25. **[REF: DATE-11] Time Preservation:**
    Decouples `HH:mm:ss` payloads from date strings using whitespace isolation to prevent `00:00:00` collision bugs in timeline zoom physics.

26. **[REF: SUB-01] Universal SubLabel Delimiters:**
    RegEx parser `/[|\-·;]/` splits sublabels, capturing pipes, semicolons, dashes, and the Greek Ano Teleia (`·`).

---

## CHAPTER 3: CARTOGRAPHIC & SPATIAL PHYSICS (GEO-ENGINE)

1. **[REF: MAP-01] WKT & OGC Spatial Engine:**
   Natively parses Well-Known Text (`WKT`), GeoJSON payloads (`GeometryCollection`, `MultiPoint`, `LineString`, `Polygon`), and raw `[Lat, Lon]` pairs via `Wicket`.

2. **[REF: MAP-01b] WKT Axis Inversion Physics:**
   WKT syntax natively formats coordinates as Cartesian `[Longitude, Latitude]`. Wicket (`wkt.read().toObject()`) performs automatic axis inversion to Leaflet's `[Latitude, Longitude]`. Manual Regex fallbacks for `POINT()` explicitly invert capture groups `[parseFloat(m[1]), parseFloat(m[2])]`. Comma-separated inputs (`37.98, 23.72`) are naturally `[Lat, Lon]` and require zero inversion.

3. **[REF: MAP-01c] MultiPoint & Polyline Sub-Label Parsing:**
   Parses line names and endpoint labels from polyline place strings (e.g. `[LineName] StartLabel, EndLabel`), binding start/end markers to respective coordinates.

4. **[REF: MAP-01c2] SubLabel Regex Boundary:**
   Normalizes bracket extraction regex `/\[(.*?)\]/` for polyline place strings across browser engines.

5. **[REF: MAP-01e] Polyline Start/End Marker Anchoring:**
   Binds 6x6px circular Leaflet divIcons to polyline start and end coordinates with distinct tooltip bindings.

6. **[REF: MAP-01f] WKT GeometryCollection Parser & Error Dispatch:**
   Expands WKT parser to recursively deconstruct composite `GEOMETRYCOLLECTION` payloads and GeoJSON feature collections, dispatching real-time error logs to `VibeMonitor` on syntax failure.

7. **[REF: MAP-01g] Map Center-Mass Re-Centering:**
   Calculates visual bounding boxes of active multi-geometry features, flying to center-mass coordinates.

8. **[REF: MAP-01h] Polyline Tooltip Offset:**
   Anchors polyline start/end tooltips with Pt(-34) vertical offset to prevent icon coverage.

9. **[REF: MAP-02] R-Tree Spatial Indexing & Decluttering:**
   Employs an R-Tree spatial index (`MarkerCluster`) using `RBush` to group proximate points within a 40px screen radius into numbered cluster bubbles.

10. **[REF: MAP-02b] Stacked Pin Coordinate Engine:**
    When multiple distinct events share exact, mathematically identical Cartesian coordinates `[Lat, Lon]`, `iconCreateFunction` renders a Stacked Pin (standard pin adorned with a numeric depth badge) instead of a generic cluster bubble, triggering spiderfy animations on click.

11. **[REF: MAP-02c] Anti-Swallow Indexing Pattern:**
    Uses ES6 `.at(0)` accessor (`children.at(0).getLatLng()`) when inspecting cluster arrays to prevent markdown/compiler pipelines from swallowing bracketed index numbers.

12. **[REF: MAP-03] O(1) Spatial State Architecture (Delta Tracker):**
    Builds an $O(1)$ memory dictionary (`markersRef`) on load. During slide navigation, `prevActiveIndexRef` explicitly targets and demotes *only* the old active marker, and targets and promotes *only* the new target marker, reducing spatial rendering complexity by 99.8%.

13. **[REF: MAP-04] Parallel Array Sub-Label Mapping:**
    Strict Linear Map algorithm locking 3 geometries to 3 sub-labels 1:1, preventing label duplication across LayerGroups.

14. **[REF: MAP-04b] Explicit SubLabel Fallback Hierarchy:**
    If an event provides fewer SubLabels than geographic MultiPoints, the engine falls back to the `Place` array, and ultimately to the root event `Title`.

15. **[REF: MAP-05] Linear WKT MultiPoint Flattening:**
    MultiPoint geometries are recursively flattened into a linear array to maintain 1:1 parity with pipe-delimited sub-label arrays.

16. **[REF: MAP-06] The Breathing Map (Temporal Ghosting):**
    Passively monitors `visibleTimeBounds` broadcasted by `TimelineScrubber`. Coordinates outside the active temporal window attenuate to 20% opacity and detach from MarkerCluster buckets, ensuring cluster numbers reflect only active epoch events.

17. **[REF: MAP-07] Precision Vertical Tooltip Offset:**
    Tooltips are anchored with a `-34px` / `-48px` vertical offset to provide aesthetic breathing room above the Map Pin head.

18. **[REF: MAP-07b] Semantic Tooltip Engine:**
    Individual pins broadcast `itemTitle`. Aggregated clusters execute `.getAllChildMarkers()` to project a unified `itemPlace` header followed by a bulleted list of underlying event titles.

19. **[REF: MAP-08] Dynamic Minimap Radar:**
    A secondary Leaflet instance tracks primary map bounds, dynamically adjusting zoom offset (`minimapOffset`, -4z default) and reflowing via `ResizeObserver`.

20. **[REF: MAP-08b] Bidirectional Radar Telemetry:**
    Uses an `isSyncingRef` clutch. Manual zoom/drag on the minimap calculates the integer zoom gap and broadcasts it back to React state, updating `minimapOffset`.

21. **[REF: MAP-08c] Radar DOM Expansion:**
    `.minimap-container` utilizes `resize: both` monitored by a `ResizeObserver` firing `miniMap.invalidateSize()` on resize.

22. **[REF: MAP-09] Telemetry Bridge (Stale Closure Fix):**
    Injects `minimapOffsetRef` to feed live data into frozen React event listeners.

23. **[REF: MAP-10] Visual Projection Math (Minimum Viewport Clamp):**
    Projects synthetic expanded `L.latLngBounds` when zooming deep, guaranteeing the minimap aiming rectangle never shrinks below a 30-pixel readable limit.

24. **[REF: MAP-11] Basemap Core Registry:**
    Holds Leaflet construction data for base providers, injecting selected target layers into Main Map and Minimap simultaneously.

25. **[REF: MAP-12] EDTF Quantum Evaluation:**
    Map chronological intersections bypass linear duration checks when EDTF Sets `[]` or Lists `{}` are detected, looping through disjointed `edtf.values` to enable quantum (flashing) marker visibility over fragmented timelines.

26. **[REF: MAP-80] Dynamic Web Map Service (WMS) Routing:**
    Parses `format` and `wmsLayer` columns. WMS flags route layers through `L.tileLayer.wms()`, requesting custom single-image renders directly from enterprise GeoServers (e.g. Harvard Geospatial Library `mapimages_public:G6814_A9_1923_G4` or Dipylon Attica Survey `Kaupert:kaupert_front_georeferenced`). Supports comma-separated server-side layer compositing.

27. **[REF: MAP-81] Overlay Severance:**
    Forbids rendering heavy historical overlays on the Minimap, cutting HTTP payloads to third-party IIIF servers by 50%.

28. **[REF: MAP-85] WebGL & Vector Tile Architecture:**
    Dynamically injects MapLibre GL JS and Leaflet bindings for Protomaps `.mvt`/`.pbf` vector tiles, spinning up WebGL only when vector basemaps are selected.

29. **[REF: MAP-86] Layer Casing (Cartographic Styling):**
    Controls vector basemap aesthetics via local `style.json` using WebGL layer casing (thicker casing layer underneath a thinner fill layer) with `stops` arrays to scale line width by zoom level.

30. **[REF: MAP-87] IIIF Spatial Proxy Integration (Allmaps):**
    Extracts IIIF `manifest.json` from academic archives (Princeton, Harvard), georectifying via Allmaps Editor GCPs and loading XYZ tile endpoints (`https://allmaps.xyz/images/{ID}/{z}/{x}/{y}@2x.png`).

31. **[REF: MAP-GEOM-03] Spatial Geometry Bounds Checking:**
    Safely validates bounds objects (`b.isValid()`) before flying or fitting Leaflet camera positions.

32. **[REF: MAP-HUD-01 & MAP-HUD-01c] Spatial Control Cluster:**
    Anchors zoom in/out buttons, zoom factor indicator, coordinate grid toggle, and layers menu popover to top-left / top-right viewport coordinates.

---

## CHAPTER 4: TEMPORAL PHYSICS & CHRONOLOGICAL MATHEMATICS (CHRONO-ENGINE)

1. **[REF: CHRONO-01] Pinned EDTF.js Version:**
   Pins `edtf@4.11.0` via esm.sh to insulate chronological AST parsing against upstream breaking changes.

2. **[REF: CHRONO-08] Strict EDTF Object Comparison:**
   Uses strict type checking (`parsed.min === Number.NEGATIVE_INFINITY || parsed.max === Number.POSITIVE_INFINITY`) for open-ended EDTF dates (`..`).

3. **[REF: CHRONO-09] P-Type EDTF Duration Clamp:**
   Resolves EDTF P-type duration parsing (`P1Y6M`), clamping range expansions from erroneously expanding 25 years wide.

4. **[REF: TL-01] Intelligent Time Rendering Range:**
   Buffers dataset time edges with a 5% chronological margin (`padMs = rawTimeRange * 0.05`), generating breathing room for first and last graphical event nodes.

5. **[REF: TL-02] Dynamic Timeline Swimlane Math:**
   Iterates through dataset tags to generate `laneCount`, binding `orderedTags.indexOf(tag)` to calculate Y-axis placement constraints and prevent chronological collisions.

6. **[REF: TL-02d & TL-05c] Timeline Zoom & Pin Anchor Synchronization:**
   Synchronizes X-axis percent placement (`startPct`) with manual zoom level shifts.

7. **[REF: TL-12] Hexagon Node Vertical Alignment:**
   Aligns left-facing hexagon chevrons cleanly within tag swimlanes.

8. **[REF: TL-13] Hexagon Arrow Typographic Envelope:**
   Event geometry uses absolute CSS `clip-path` (`polygon(0 calc(50% - 12px), ...)`), allowing blocks to expand infinitely downward for 3-line text wrapping without skewing directional chevrons.

9. **[REF: TL-14] Drop-Line Vertical Pinning:**
   Anchors `.event-group` parent above X-axis track (`bottom: 28px`), calculating indicator height (`containerHeight - 28 - topPos - blockHeight/2`) straight down from hexagon geometric center to X-axis plane.

10. **[REF: TL-15] Semantic Timeline Spans:**
    Auto-converts millisecond variables to human-readable span strings (Minutes, Hours, Days, Years) based on scroll zoom coefficients.

11. **[REF: TL-16] Smart Chronology Formatting:**
    Renders Year for multi-year spans, `DD/MM/YYYY` for intermediate spans, and `HH:mm` clock arrays for intra-day zooms.

12. **[REF: TL-17] Timeline Omni-Splitter Ingestion:**
    Intercepts `item.tags` via `getParsedTags()`, splitting horizontal swimlanes during background track generation.

13. **[REF: TL-18] Z-Stacking Density Engine:**
    $O(1)$ memory registry (`stackRegistry`) intercepts concurrent chronological events, generating keys `${timestamp}_${laneIndex}`. Simultaneous events fan out via sequential CSS `calc()` offsets (`+6px` X, `+4px` Y), preventing eclipsing and communicating historical density.

14. **[REF: TL-19] 4D Telemetry Hoisting:**
    Timeline Scrubber passively calculates and broadcasts its absolute chronological boundaries `[visibleLeftMs, visibleRightMs]` to global state for spatial filtering.

15. **[REF: TL-19b] Stepped Orthogonal Duration Trapezoids:**
    Duration spans render `clip-path: polygon(0 0, 100% 4px, 100% 100%, 0 100%)` with a `2px solid` left border. Overlapping spans eclipse prior tails with an 8px leading border, generating a heat-map band along the bottom 4px track. EDTF approximate boundaries render a `3px solid #ffb300` (Gold) line.

16. **[REF: TL-20] The Momentary Drop-Line:**
    Point-in-time events (`!hasDuration`) project a solid 2px vertical drop-line straight down to the X-axis, piercing duration ribbons. Color mapping: `#cc0000` (Red) inactive, `#ffb300` (Gold) approximate, `#28a745` (Green) active.

17. **[REF: TL-21] Temporal Intersection Filter (Ribbon Suppression):**
    Ribbons intersecting the active slide envelope receive full rendering mass; ribbons outside are suppressed to a 2px dotted baseline (`z-index: 800`).

18. **[REF: TL-22] Full-Matrix Tag Adjacency Algorithm:**
    Combinatorial tag extraction loop (`A-B`, `A-C`, `B-C`) clusters related `laneHeight` blocks, minimizing vertical rendering waste.

19. **[REF: TL-23] Stratified Ghost-Caliper Matrix:**
    Inactive duration ribbons render as "Ghost-Hatch Calipers" (open inverted Π) with `border-left: 3px`, `border-right: 3px`, `border-bottom: 2px` and repeating linear gradient transparent hatch fills, elevating via `bottom: calc(${stackDepth * 4}px)` up to a 22px safe-zone ceiling.

20. **[REF: TL-24] Interaction-Time Intersection (Lazy Tooltips):**
    Hovering a ribbon triggers a 400ms `setTimeout` query, filtering dataset for temporal collisions and rendering HUD tooltips listing all intersecting titles.

21. **[REF: TL-26] The Modulo-Pattern Matrix:**
    Applies `stackDepth % 3` array indexing to rotate stacked ribbons through `['solid', 'dashed', 'dotted']` borders and `['45deg', '-45deg', '90deg']` repeating gradients.

22. **[REF: TL-27] The Spatial Anchor Pattern:**
    `.event-group` wrapper acts as an unmoving Cartesian anchor (`left: ${startPct}%`). Drop-lines, trapezoids, and hover bridges sit at `left: 0`. Only the typographic child (`.event-block`) receives `xOffset` CSS displacement.

23. **[REF: TL-28] Floorless Woven Matrix & Rotating Vector Pattern Hatching:**
    Inactive ribbons anchor to `bottom: 0` without lower CSS borders, using deterministic `startDate` modulo indices to map `hatchingAngles` (`135deg` /, `90deg` |, `45deg` \) with a 24px pattern cycle (1.2px stroke, 22.8px transparent gap). Applies GPU `-webkit-mask-image: repeating-linear-gradient` (70px drawn, 30px erased).

24. **[REF: TL-29] The Dual-Tone Barber Pole (Approximations):**
    When `isApproxStart` is true, drop-lines transition to `repeating-linear-gradient` weaving active color (`#28a745` / `#007acc`) with Gold (`#ffb300`) uncertainty in a 4px/8px dashed sequence.

25. **[REF: TL-30] Emerald Active Parity & Weighted Gravity Matrix:**
    Active state tokens across Map pins, TOC indicators, event cards, and duration ribbons strictly use Emerald Active Green (`#28a745` / `#b3e2c2`). Tag swimlanes execute an $O(N^2)$ Weighted Gravity Sort, placing highest frequency tags at `laneIdx = 0` (top) and pushing rare orphaned tags to bottom swimlanes.

26. **[REF: TL-31] True Cartesian Anchoring:**
    Eliminates barcode drift by locking `.event-group` wrapper to `left: ${startPct}%`, declaring drop-lines and trapezoids at `left: 0`, and applying `labelXOffset` exclusively to the text card.

27. **[REF: TL-32] Equal Height Track Partitioning & Inverted Tooltip Physics:**
    Timeline height above X-axis is partitioned equally across all category swimlanes and the Duration Lane:
    $$	ext{totalTracks} = 	ext{laneCount} + 1$$
    $$	ext{laneHeight} = rac{	ext{containerHeight} - 28	ext{px}}{	ext{totalTracks}}$$
    Hover bridge tooltips anchor to `top: 15px` projecting downwards (`max-height: calc(100% - 45px)`).

28. **[REF: TL-33] Chronological Heat-Glow (Matte Glow) & Duration Lane Line Purge:**
    Concurrent simultaneous events apply dynamic `box-shadow: 0 0 ${stackDepth * 2}px ${stackDepth * 0.25}px` directly to 2px drop-lines. Purged obsolete `bottom: 28px` white separator band `div`, adding a `#f8fafc` slate track bed for Duration Lane.

29. **[REF: TL-34] Cursor-Relative Tooltip Clamping & Category Header Purge:**
    Caliper tooltips intercept `e.clientX` over duration ribbons, dynamically clamping (`Math.max(125, Math.min(x, width - 125))`) to keep HUDs in viewport. Purged `⏱️ Duration Lane` text header from left sticky column.

30. **[REF: TL-35] Asymmetric Duration Trapezoid Slope:**
    Duration spans project an asymmetric ribbon using clip-path:
    $$	ext{clip-path}: 	ext{polygon}(0\%\ 0\%, 100\%\ 75\%, 100\%\ 100\%, 0\%\ 100\%)$$
    leaving a distinct 25% height vertical end-cap marker.

31. **[REF: TL-CLAMP-01] Span Geometry Clamp:**
    Timeline Scrubber enforces a minimum temporal visual width of 24 hours (`86400000` ms) to prevent `0px` layout collapse in single-event datasets.

32. **[REF: TL-CLAMP-02] Infinity Geometry Clamp:**
    Automatic scaling math enforces a strict `60000` ms floor on event time gaps, preventing divide-by-zero errors.

33. **[REF: UI-66] 6px Swimlane Top Padding Clearance:**
    Enforces `topPadding = 6px` above top swimlane track bed (`topPos = topPadding + laneIdx * laneHeight`), shifting top swimlane nodes down by 6px (~half a lane height) to provide complete visual clearance for 3-line hexagon node labels without top clipping.

---

## CHAPTER 5: UI/UX ELEMENTS & RESPONSIVE LAYOUT ENGINE

1. **[REF: UI-01f] Unified Layout Root:**
   Root `#app-layout` container manages flex column layout, resizers, and status bar positioning.

2. **[REF: UI-04] Media Link Formatting:**
   Formats description snippets with paragraph wrappers and inline hyperlinks.

3. **[REF: UI-05] Visual Hierarchy (Map Pins):**
   VIPs = Gold pins (`#ffb300`), Active = Oversized Green pins (`#28a745`), Inactive = Standard Royal Cyan pins (`#007acc`).

4. **[REF: UI-08 & UI-08c/e] Multi-Context Branding Logo:**
   Logo Hex-Frame Chrono-Compass vector geometry (`cartimap-favicon.svg`) scales dynamically from Splash Context to Status Bar and About Modal contexts.

5. **[REF: UI-12c] Search Close Centering:**
   SVG cross icon inside circular 32x32px close button centered in search modal.

6. **[REF: UI-13] Metadata Hierarchy:**
   `📍 Place` badge utilizes non-bold pill aesthetic to distinguish metadata from narrative text.

7. **[REF: UI-32] Smart Date Deduplication (Same-Day Delta):**
   Strips midnight `00:00:00` signatures. Same-day events with differing times output clean temporal deltas (e.g. `15:45 — 16:00`).

8. **[REF: UI-35] Filter Cockpit Popover:**
   Floating Filter Cockpit menu supporting extract type switches (`Storyline`, `Context`, `Related history`, `Presentation`) and tag swimlane toggles. Button turns blue when filters are active.

9. **[REF: UI-39] Shrink-Wrapped Sticky Header (Direct-Child Architecture):**
   `ContentSlider` enforces geographic-first hierarchy (`Date ➔ Places ➔ Tags ➔ Title`). Header freezes at `top: 0` while narrative body scrolls.

10. **[REF: UI-40] Golden SVG Tag Identity:**
    Semantic Tags use inline `<svg>` path (`#ffc107`), universally rendering a gold tag icon.

11. **[REF: UI-41] Multi-Provider Universal Binary Translation:**
    Regex pipeline intercepts Google Drive and GitHub URLs, transposing them to raw API endpoints (`uc?export=view&id=` and `raw.githubusercontent.com`) for direct media rendering.

12. **[REF: UI-42] InvalidateSize Base-Tile Forcing:**
    Delays execution for 250ms on resize/maxPane transitions and forces `mapInstance.invalidateSize()`, commanding Leaflet to poll true DOM dimensions and trigger pending tile fetches.

13. **[REF: UI-43] Bottom-Up Zebra Contrast:**
    Enforces bottom-up swimlane zebra striping (`(laneCount - 1 - i) % 2 === 0`), guaranteeing dark shading on the bottom swimlane directly adjacent to Duration Lane.

14. **[REF: UI-44] Borderless Soft Mint Hexagon:**
    Inactive hover/highlight states style `.event-block` with borderless soft mint background (`#e6f4ea`) and dark forest green text (`#137333`).

15. **[REF: UI-45] Color-Matched Active Hexagon:**
    Active card fill matches duration ribbon alpha (`rgba(40, 167, 69, 0.35)`) with bold black text (`#111111`).

16. **[REF: UI-46] Solid Opaque Active Card Fill:**
    Active `.event-block` cards use solid opaque `#b3e2c2` fill with normal font weight (`500`) pure black text (`#111111`), securing 11.8:1 WCAG AAA contrast and blocking drop-line vector bleed-through.

17. **[REF: UI-47] The 75ch Readability Clamp:**
    Narrative description block (`.slide-desc`) is clamped to `max-width: 75ch` and centered, preserving natural scroll and readable line length.

18. **[REF: UI-48] Flex-Greed Typographic Capping:**
    Desktop 50/50 split caps narrative text at `max-width: 95ch`. When text hits readability limits on ultrawide monitors, Visual Pane (`flex: 1 1 0; width: auto`) consumes 100% of remaining horizontal space.

19. **[REF: UI-49] Typographical Outset (The Master Typographic Envelope v3):**
    Sticky header enforces `max-width: 85ch` Master Envelope, overhanging the `65ch`/`75ch` narrative text block below. Long Titles and Place names expand without premature breaks while sharing left-flushed alignment with Date strings.

20. **[REF: UI-51 & UI-51b] Fluid Responsive Reading Room Axis Rotation:**
    - Viewports `<1024px` (Mobile/Portrait): Vertical column stack (`--primary-split: 55%`). Resizer calculates Y-axis deltas. Flex-greed is suspended.
    - Viewports `>=1024px` (Desktop): Geometric axis rotates 90 degrees to side-by-side reading room layout (`50% / 50%` split). Text pane claims 50% left; Map & Media claim 50% right sidebar. Resizer calculates X-axis deltas.

21. **[REF: UI-52] Layout Boundary Mathematical Reset:**
    Crossing `1024px` threshold zeroes structural variables back to baseline, preserving proportional integrity.

22. **[REF: UI-53] Dynamic Secondary Viewport Collapse:**
    When `activeSlide.media.length === 0`, Media pane and secondary resizer hide (`display: none`), and Map instance expands to consume 100% of visual quadrant.

23. **[REF: UI-61] CSS Native Touch Override:**
    Applies `touch-action: none` to `.resizer-dyn` splitters, yielding 100% of raw touch coordinates to JavaScript drag handlers.

24. **[REF: UI-62] Strict Android Flexbox Containment Cage:**
    Stylesheet enforces `max-width: 150px !important; flex-shrink: 0 !important` on minimap wrappers to prevent Android webviews from expanding the node.

25. **[REF: UI-63 & UI-64] Side-by-Side Metadata Ribbon Flex Allocation:**
    Configures `.metadata-date` to `flex: 1 1 200px` / `flex: 2 1 300px` and `.metadata-pills-wrapper` to `flex: 1 1 160px` / `flex: 1 2 140px`, allowing location and tag pills to wrap vertically right-aligned while Date claims left width across 2 clean lines.

26. **[REF: UI-65] Micro-Scroll Ribbon Header Compression:**
    Breaching 40px scroll in `ContentSlider` compresses header padding, shrinks Title font size, and merges metadata into a sticky compact ribbon.

27. **[REF: UI-67 & UI-68] 70%/70% Elastic Movable Border Architecture:**
    - `ContentSlider` Ribbon: Sets Date to `flex: 1 1 100px; max-width: 70%` and Pills wrapper to `flex: 1 1 100px; max-width: 70%; margin-left: auto; justify-content: flex-end`.
    - `OverviewGantt` Header: Sets Title to `flex: 1 1 auto; max-width: 70%` and Date to `flex: 0 1 auto; max-width: 70%`.
    - Minimizes total ribbon height by allowing long Place pills or EDTF dates to claim up to 70% row width without full-screen row drops.

28. **[REF: UI-69] Contextual Keep-Out Zones & Spatial Ribbon Decoupling:**
    Injects `padding-right: 55px` keep-out zone into right flank of metadata ribbon, isolating right-aligned pills from floating top-right Maximize buttons.

29. **[REF: UI-70] Map HUD Typography & Interaction Matrix:**
    Zoom controls use vertical "Sandwich" flexbox column (`[+]`, `[14z]`, `[-]`), anchoring focal integer between action triggers.

30. **[REF: UI-71] Real-Time Layer Opacity Engine:**
    Layers HUD mounts HTML `<input type="range">` opacity sliders decoupled from `<label>` parents, executing `L.tileLayer.setOpacity()` in real-time.

31. **[REF: UI-72] Global Maximization Matrix:**
    `AppOrchestrator` injects scoped CSS classes (`max-text`, `max-map`, `max-media`), expanding active pane to 100% width/height while safely unmounting sibling viewports without destroying Virtual DOM state.

32. **[REF: UI-83] Top-Right Spatial Constraints:**
    External links, maximize toggles, and media counters lock to floating absolute top-right spatial axes.

33. **[REF: UI-85] Spatial Window Management:**
    Window management (Minimize/Maximize) anchors top-right; temporal navigation (Zoom, Lock) docks lower to prevent accidental clicks.

34. **[REF: UI-86] Drawer & FAB Synergy:**
    Minimizing timeline shrinks container height to `0px`. CSS transition buffers resize for `ResizeObserver` tile redrawing. Floating Action Button (FAB) mounts over map to restore timeline drawer.

35. **[REF: UI-87] Android Typography Reset:**
    Abandons emojis in favor of mathematically defined SVGs with `-webkit-appearance: none` and hardcoded dimensions to prevent mobile OS font inflation.

36. **[REF: UI-88] Universal Button Topology & The Phantom Hitbox:**
    Tier-2 utility toggles (`.status-btn`, 22x22px / 24x24px) wrap in an invisible `::after` pseudo-element projecting an 8px interactive bounding box beyond visual perimeter, securing mobile touch target compliance.

37. **[REF: UI-136] Absolute Pane Flex-Cages:**
    Map wrappers lock to `flex: 0 0 var(--secondary-split); min-height: 0; min-width: 0; flex-shrink: 0`, preventing high-res media from crushing map panes to 0x0.

38. **[REF: UI-139] The 270-Degree Back Vector:**
    Navigation Back button SVG arc traces counter-clockwise `M 4 12 A 8 8 0 1 0 12 4`, creating a rewind visual cue.

39. **[REF: UI-142] Media Spotlight Casing:**
    Vertical media uses CSS dot-matrix casing overlay (`radial-gradient(#333 1px, transparent 1px)`) with absolute-center soft white spotlight to separate media from UI.

40. **[REF: UI-150] Layout Reset Engine:**
    `Reset Layout` command zero-states active pane variables back to structural baseline (`55% / 50% / 10%`) and clears Maximize states.

41. **[REF: UI-154] Intelligent Contextual Maximize:**
    Maximize evaluates data footprint (`timelineRequiredHeight = (laneCount * 24) + 40`), snapping drawer height to reveal all swimlanes with zero pixel waste (clamped to 70% max viewport height).

42. **[REF: UI-156] Ascender/Descender Brand Typographic Locking:**
    `CarTiMapperLogo` SVGs bind to 22px height wrapper, forcing `align-items: baseline` to align Logo ascender to brand text descender.

43. **[REF: UI-159] Z-Index Layer Menu Liberation:**
    Map and Visual panes use `overflow: visible; z-index: 30` while map tiles lock to `overflow: hidden; z-index: 1`, preventing tablet viewports from clipping overlay menus.

44. **[REF: UI-164 & UI-164c] Viewport Center-Mass Selection & Status Cockpit:**
    Isolates `viewportCenterMs`, granting `DD/MM/YYYY` anchor label to Major Tick closest to screen center-mass with 65px keepout radius. Conformed 38px Status Cockpit centers Prev/Next buttons with non-bold scale metrics (`Span`, `Zoom`).

45. **[REF: UI-165] Declutter Modulo Masks:**
    Minor tick geometry renders unconditionally; semantic text values execute Modulo arrays (`% 2 === 0` or median instance).

46. **[REF: UI-167] Contextual Truncation Math:**
    Ticks snapping to exact hour truncate to hour integer (`14h`); trailing minor ticks render fractional deltas (`:15`, `:30`). Daily zooms replace `00h` with date strings (e.g. `12 May`).

47. **[REF: UI-175] Global Beam Architecture:**
    Status bar (`.global-status-bar`, 38px) sits as a static horizontal beam between Core Viewports and Timeline Scrubber, surviving pane maximizations.

48. **[REF: UI-176 & UI-176b] Universal Hardware Escape & Sticky Closures:**
    Modals (`About`, `Search`, `Settings`) and `VibeMonitor` inject absolute inline `z-index: 10001` / `10000` at `#tm-root` level, bypassing isolated flex-cage stacking contexts. Modals use flexbox geometry with sticky close buttons.

49. **[REF: UI-177] Fluid Metadata Wrapping:**
    Removes restrictive `white-space: nowrap` from `.metadata-ribbon`, allowing multi-location strings to wrap gracefully.

50. **[REF: UI-178 & UI-178b] Ghost Margin & Precision Scrollbar Suppression:**
    Globally suppresses WebKit scrollbars on horizontal track containers (`::-webkit-scrollbar { display: none }`), while permitting standard vertical scrollbars in text panes.

51. **[REF: UI-179] Absolute Grid Lockdown:**
    Bans `100vw`/`100vh` on `#tm-root`. Locks root via Absolute Hardware Anchoring (`position: absolute; top: 0; bottom: 0; left: 0; right: 0; box-sizing: border-box`), sealing UI against OS scrollbar bleed.

52. **[REF: UI-181] Desktop Carousel Kinetics:**
    Desktop `MediaViewer` intercepts `onMouseDown`, applying `.is-dragging` class to disengage CSS `scroll-snap-type` and yield panning control to JavaScript friction loops before snapping on `onMouseUp`.

53. **[REF: UI-182] Obsidian Glass Universal Contrast Matrix:**
    Carousel controls apply `rgba(0,0,0,0.6)` obsidian glass styling with 1px border, securing >4.5:1 WCAG contrast over bright/dark media.

54. **[REF: UI-183] Contextual Modal Architecture:**
    Bifurcates "About" modal: primary layer shows historical narrative and dataset download links; technical specs relegate to bottom `<details>` accordion.

55. **[REF: UI-184] Pure CSS Legend Geometries:**
    Constructs `SymbologyLegend` HUD using exact same CSS geometries, clip-paths, and radial gradients used by Leaflet and Timeline Scrubber.

56. **[REF: UI-185] Magnetic Hover Text:**
    CSS `.event-block:hover { width: max-content !important; z-index: 40 !important }` magnetically expands elided hexagon labels to full width on hover without JS layout recalculation.

57. **[REF: UI-186] Swimlane Bottom-Clearance Math:**
    `.tag-lane` enforces `bottom: 40px` offset; `xAxisMarker` duration ribbons sit at `bottom: 0` inside `.event-group` anchored at `bottom: 28px`, guaranteeing a 2px clearance gap above X-axis ruler.

58. **[REF: UI-187] Timeline Y-Axis Boundary Clamping:**
    Locks top track boundary to `top: 15px` to insulate `.tag-lane-label` from status bar drop-shadows. Restricts `yOffset` displacement to 2px per stack depth integer.

59. **[REF: UI-188] Asymmetrical Hit-Boxes:**
    Decouples CSS clip-paths from interactive listeners. Sibling `.hover-bridge-hitbox` node is biased downwards (`bottom: -15px`) past typography into 28px X-axis dead-space.

60. **[REF: UI-190] Semantic Cartographic Palette:**
    Active focus = Sapphire Blue (`#0066cc`) / Emerald Green (`#28a745`); Inactive = Slate Grey (`#78909C`); EDTF Approximations = Burnt Amber (`#E65100`).

61. **[REF: UI-191] Parallel Racing Stripes (Vertical Approximations):**
    Renders 2px dominant core of Burnt Amber (`#E65100`) flanked by 1px Sapphire Blue (`#0066cc`) anchor shadow to signal active event uncertainty.

62. **[REF: UI-192] Defensive CSS RGB Architecture:**
    Color variables use defensive fallbacks `rgb(var(--tm-active-rgb, 0, 102, 204))` to prevent CSSOM failure when dynamic themes are uninitialized.

63. **[REF: UI-193] White-Label Theme Expansion:**
    Decouples timeline floor, tooltip background, and heat-shadows into `--tm-` CSS Custom Property matrix controlled by `ThemesT` database tab.

64. **[REF: UI-194 & UI-194b] Scrollbar Detection & Anti-Occlusion:**
    Calculates OS scrollbar width (`offsetWidth - clientWidth`) and casts to `--sb-w`, dynamically shifting right click-zones to prevent Z-index scrollbar occlusion. Eliminates phantom scroll hijacking.

65. **[REF: UI-195] Fluid Flex-Wrap Metadata Topology:**
    `.metadata-ribbon` uses Date as left anchor (`flex-shrink: 0`) and propels Places/Tags via `margin-left: auto` into right-aligned flex-wrapping sub-container.

66. **[REF: UI-196] Flexbox & Cartesian Hanging Indents:**
    Google Sheets ETL outputs `display: flex` DOM structures isolating emojis into non-shrinking columns (`flex-shrink: 0; width: 1.2rem`) adjacent to text body, guaranteeing flush-left margins across operating systems.

67. **[REF: UI-197] Aggressive Typographical Compaction:**
    Breaching 40px scroll compresses header padding 50%, reduces Title to 0.95rem / Date to 0.75rem, and applies GPU-accelerated `transform: scale(0.9)` to metadata pills.

68. **[REF: UI-199 & UI-199b] Universal Button Topology & Flexbox Clamping:**
    - Tier 1 (Navigation): 36x36px.
    - Tier 2 (Utility Toggles): 24x24px baseline (`.status-btn`).
    - Parent flex containers enforce rigid `width: 24px; box-sizing: border-box` dimensional clamps to prevent Flexbox from stretching square utility buttons. Contextual size overrides are purged.

69. **[REF: UI-201] Native Scrollbar Keep-Out Zone (28px Gutter):**
    Top-right floating HUD elements in `overflow-y: auto` parent containers enforce strict `right: 28px` minimum anchor to permanently clear native OS vertical scrollbars (15-17px width).

70. **[REF: UI-236b] Compass Vector Logo Identity:**
    Restores high-fidelity compass needles and bracket base vector graphics for `CarTiMapperLogo`.

71. **[REF: UI-340] Search Slide Drift Resolution:**
    Search click-handler `handleResultClick` uses absolute dataset ID lookup `data.findIndex(d => d.id === id)` to jump to exact sorted slide index without drift.

72. **[REF: UX-30] State-Reset Scroll Zeroing:**
    `ContentSlider` useEffect hook bound to `activeIndex` fires `viewportRef.scrollTo({ top: 0 })` on slide mutation, resetting vertical scroll position.

---

## CHAPTER 6: MEDIA CAROUSEL & ASSET HUD (MEDIA-ENGINE)

1. **[REF: MED-08] Aggressive CRLF Sanitization:**
   RegEx `/\||?
/` identifies and strips Windows carriage return `` ghosts from URLs, preventing HTTP 404 connection failures.

2. **[REF: MED-11] Omni-Splitter Array Flattening:**
   CSV mapping phase splits multi-value cell arrays 1:1 across Media, Caption, and Credit columns via `omniSplitRegex` (`/\||?
/`).

3. **[REF: MED-12] YouTube API Timestamp Translation:**
   Regex interceptor extracts `?t=` parameters, converting seconds to integer values and appending `?start=[seconds]` to embed iframe URLs.

4. **[REF: MED-13 & MED-13b] Z-Stack Passive PDF Failsafe & Contrast Protection:**
   Mobile PDF iframes deploy a Z-stack failsafe: explanatory text banner painted at z-index 1 under transparent PDF iframe at z-index 2. Failsafe wrapper enforces `#222` (Charcoal) background for dark contrast.

5. **[REF: MED-14] 404-Protected Clickable Metadata:**
   Media credits pass through HTTP string detector (`/^https?:\/\//i`). Valid URLs wrap in target-blank anchors; plain text strings render natively.

6. **[REF: MED-15] Iframe Event-Swallow Failsafe (Chevron HUD):**
   When media arrays contain >1 items, MediaViewer mounts `<` and `>` navigation chevrons at `z-index: 1000` over interactive iframes (YouTube, PDFs, WebGL) to prevent touch-swallow trapping.

7. **[REF: MED-16] URL Sanitization (Evaluation vs Routing):**
   Decouples URL strings for file type evaluation: temporary `evalUrl` strips `?` queries and `#` hashes for extension checks (`.pdf`, `.png`), while Virtual DOM routes to original url.

---

## CHAPTER 7: DIAGNOSTICS, INTEGRITY & SYSTEM STABILITY (VIBE-MONITOR)

1. **[REF: DIAG-01] Floating Diagnostic HUD:**
   Draggable, resizable, fixed-position telemetry window (`#vibe-monitor`).

2. **[REF: DIAG-02] Dynamic Variable Extraction:**
   Telemetry monitor configuration mode scans `activeSlide` DOM node, mapping available CMS fields to `tm_telemetry_fields` in local storage.

3. **[REF: DIAG-03] Exact Millisecond Diagnostics:**
   Telemetry readouts for `startDate` and `endDate` yield strict ISO payloads (`val.toISOString()`) for precise verification.

4. **[REF: DIAG-04] Omni-Directional Telemetry Scaling & DOM Anchoring:**
   `onMouseDown` drag events poll physical DOM via `getBoundingClientRect()`, locking physical dimensions into React `size` state (`resize: both`). Drops monitor 15px above global status bar.

5. **[REF: DIAG-05] Multi-Segment Telemetry Layout:**
   - Top Segment (Unscrollable): App/Module versions, layout mode, CSV row counts.
   - Middle Segment: Active slide variable inspector.
   - Bottom Segment: Running error/warning log stream.

6. **[REF: TELEMETRY-01] Real-Time Event Logging:**
   Central `addLog(msg, type)` dispatcher records fetch statuses, parsing warnings, and spatial syntax errors.

7. **[REF: TELEMETRY-05] Dynamic Document Title Sync:**
   Regex strips narrative HTML tags (`<b>`, `<i>`) from CMS title payloads before syncing with native `document.title` API.

8. **[REF: BOOT-CRASH-01] Boot Safety Validation:**
   Validates native JS constructors (`new URLSearchParams`) against syntax typos prior to React's first render hook.

9. **[REF: BOOT-CRASH-02 & BOOT-CRASH-02b] Spatial Array Integrity & Hardcoded Pin Dimensions:**
   Leaflet camera calls (`setView`, `fitBounds`) enforce rigid `[x, y]` pixel array structures (`iconSize: new L.Point(24, 34)`, `iconAnchor: new L.Point(12, 34)`), insulating geometry against markdown parser truncation and preventing `t is null` crashes.

10. **[REF: BOOT-CRASH-03] Character Class Escape Validation:**
    Sanitizes character class range bounds in coordinate matching regexes (`/(-?\d+(?:\.\d+)?)[,\s]+(-?\d+(?:\.\d+)?)/`).

11. **[REF: CRASH-01] WKT GEOMETRYCOLLECTION Polyfill:**
    Deconstructs composite `GEOMETRYCOLLECTION` wrappers and passes isolated internal primitives through parser. Dynamic zoom ceilings calculate `maxGlobalZoom` from highest available CMS layer.

12. **[REF: CRASH-02] React Prop Continuity:**
    Cross-component functions (`jumpToSlide`) pass explicitly via React component props to prevent ReferenceErrors in isolated modals.

13. **[REF: CRASH-03] HTM/Preact Parser Collision Prevention:**
    Forbids standard React pseudo-comments (`{/* comment */}`) inside HTM template literals (`html```), preventing phantom DOM element generation.

14. **[REF: CRASH-04] VDOM Array Reconciliation Integrity:**
    Binds explicit `key=${...}` properties to root nodes of mapped literals in HTM templates, preventing fatal `Node.insertBefore` crashes during slide navigation across differing array lengths.

15. **[REF: CRASH-05 & CRASH-05b] HTM Template Literal Escaping:**
    Text nodes containing `<` followed by numbers/strings (e.g. `<10 items`) must escape HTML entities (`&lt;`, `&amp;`) to prevent `htm` parser from interpreting them as unclosed tags and triggering `invalid character` DOMExceptions. Refactored About Modal download links out of nested JSX templates.

16. **[REF: CRASH-06] The TouchList Prototype Trap:**
    Mobile touch listeners must never call Array prototype methods (`.at()`) on `e.touches` or `e.changedTouches` (which return TouchList DOM interfaces), relying strictly on bracket notation (`e.changedTouches[0]`).

17. **[REF: CRASH-07] Bracket Stripping Immunity:**
    Uses `.shift()` for arrays and `.item(0)` for TouchLists to retrieve first elements, insulating code against text-stripping transmission pipelines that swallow bracketed `[0]` indexers.

18. **[REF: SYNTAX-02 to SYNTAX-05] ES Module & Template Literal Integrity:**
    Validates JS module export strings, string template interpolations, and backtick delimiters against AST syntax errors.

19. **[REF: STY-01c] CSS Variable Fallback Security:**
    Enforces valid CSS Custom Property fallback definitions across stylesheets.

20. **[REF: COMP-01 & COMP-02] Ten-Sector Component Topology:**
    Structures `AppOrchestrator` into ten standardized code sectors, enforcing zero-build single-file HTML monolithic architecture under 500KB.

21. **[REF: SEARCH-01c & SEARCH-02/02b/02c/03] Omni-Search Engine & Greek Normalization:**
    `stripAndNormalize` closure executes NFD Unicode decomposition, stripping accents (`/[̀-ͯ]/g`), purging HTML tags, mapping Greek `σ = ς`, and matching title numbers (`74.`) via dataset ID `d.id`. `stripHTMLForDisplay` swaps `<p>` tags for readable dashes (-) before rendering result lists.

22. **[REF: PERF-01 & PERF-01c] Keyboard Navigation State Decoupling:**
    Decouples history state mutation (`setSlideHistory`) from active state update loop, wrapping side-effects in pure `jumpToSlide` closure to prevent recursive re-renders.

23. **[REF: PERF-02] O(1) Spatial State Architecture (Delta Tracker):**
    Uses `prevActiveIndexRef` pointer to demote old marker and promote new target marker, reducing spatial rendering complexity by 99.8%.

24. **[REF: PERF-03 & PERF-03b] Kinetic HTTP Brakes (Anti-DDOS / Proxy Armor):**
    `map.stop()` aborts active flight frames during rapid navigation. Secondary map overlays set `updateWhenZooming: false` and `updateWhenIdle: true`, freezing HTTP tile pings to slow IIIF proxies (`allmaps.xyz`) until camera motion stops.

25. **[REF: PERF-04] The Transmission Clutch (Map Debouncing):**
    `debouncedIndex` transmission clutch suspends heavy spatial math until a 100ms pause in keystrokes is detected.

26. **[REF: PERF-05] MarkerCluster Bulk Ingestion Engine:**
    Geometries collect in invisible JavaScript array (`bulkClusterMarkers`), executing a single `clusterLayer.addLayers()` call post-loop.

27. **[REF: PERF-06] Singleton Hoisting:**
    `_globalTmCtx` singleton instantiated once on script load serves as permanent zero-leak mathematical reference for global canvas calculations.

28. **[REF: PERF-07] Global DOM-Based Filter Purge:**
    Purged global DOM HTML filters in favor of localized regex closures (`safeStripHTML`).

29. **[REF: PERF-12] Scroll-Tracking Indexing:**
    `MediaViewer` uses native CSS `scroll-snap-type: x mandatory` with passive `scrollLeft` indexing for touch swiping.

30. **[REF: PERF-24] Cross-Browser Axis Pinning:**
    X-axis `.timeline-axis` uses pure CSS structural anchoring (`position: absolute; bottom: 0; left: 0; right: 0; height: 28px`), locked to 100% track container height.

31. **[REF: PERF-25] Shrink-Wrapped Swimlane Matrix:**
    Swimlanes use fixed baseline height (`laneHeight = 24px`), allowing horizontal scrolling to mask overflows without vertical collapse.

32. **[REF: PERF-28] Axes Density Throttle:**
    Restricts major ticks to 6-12 occurrences per screen width (~120px spacing), controlling minor ticks via `minorCount`.

33. **[REF: PERF-29] One-Indexed Monthly Drift Protection:**
    Chronological stepping operates on `getDate() - 1`, forcing monthly/yearly major ticks to render on the 1st of calendar periods.

34. **[REF: PERF-31] Real-Time Geometric Culling:**
    Calculates visible pixel boundaries before rendering Ticks, bypassing off-screen iterations.

35. **[REF: PERF-33] Synchronized Boot Camera:**
    Boot camera executes `fitBounds` first to paint geometry, followed by `activeIndex` marker `flyToBounds` to dived to `maxAutoZoom`.

36. **[REF: PERF-34] Concurrent Priority Sorting:**
    Concurrent events sharing exact millisecond start times use secondary fallback to Spreadsheet Row ID (`a.id - b.id`).

37. **[REF: PERF-35] Passive Dimension Caching (Anti-Layout Thrashing):**
    `ResizeObserver` linked to `useRef` passively caches container pixel width, allowing `onScroll` loops to run pure JS math without triggering browser layout recalculations.

38. **[REF: PERF-36] Universal URL Parameter Memoization:**
    `getOmniParam` URL parsing isolates strictly to initial `useEffect` boot sequence, caching parameters into state.

39. **[REF: PERF-37 & PERF-38] Transmission Clutch (Search Debouncing):**
    `searchQuery` input buffers through a 250ms `setTimeout` clutch before updating `debouncedSearchQuery`, protecting main thread from Virtual DOM over-rendering.

40. **[REF: PERF-40] Off-Screen DOM Culling Matrix:**
    Evaluates chronological viewport boundaries with a `viewPadMs` buffer (50% screen width). Out-of-bounds timeline nodes return `null`, securing 60fps scrolling.

41. **[REF: PERF-41] Kinetic Camera Orchestrator (Time-to-Pixel Binding):**
    Decouples Time domain from Pixel range. Caches `scrollTargetPayloadRef`, transforms container width, and uses `useLayoutEffect` to calculate pixel coordinates and snap scrollbar synchronously before paint.

42. **[REF: PERF-42] Exact Node Geometry Sub-Pixel Math:**
    `getExactNodeScrollPos()` algorithm intercepts target Node ID, recalculates Z-stack sequence for `xOffset`, extracts `pxWidth`, and computes Cartesian pixel center of node.

43. **[REF: PERF-43] Active-Only Duration Clamp:**
    Kinetic camera cluster evaluation reads `endDate.max` exclusively for active target node, ensuring micro-events inside macro-durations trigger deep zoom.

44. **[REF: PERF-44] O(1) Absolute Time-Axis Centering:**
    Calculates `((itemStartMs - renderMinTime) / renderTimeRange) * trackW - (containerW / 2)`, guaranteeing `startPct` drop-line aligns with vertical median of viewport in $O(1)$ time.

---

## CHAPTER 8: HISTORIOGRAPHICAL METHODOLOGY & SOURCE PHYSICS

1. **[REF: METH-01] The Triangulation and Reliability Matrix:**
   Resolves spatial, temporal, and narrative conflicts through multi-modal triangulation (Data, Investigator, Methodological). Applies 12-tier reliability hierarchy: Government Archives (120 pts) and History Books (110 pts) dictate baseline truth, overriding Biographies (90), Periodicals (80), Documentaries (70), Podcasts (60), Digital News (50), Online Sources (40), Blogs (30), Recommendations (20), and Oral Histories (10 pts). Added metadata modifiers (+5 Author, +5 Publisher, +5 Date, +5 CDI, +5 RDR).

2. **[REF: METH-02] Spatial-Temporal Coercion Standards:**
   Ambiguous temporal data is coerced: morning print media = 06:00; second editions = 12:00; month/year dates = first/last day bounds. Spatially: aerial transit = straight-line vectors; terrestrial transit = modern route approximations.

3. **[REF: URL-01] Dynamic URL Parameter Ingestion:**
   Intercepts CLI/URL query parameters (`?source=`, `&gid=`, `&bgid=`, `&slide=`, `&date=`, `&mapzoom=`, `&theme=`). `getOmniParam()` sanitizes `amp;` corruptions natively and supports hash routing (`#/?key=val`).

---

## CHAPTER 9: CARTIMAP EXHAUSTIVE GLOSSARY

| Term / REF Tag | Category | Technical & Methodological Specification |
| :--- | :--- | :--- |
| **Z-Stacking Density Engine** `[REF: TL-18]` | Timeline / Map Physics | An $O(1)$ algorithmic sequence offsetting concurrent chronological events via CSS `calc()` injections (`+6px` X, `+4px` Y) to prevent text and geometry eclipsing. |
| **O(1) Spatial State Architecture** `[REF: MAP-03 / PERF-02]` | Map Physics | A dictionary-based caching strategy (`markersRef`) tracking only the delta between previous active marker and target marker, dropping navigation rendering complexity by 99.8%. |
| **Omni-Splitter Matrix** `[REF: MED-11 / ETL-11]` | Data Pipeline | A Regex interceptor (`/\||?
/`) utilized during CSV ingestion to safely flatten multi-value cells (Media, Captions, Credits, Tags) 1:1 without fracturing URLs. |
| **Flex-Greed Typographic Capping** `[REF: UI-48]` | Responsive Layout | Responsive flexbox logic capping narrative text at `max-width: 95ch`. Unused screen real estate on ultrawide monitors expands Map and Media panes (`flex: 1 1 0`). |
| **Ghost-Caliper** `[REF: TL-23]` | Timeline UI | Inactive duration ribbons rendering as open inverted Π markers with `border-left: 3px`, `border-right: 3px`, `border-bottom: 2px` and repeating linear gradient transparent fills. |
| **Dual-Tone Barber Pole** `[REF: TL-29]` | Timeline UI | GPU-rendered repeating linear gradient weaving Active color (`#007acc`/`#28a745`) with EDTF Gold (`#ffb300`) uncertainty into a 4px/8px dashed drop-line. |
| **Temporal Ghosting (Breathing Map)** `[REF: MAP-06]` | Cartography | Dynamic map filtering tracking Timeline visible bounds `[visibleLeftMs, visibleRightMs]`, attenuating out-of-bounds map pin opacity to 20% and detaching them from cluster counts. |
| **Stacked Pin** `[REF: MAP-02b]` | Cartography | Custom Leaflet marker adorned with a numeric badge, deployed when multiple distinct events share identical `[Lat, Lon]` coordinates. Clicking triggers spiderfy animation. |
| **Vibe-Monitor** `[REF: DIAG-01]` | Diagnostics | Floating, resizable HUD telemetry modal exposing data fetch statuses, row counts, active variable inspection, and real-time error log streams. |
| **Floorless Woven Matrix** `[REF: TL-28]` | Timeline UI | Anchors all duration ribbons directly to `bottom: 0` without lower CSS borders, relying on `mix-blend-mode: multiply` and GPU `-webkit-mask-image` (70px drawn, 30px erased). |
| **Segmented CSS Mask-Rhythm** `[REF: TL-28]` | Timeline UI | GPU mask pattern instructing browser to render a 70px/30px visible/invisible rhythm across duration ribbons, creating typographic breathing room. |
| **Weighted Gravity Matrix** `[REF: TL-30]` | Timeline Physics | An $O(N^2)$ sorting loop placing highest frequency tags at `laneIdx = 0` (top) and pushing rare orphaned tags to bottom swimlanes, preventing typographic crowding near X-axis. |
| **Αραίωση (Ghost-Hatch)** `[REF: TL-23]` | Timeline UI | Maximizes transparent spacing within CSS repeating linear gradients (1.2px stroke, 22.8px transparent gap) to render sparse duration ribbons. |
| **Parallel Racing Stripe** `[REF: UI-191]` | Timeline UI | Continuous 3px vertical drop-line (2px Burnt Amber core, 1px Sapphire Blue anchor shadow) signaling EDTF uncertainty on Active events without gradient clipping. |
| **White-Label Theme Expansion** `[REF: UI-193]` | UI Architecture | Decouples UI surface colors into global `--tm-` CSS Custom Property matrix controlled by `ThemesT` database tab. |
| **Cursor-Relative Tooltip Clamping** `[REF: TL-34]` | Timeline Physics | Intercepts `e.clientX` over duration ribbons, projecting tooltips exactly where user hovers, clamped (`Math.max(125, Math.min(x, width - 125))`) to prevent edge-clipping. |
| **Luminous Shadow Matrix** `[REF: TL-35]` | UI Styling | Sub-pixel box-shadow glow using higher-luminosity RGB counterparts (Soft Cyan for Sapphire Blue), preventing optical "mud" and simulating light radiation. |
| **Dynamic Hardware Scrollbar Detection** `[REF: UI-194]` | UI Architecture | A mathematical mechanism (`offsetWidth - clientWidth`) used to detect the exact pixel width of the host operating system's native scrollbar, injecting it as a CSS variable to prevent Z-index occlusion by fixed overlays. |
| **Fluid Flex-Wrap Topology** `[REF: UI-195]` | Layout Engineering | A CSS Flexbox methodology that relies on `margin-left: auto` and `flex-wrap`, allowing dynamic metadata (like multiple locations) to stack cleanly without crushing adjacent fixed-width elements. |
| **Absolute Anchor Hanging Indents** `[REF: UI-196]` | Typography | Google Sheets ETL outputs `display: flex` DOM structures isolating emojis into non-shrinking columns (`flex-shrink: 0; width: 1.2rem`) adjacent to text body. |
| **70%/70% Elastic Movable Border** `[REF: UI-67/68]` | Responsive UI | Flex allocation assigning Date and Pills wrapper `flex: 1 1 100px; max-width: 70%`, allowing long Place pills or EDTF dates to claim up to 70% container width. |
| **Dual-Signature Modification Protocol (DSSMP v3.0)** `[REF: ARCH-01 / PROT-01]` | Engineering SCM | Mandatory 6-phase engineering pipeline governing client-side JS/CSS modifications, requiring formal cryptographic approval (`έγκριση`) prior to code generation. |

---

## CHAPTER 10: HISTORICAL VERSION MILESTONES & BASELINE PROGRESSION

- **`v8.17.3-b606` (2026-10-12):** Recalibrated swimlane top padding clearance to 6px (`TimelineScrubber`) `[REF: UI-66]`; expanded `formatSmartDate` zero-width space replacements (`​`) to commas, closing brackets `]`, and closing braces `}` `[REF: ETL-10]`.
- **`v8.17.3-b605` (2026-10-06):** Configured 2D minimum-lines ribbon flex allocation (`flex: 2 1 300px` Date / `flex: 1 2 140px` Pills) `[REF: UI-63/64]`; added 14px top swimlane padding clearance `[REF: UI-65]`.
- **`v8.17.3-b604` (2026-10-06):** Side-by-side flex allocation and intra-pill right-aligned wrapping.
- **`v8.17.3-b600` (2026-10-06):** Single-file HTML monolith consolidation (`cartimap-v8.17.3-b600.html.js`).
- **`v8.17.2 Series (b592–b599)` (2026-10-06):** OverviewGantt Strategy A card header, EDTF soft breaks, and choice set leg event propagation fixes.
- **`v8.17.1-b591` (2026-10-06):** Solid opaque active card fill (`#b3e2c2`) `[REF: UI-46]`, normal typography weight (`500`) with pure black text (`#111111`) securing 11.8:1 WCAG AAA contrast `[REF: UI-47]`.
- **`v8.17.1-b590` (2026-10-06):** Purged `⏱️ Duration Lane` sticky column text header `[REF: TL-34]`, steeper 75% trapezoid clip-path `[REF: TL-35]`, color-matched active hexagon `[REF: UI-45]`.
- **`v8.17.1-b589` (2026-10-06):** Purged white separator band `div` `[REF: TL-33]`, bottom-up zebra striping `[REF: UI-43]`, slate track bed `#f8fafc`.
- **`v8.17.1-b588` (2026-10-06):** Equal height track partitioning (`totalTracks = laneCount + 1`) `[REF: TL-32]`.
- **`v8.17.1-b587` (2026-10-06):** Emerald active state parity (`#28a745` / `#b3e2c2`) across map, TOC, and scrubber `[REF: TL-30]`.
- **`v8.17.1-b585/b586` (2026-10-06):** Primary chronological event sorting `[REF: DATA-12]`, sparser 24px rotating vector hatching `[REF: TL-28]`, borderless Leaflet polygon swatches in legend.
