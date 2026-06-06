# CarTiMapper Changelog
All notable changes to this project will be documented in this file.

## [v7.0.7] - 2026-06-06
### Changed
- **DOM Filter Eradication:** Purged the legacy `stripHTML` DOM-dependent utility. Substituted all calls natively via local component closures using lightweight regex logic, securing the engine against fatal `ReferenceError` crashes during high-velocity timeline scrolling.
### Fixed
- **Virtual Subtitle Preservation:** Timeline labels and Map Tooltips no longer aggressively squash text. If a Title contains a virtual subtitle within a `<p>` tag, the engine intelligently substitutes the paragraph break for a semantic dash (` - `) before dropping the underlying HTML nodes.

v7.0.6 - Layout Axis Synchronization & Parser Invocation Fix

* **Version Bump:** Advanced App to v7.0.6, Styles to v5.0.1, Globals to v2.0.3, and AppOrchestrator to v2.0.6.
* **ESM Namespacing Fix:** Transpilation via `esm.sh` exports `edtf` as the default function. Directly calling `edtf.parse()` was failing silently and causing a lethal data purge (the "No valid temporal data" crash). The engine now executes `edtf(cleanEdtf)` directly, restoring chronological data parsing.
* **Global Engine Modes Restored:** Reverted the aggressive purge of the legacy parser. The global toggle ('Auto', 'Strict EDTF', 'Legacy') is maintained. It strictly enforces row-by-row isolation based on the global state without triggering per-record fallback loops.
* **Resizer / Layout Physics Fix:** The JavaScript Resizer hooks possessed an `isDesktop` toggle that had been disconnected from the CSS. Both CSS layout geometry and JS Delta calculations are now universally hard-locked to follow the Master Blueprint. Desktop matrix enforces `flex-direction: row` natively pinning Text to the left and Visual panes to the right. Desktop primary resize math correctly pulls horizontally, and secondary resize correctly drags vertically.


## [v7.0.5] - 2026-06-06
### Changed
- **Strict Chronological Engine Modes:** Abolished per-record fallback. Introduced `dateEngineMode` state (`auto`, `edtf`, `legacy`). On boot, the app scans the `start edtf` column and automatically locks into the highest available standard. Added a dropdown to the Settings Modal for manual overrides. 
### Fixed
- **Legacy Date Inversion:** The legacy parser now mathematically obeys `dateLocale`. Selecting `en-US` cleanly swaps the `dParts.at()` index targeting, fixing the bug that inverted Days and Months. 
- **EDTF Visual Formatting:** Decoupled EDTF strings from the `toLocaleDateString` formatter. They now display their raw literal text directly, preventing visual confusion with the localized legacy date strings.

v7.0.4 - ESM Bootloader Crash Fix (EDTF Transpilation)

* **Version Bump:** Advanced App to v7.0.4 and Globals to v2.0.1.
* **Fatal Boot Crash Diagnosed:** Identified a fatal ES Module loader crash that resulted in a completely blank white screen and bypassed the React Error Boundary. 
* **Unpkg Node.js Incompatibility:** The `edtf.js` package was being fetched via `unpkg`. Because `edtf.js` utilizes Node.js bare-specifier imports, the browser's native ESM loader threw a Syntax Error and aborted script execution before Preact could mount.
* **ESM.sh Transpilation:** Rerouted the EDTF import through `https://esm.sh/edtf`. This guarantees on-the-fly transpilation of the Node.js module into a browser-compatible payload, allowing the engine to successfully boot and mount the application.

## [v7.0.3] - 2026-06-06
### Fixed
- **The "Missing Bracket" Markdown Bug (Patch .3):** Identified the root cause of the Preact compiler crashes. The text generation parser was mistaking hardcoded Javascript array indices (``, `[1]`) for markdown reference links and silently destroying them before they reached the `.html` file.
- **ES2022 Architecture Update:** Completely eradicated standard array bracket referencing from the `AppOrchestrator` and `TimelineScrubber`. Rewrote all numerical string splitting (Dates) and Mobile Touch Kinetics (`e.touches`) to utilize `Array.prototype.at(index)` and Array Destructuring. This makes the code fundamentally indestructible to text parsers. 

## [v7.0.2] - 2026-06-06
### Fixed
- **Fatal Boot Crash (Patch .2):** Executed a full manual sweep to restore missing Javascript Array Accessor brackets (``, `[1]`, `[2]`). In the prior build, these symbols were erroneously stripped from the output format, causing the legacy Date parser to evaluate entire arrays instead of isolated variables (resulting in `NaN` logic and a blank white screen).
- **Touch Event Hijack:** Restored the `` array targets to `e.touches` across all UI resizers and the timeline scrubber to re-enable mobile swiping interactions.
- **Smart Date Formatting:** Restored the `sParts[2] === eParts[2]` exact comparisons within the display output engine to prevent visual concatenation errors.

## [v7.0.1] - 2026-06-06
### Added
- **Parallel EDTF Schema:** The engine now seamlessly intercepts EDTF strings from newly designated "Start EDTF" and "End EDTF" spreadsheet columns [4].
- **Mathematical EDTF Visuals:** Integrated EDTF uncertainty visuals on the X-Axis. Approximate dates render with radial gold gradients, uncertain dates render with dashed `#ff4500` borders, Sets render as transparent gold bounding boxes, and Lists render as sub-dots along a baseline span.
- **Global Styles (v5.0.0):** Deployed updated CSS block containing Hexagon Arrow Typographic Envelopes (`clip-path`) and strict hardware bounds for the timeline.

### Fixed
- **Fatal Boot Crash (Patch .1):** Hotfixed a critical syntax destruction bug in the legacy date parser where empty array indices crashed the Preact engine and caused a blank white screen.
- **Touch Kinetics:** Restored stripped `e.touches` array targets to resolve broken touch-zoom event handlers on mobile viewports.

### Changed
- **Major Version Sync:** Advanced App to `v7.0.0` (hotfixed to `v7.0.1`), AppOrchestrator to `v2.0.1`, TimelineScrubber to `v25.0.1`, and GlobalStyles to `v5.0.0`.
- **Indentation Protocol:** Hardened entire codebase to adhere to a strict 8-character base indentation rule for major blocks.

v7.0.0: The Chrono-Engine Update (EDTF Integration)

- [FEATURE] Integrated `edtf.js` via ESM import to natively parse Level 0, 1, and 2 ISO 8601-2 Extended Date Time Formats.
- [ARCHITECTURE] Bypassed need for strict build tools, maintaining the zero-build, <500KB constraint.
- [UI/UX] Timeline Engine now dynamically resolves overlapping temporal limits using absolute `min` and `max` EDTF boundaries.
- [UI/UX] Replaced standard timeline dots with semantic geometry:
  * Solid red for precise historical marks.
  * Gold glowing `<radialGradient>` for approximate (~) markers.
  * Orange-Red dashed `<circle>` for uncertain (?) markers.
  * `<rect>` Probability Bands for single-choice Sets [].
  * Multi-point Constellations for inclusive Lists {}.
- [UI/UX] Duration lengths now project discrete horizontal spans directly on the X-axis, featuring linear gradients for open-ended intervals (../).
- [DATA] Engine receives un-coerced, pristine strings directly from the Extracts Combined Formula v6.1.2 without requiring local JavaScript artifact scrubbing.



### [v6.8.26] - Desktop Pointer Drag Kinetics

**MediaViewer (v2.11.7):**
*   **[UI-181] Pointer DOM Interception:** Injected explicit React pointer events (`onMouseDown`, `onMouseMove`, `onMouseUp`) into the Media Carousel. Added a 1.5x friction multiplier to calculate desktop mouse deltas. 
*   **[UI-182] Snap-Scroll Decoupling:** Added dynamic `.is-dragging` CSS class injection during pointer drag. This temporarily strips CSS `scroll-snap-type: x mandatory` to prevent violent engine stuttering, resulting in buttery smooth desktop image panning.
*   **[PERF-35] Image Ghosting Annihilation:** Passed `draggable="false"` and `user-select: none` to the DOM `<img />` tags, physically preventing the browser from attempting to drag the image asset itself off the canvas during swipe routines.

### [v6.8.25] - Typographic Restoration & Margin Sealing

**Global Styles (CSS):**
*   **[UI-51] 50/50 Split Reset:** Modified the root `--primary-split` variable from `55%` down to `50%`, enforcing a perfectly symmetrical initial geometry between the Narrative and Visual columns on wide viewports.
*   **[UI-179] Inner Boundary Cages:** Injected strict `max-width: 100%; box-sizing: border-box; overflow: hidden;` rules directly into the `#app-layout` and `.timeline-pane` nodes. This stops the internal flex grids from physically pushing the absolute root container outward, fully sealing the phantom grey/black browser margins.

**ContentSlider (v4.4.1):**
*   **[CRASH-04] Transpiler Cleansing:** Eradicated invalid `{/* */}` JSX comments from the `htm` template literal, terminating the bug that caused literal engine instructions to render as physical text blocks in the UI.
*   **[UI-49] Typographical Alignment Matrix:** Remapped the padding architecture. The 55px Maximize button "keep-out zone" is now applied to the top-level sticky header wrapper, allowing the internal `85ch` envelope to securely center itself. This mathematically guarantees the Ribbon and the Title lock flush to the exact same left-axis, while symmetrically overhanging the `65ch` text block.

### [v6.8.24] - Typographic Envelopes & Density Rendering

**ContentSlider (v4.4.0):**
*   **[UI-49] Master Alignment Wrap:** Re-architected the header to utilize a unified `85ch` bounding box. The Date strings and Title headers now correctly share an absolute left-aligned margin, eliminating the previous staggered indentation while preserving the symmetrical text overhang.

**TimelineScrubber (v24.3.0):**
*   **[TL-18] Concurrent Stacking Physics:** Injected a `stackRegistry` algorithm into the map loop. Exact concurrent events (same time, same tag lane) are now mathematically fanned out in a cascading `6px x 4px` geometric stack, exposing hidden event densities previously masked by pure overlapping absolute positioning. 

**AppOrchestrator:**
*   Manually incremented `APP_VERSION` string to `'v6.8.24'`.

### [v6.8.23] - Absolute Geometry Locks

**Global Styles (CSS):**
*   **[UI-179] Absolute DOM Lock:** Replaced `#tm-root` `width: 100% / height: 100vh` parameters with `position: absolute; top: 0; bottom: 0; left: 0; right: 0;`. This hardware-level bounding box entirely eradicates the sub-pixel left and bottom margin bleeding caused by CSS percent/viewport miscalculations.

**ContentSlider (v4.3.3):**
*   **[UI-69] Decoupled Ribbon Architecture:** Extracted `.metadata-ribbon` from the centered `.title-header-container`. The ribbon now executes fluidly across 100% of the pane width, allowing the Pills to strike the absolute right edge of wide viewports.
*   **[UI-84] The Button Keep-Out Zone:** Injected a strict `padding-right: 55px` into the decoupled metadata ribbon to mathematically prevent right-flushed pills from colliding with the absolute-positioned Maximize toggle button.

### [v6.8.21] - UI/UX Physics Implementation

**Global Styles (CSS):**
*   **[UI-178] Root Boundary Lock:** Applied `height: 100vh; overflow: hidden;` to `#tm-root` and normalized `html, body` dimensions to eradicate phantom vertical scrollbars and sub-pixel left-margin grey bleed.

**VibeMonitor (v2.1.16):**
*   **[DIAG-05] Fluid Telemetry Matrix:** Demolished the rigid `1fr 1fr` CSS grid. Deployed a fluid Masonry flexbox configuration, allowing tracked variables to densely pack themselves based on string length, eliminating dead UI zones.
*   **[DIAG-04] Resize DOM Anchoring:** Bound the OS-level `resize: both` vectors to a new React `size` state. The drag-handler now intercepts and locks the current bounding box dimensions, preventing Virtual DOM reconciliation loops from snapping the monitor back to its default size when moved.

**ContentSlider (v4.3.1):**
*   **[UI-49] Typographic Title Overhang:** Decoupled the `.slide-desc` (`max-width: 75ch`) from the Title/Header container (`max-width: 90ch`), forcing symmetric visual overhangs for headers.
*   **[UI-69] Strict Axis Ribbon Wrapping:** Wrapped Places and Tags in an isolated flex-wrapper with `margin-left: auto`. This permanently locks the Date to the left (`flex-shrink: 0`) while forcing all metadata pills to fluidly wrap on the right-hand alignment axis.

**AppOrchestrator (v1.55.1):**
*   **[CRASH-03] Phantom Node Eradication:** Stripped rogue `{/* GLOBAL MODALS */}` JSX comments from the template literal. This terminates the parser collision that was injecting invisible text nodes into the DOM and causing the bottom "black ribbon" overflow.

### [v6.8.17] - Architectural Global Liberation (Multi-Block Patch)

**AppOrchestrator (v1.55.0):**
* **[ARCH-01] Global Status Bar Extraction:** Amputated the `.unified-status-bar` from the `ContentSlider` viewport. Elevated it structurally into `#app-layout` directly above the `.resizer-dyn-timeline`. The Status Bar now acts as an omni-present, structural dividing beam traversing the full width of the application window. It is permanently immune to `.visual-pane` maximizations. 
* **[UI-175] Telemetry Z-Index Escape:** Ripped the `<VibeMonitor />` out of the `.map-pane` flex-cage and hoisted it to the absolute root level of `#tm-root`. Telemetry panels now globally overwrite all pane resizers and interior map components flawlessly.
* **[UI-176] Universal Modal Hardware Anchoring:** Expanded the inline `z-index: 10001` mandate to encompass the `About` and `Search` modals (and their backdrops). Extracted their DOM state logic from `ContentSlider` into `AppOrchestrator` to ensure they bypass nested CSS flex stacking contexts. 

**MapViewer (v4.1.10):**
* **[PERF-33] Synchronized Boot Camera:** Re-engineered the marker bounding logic on application startup. Introduced a strict latency differential (delaying the active marker `flyToBounds` cycle until the initial `fitBounds` paint concludes). This geometrically guarantees that the camera actively dives to the `activeIndex` target upon boot at the precise `maxAutoZoom` depth, ignoring initial un-focused state payloads.

**ContentSlider (v4.3.0):**
* **[UI-177] Fluid Metadata Wrapping:** Extinguished the restrictive `white-space: nowrap` horizontal cage on the `.metadata-ribbon`. The global spatial wrapper is now configured to `flex-wrap: wrap;`. Locations string pills containing massive text strings will gracefully stack secondary labels (Tags) vertically, preserving absolute UX safety margins inside the text block.

**VibeMonitor (v2.1.14):**
* **[DATA-04] Exact Millisecond Diagnostics:** Abolished string sanitization inside the diagnostic readout. Telemetry for `startDate` and `endDate` fields now yields strict, high-fidelity `val.toISOString()` payloads (e.g., `2026-05-02T14:30:00.500Z`), empowering absolute validation of sub-second chronological offsets.

### [v6.8.16] - Telemetry Expansion & Temporal Ceilings (Block Patch)

**TimelineScrubber (v24.2.15):**
* **[PERF-32] Absolute Density Capping:** Injected a `Math.max()` hard ceiling into the `targetMsPerMajorTick` calculation (`Math.max(pixelDensityTarget, timeSpan / 12)`). This algorithm strictly caps the rendering engine at a maximum of 12 Major Ticks per viewport across all zoom depths and all monitor widths, permanently eliminating X-Axis clutter.
* **[UI-171] Contextual Day Overrides:** Upgraded the string formatter logic on `hour` and `minute` scale configs. The engine now reads the global span of the viewport (`visibleTimeSpanMs > 24 Hours`). If true, but the scale demands an hourly tick at midnight (`getHours() === 0`), it unconditionally overrides the hour text and outputs the Short Date (e.g., `12 May`). This preserves daily context when zooming out horizontally.
* **[UI-172] Unconditional Physical Sub-Ticks:** Decoupled the rendering of the `1px` vertical minor tick mark from the collision logic controlling its text label. The comb-tooth geometric axis now renders every single minor increment flawlessly, while typography is selectively culled above it.

**VibeMonitor (v2.1.13):**
* **[UI-173] Dynamic Variable Inspection:** The Telemetry modal is no longer a static readout. Injected a Configuration Mode (`⚙`) that mathematically scans the `activeSlide` DOM node and arrays all available CMS fields. 
* **[UI-174] Telemetry Persistence:** Checkbox selections are now strictly bound to `localStorage.getItem('tm_telemetry_fields')`. Custom user tracking profiles securely survive across hard page reloads and cross-session navigation.

### [v6.8.15] - Stacking Contexts & State Persistence (Block Patch)

**AppOrchestrator (v1.54.8):**
* **[UI-170] Universal Z-Index Domination:** Stripped CSS reliance for modal overlays. Injected absolute, hardware-accelerated inline styles (`z-index: 10001` for modals, `z-index: 10000` for the backdrop) directly into the DOM tree. This surgically overrides all isolated stacking contexts initiated by the Flex-Cages (`.map-pane` and `.visual-pane`), unconditionally preventing Leaflet tiles or Layer menus from clipping through the settings interface on mobile and tablet arrays.
* **[PERF-31] Unified Storage Persistence:** Re-wired the `polygonOpacity` state parameter. Converted its initial hardcoded bootstrap to a `localStorage` parser, and bound the DOM slider's `onInput` event directly to a `localStorage.setItem` stringify array. All five engine settings are now entirely sticky and immediately recoverable across cross-session reloads.

### [v6.8.15] - X-Axis Hardware Anchorage (Block Patch)

**TimelineScrubber (v24.2.13):**
* **[PERF-30]** **Absolute Axis Hardware Anchoring:** Stripped the volatile JavaScript `ResizeObserver` math calculating the `top` position of the X-Axis (`top: ${containerHeight - 28}px`). Injected pure CSS structural anchoring directly into the track container (`position: relative; height: 100%;`). This permanently bypasses the DOM rendering race condition, guaranteeing the absolute timeline ruler (`bottom: 0`) flawlessly anchors to the hardware floor of the scrolling pane across all browser engines, regardless of initial boot latency or collapsed flex-boundaries.
* **[UI-167]** **Hour/Minute Modulo Formatting:** Integrated a unified string truncator for both major and minor ticks. Time scales operating on standard hour/minute rules now perfectly adhere to the geometric rule: if the tick aligns perfectly with an hour (`getMinutes() === 0`), it suppresses the minutes (`14h`). If it intersects an hour block (`getMinutes() !== 0`), it completely strips the hour identifier, isolating the exact minute delta (`:15`).

### [v6.8.14] - Axes Density Matrix & Center-Mass Anchoring

**TimelineScrubber (v24.2.12):**
* **[PERF-28] Density Throttling & Scale Overhaul:** Abandoned the static 200px threshold. Adjusted `targetMsPerMajorTick` to mathematically enforce 6-12 major ticks per viewport (`120px` target base). Completely rebuilt the `scaleConfigs` array to inject explicit `minorCount` parameters, guaranteeing 5-12 minor ticks per major block across all zoom hierarchies.
* **[UI-164] Absolute Center Anchoring:** The rendering loop now pre-calculates the exact temporal midpoint of the viewport (`viewportCenterMs`). It evaluates the generated major ticks and assigns the full `DD/MM/YYYY` label *exclusively* to the single tick mathematically closest to absolute center-mass, completely eliminating edge-clipping.
* **[UI-165] Minor Tick Modulo Decluttering:** Implemented an index-based rendering mask for minor tick labels. While the physical 1px vertical tick marks always render, the text strings are heavily suppressed: even `minorCount` arrays utilize modulo logic (`minorIndex % 2 === 0`) to alternate labels, while odd arrays isolate and label only the exact median tick.
* **[UI-166] Granular Delta Truncation:** Engineered a string-truncation mask for minor ticks operating within minute-level scales. The leading hour is stripped entirely, outputting pristine temporal deltas (e.g., `:15`, `:30`, `:45`) to drastically reduce horizontal character footprint and prevent overlapping.
* **[PERF-29] 1-Indexed Month Alignment:** Re-engineered the day-stepping algorithm to utilize a 1-indexed date foundation (`setDate(Math.floor((iterDate.getDate() - 1) / step) * step + 1)`). This mathematically guarantees that major ticks perfectly anchor to the 1st of the month during macro-level zoom limits, resolving native JS zero-index drift.

### [v6.8.13] - X-Axis Hardware Anchorage (Block Patch)

**TimelineScrubber (v24.2.11):**
* **[PERF-27]** **Absolute Axis Hardware Anchoring:** Stripped the volatile JavaScript `ResizeObserver` math calculating the `top` position of the X-Axis (`top: ${containerHeight - 28}px`). Replaced it with pure CSS structural anchoring (`position: absolute; bottom: 0; left: 0; right: 0;`) inside the `.timeline-track-container`. This permanently bypasses the DOM rendering race condition, guaranteeing the timeline ruler flawlessly anchors to the hardware floor of the scrolling pane across all browser engines, regardless of initial boot latency.

### [v6.8.11-2] - Stable Geometry Reversion & Intelligent Maximize

**TimelineScrubber (v24.2.10):**
* **[PERF-26]** **Geometric Baseline Restoration:** Hard-reverted the swimlane `laneHeight` to the proven static `24px` constant. This restores the native CSS fluid shrink-wrapping of the timeline track container and permanently eliminates the dynamic stretching distortion from previous builds.
* **[UI-160]** **Hexagon Mathematics Reversion:** Restored the original `v6.7.5` `clip-path` polygon formula (`calc(50% - (var(--lane-h) / 2)...`). Event blocks wrapping multi-line text now seamlessly expand downward while maintaining perfect geometric symmetry on the left-facing arrow point, gracefully anchoring to the vertical drop-line without shearing into a parallelogram.
* **[UI-161]** **Media Icon Re-Alignment:** Decoupled the `.hasMedia` SVG indicator from the text flex-flow. It is now absolutely positioned (`left: 2px; top: 50%; transform: translateY(-50%)`) to sink perfectly inside the negative space of the left-facing hexagon point, guaranteeing zero interference with textual alignment.

**AppOrchestrator (v1.54.7):**
* **[UI-162]** **Intelligent Timeline Maximize:** Overhauled the Timeline Maximize button logic to respect absolute data density. The engine now pre-calculates the exact `timelineRequiredHeight` based on the dataset's active tag count (`laneCount * 24 + 40`). Toggling Maximize explicitly opens the drawer to this exact required pixel height—flawlessly framing all active swimlanes—rather than arbitrarily consuming the viewport. Toggling it off flawlessly restores the drawer to its collapsed state.
* **[UI-163]** **Absolute Pane Defaults:** Refined the root CSS initialization variables and the `Reset Layout` logic to strictly enforce the requested `55% / 50% / 10%` spatial split (Text / Map+Media / Timeline). The timeline now remains comfortably out of the way on boot until the user explicitly requests more vertical space.

### [v6.8.11] - Absolute Spatial Matrix & Z-Index Liberation

**TimelineScrubber (v24.2.9):**
* **[PERF-24]** **Cross-Browser Axis Pinning:** Abandoned `bottom: 0` CSS anchoring, which inherently conflicts with Firefox's native scrollbar height deductions. Implemented a `ResizeObserver` to extract the true `clientHeight`, plotting the `.timeline-axis` via absolute JS topography (`top: ${containerHeight - 28}px`). This mathematically guarantees the horizontal chronological ruler never drops below the visible CSS clipping mask on any engine.
* **[PERF-25]** **Liquid Swimlanes via ResizeObserver:** Re-engineered the lane height division mathematics (`Math.max(24, (containerHeight - 38) / laneCount)`). By binding this computation to the `ResizeObserver` payload rather than relying on CSS flex-grow limits, the timeline flawlessly expands and contracts to fill the drawer in real-time, strictly obeying the new axis breather margins.
* **[UI-157]** **Absolute Hexagon Drop-Line:** Rebuilt the `.event-group` absolute bounding box. The vertical tracking line now mathematically anchors exactly between the dead-center of the active hexagon and the absolute top pixel edge of the chronological axis, permanently eliminating "floating" trapezoids.
* **[UI-158]** **X-Axis Margin Safety Threshold:** Injected a `60px` geometric safe-zone (`viewLeftEdge + 60`) into the rendering loop. The algorithmic assignment of the Full Date string now forces the label to seamlessly shift to the next viable Major Tick before the text string can physically crash into the left-hand viewport margin.

**MapViewer (v4.1.8) & AppOrchestrator (v1.54.6):**
* **[UI-159]** **Z-Index Layer Menu Liberation:** Resolved the Tablet clipping collision by surgically decoupling the Map container's CSS properties. `.map-pane` and `.visual-pane` are now commanded to `overflow: visible; z-index: 30`. The Leaflet tile engine itself is trapped inside a new, absolute-positioned child node (`overflow: hidden; z-index: 1;`). This flawlessly traps the interactive map vectors while liberating the absolute-positioned Layers Menu, allowing it to render beautifully over the adjacent Media and Text viewports.

### [v6.8.10] - Architectural Reversion & Native Geometric Locks

**AppOrchestrator (v1.54.6):**
* **[UI-153]** **Absolute Pane Defaults:** Deprecated the volatile window-measure JS hooks that were hijacking the `.core-viewports` initial flex rendering. Hard-locked the `:root` equivalent CSS variables back to standard baseline parameters (`--primary-split: 55%; --secondary-split: 50%; --timeline-height: 10%`), guaranteeing a pristine boot sequence. The `Reset Layout` command successfully snaps back to these exact metrics.

**TimelineScrubber (v24.2.8):**
* **[PERF-22]** **Hexagon Mathematics Reversion:** Fully purged the `v6.8.9` `clip-path` hack. Reinstated the original, flawless geometric formula: `clip-path: polygon( 0 calc(50% - (var(--lane-h) / 2) + 0.5px), var(--diag-w) 0, 100% 0, 100% 100%, var(--diag-w) 100%, 0 calc(50% + (var(--lane-h) / 2) - 0.5px) );`. 
* **[PERF-23]** **Static Swimlane Anchorage:** Abolished the liquid `laneHeight` divisor. Re-locked the primary constant to `const laneHeight = 24;`. Swimlanes no longer stretch arbitrarily, preserving pure physical scale inside the drawer.
* **[UI-154]** **Exact Maximize Framing:** Refactored the `Maximize Timeline` button logic. It no longer attempts to hijack the timeline pane to an arbitrary `100%` height. The core engine dynamically calculates `requiredTimelineHeight = (laneCount * 24) + 40` during data digestion. Expanding the drawer now perfectly snaps the height parameter to this exact pixel value, framing the active swimlanes flawlessly without triggering internal flexbox collapse.
* **[UI-155]** Lifted the `.hasMedia` SVG icon out of the flex-stack entirely. Assigned it absolute coordinates (`left: 2px; top: 50%`) to let it optically sink perfectly into the negative geometric triangle left by the left-facing hexagon point.

**ContentSlider (v4.2.8):**
* **[UI-156]** Restored the `CarTiMapperLogo` typographical hierarchy. Re-locked the parent wrapper strictly to `<div style="height: 22px;">` in the `context="status"` return block, forcing `align-items: baseline` to perfectly match the ascender and descender boundaries of the adjacent textual string.

### [v6.8.9] - Liquid Height Restoration & Layout Reset Protocol

**AppOrchestrator (v1.54.4):**
* **[UI-147]** Engineered a global `Reset Layout` command sequence within the main `☰ Menu` UI. Clicking the reset trigger fires a DOM dispatch loop that instantly zero-states the `--primary-split`, `--secondary-split`, and `--timeline-height` CSS variables back to their exact defaults (`50%`, `50%`, `20%`), guaranteeing a flawless recovery mechanism if mobile users accidentally distort the fluid panes.

**TimelineScrubber (v24.2.6):**
* **[PERF-20]** **Liquid Swimlane Restoration:** Reinstated the dynamic mathematical equation calculating the height of each tag lane (`Math.max(24, (containerHeight - 33) / Math.max(1, orderedTags.length))`). This perfectly synchronizes the JS rendering engine with the `min-height: 100%` pure-CSS constraint of the parent drawer, guaranteeing the swimlanes structurally stretch and compress relative to the current resizer height without generating graphic voids.

**ContentSlider (v4.2.6):**
* **[UI-148]** Repaired the `CarTiMapperLogo` baseline typographic alignment bug. Re-locked the SVG wrapper inside the `context="status"` return block to exactly `<div style="height: 22px;">`. This acts as an absolute physical boundary, forcing `align-items: baseline` to render the graphic flush from ascender to descender against the neighboring text strings.

### [v6.8.8] - Structural Bounds & Precision Mechanics Patch

**AppOrchestrator (v1.54.3):**
* **[UI-136]** **Flex-Shrink Boundary Hardening:** Instructed `.map-pane` to operate strictly on `flex: 0 0 var(--secondary-split)` and injected absolute `min-height: 0; min-width: 0; flex-shrink: 0;` boundaries to both the map and media panes. This constructs an indestructible structural cage, permanently preventing high-resolution native imagery from crushing the map viewport into a `0x0` state on desktop displays.
* **[UI-137]** Removed hardcoded JS variable overrides (`appRef.current.style.setProperty`) from the boot sequence, successfully delegating baseline dimension initialization entirely to the CSS `:root` node rendering tree.

**ContentSlider (v4.2.5):**
* **[UI-138]** **Status Bar Micro-Compression:** Shrunk horizontal padding inside `.status-btn-text` to `6px`, and reduced the internal central `.status-left` gap to a dense `2px`. This successfully clears the left geometric overhang on restrictive portrait screens (1080px width), allowing the Status Logo lockup to completely bypass the central UI cluster.
* **[UI-139]** **Back Nav Path Re-Calculation:** Executed a mathematical adjustment of the SVG `<path d="M 12 4 A 8 8 0 1 0 20 12">`. It now traces a true 270-degree counter-clockwise arc, yielding a perfectly exposed top-right quadrant gap that unmistakably reads as a standard rewind icon, rather than an incomplete circle.
* **[UI-140]** **Status Bar Ascender-Descender Lock:** Explicitly defined the Status Bar SVG bounds to exactly `16px`, forcing the bounding box to perfectly mimic the ascender height (top of 'C') to descender height (bottom of 'p') of the adjacent 0.85rem `CarTiMapper` brand typography.
* **[UI-141]** Reverted `aboutData.title` in the `AppOrchestrator` splash screen pipeline to standard "CarTiMapper", maintaining instant core brand exposure during data ingestion loops. Increased the About window Core Engine SVG graphic base size to `240px`.

**MediaViewer (v2.11.4):**
* **[UI-142]** **Empty Space Spotlighting:** Adjusted the `.media-pane` background from absolute black to a softer slate (`#1e1e1e`) augmented with a dot-matrix overlay (`radial-gradient(#333 1px, transparent 1px)`). The `<img>` flex container is injected with an absolute center soft white `radial-gradient` acting as an optical spotlight. This visually decouples high-aspect ratio vertical portraits from the dark graphical void behind them.
* **[UI-143]** Converted harsh black media-carousel action buttons to frosted glassmorphism elements (`background: rgba(255,255,255,0.15)`), harmonizing perfectly with the new slate backdrop matrix.

**TimelineScrubber (v24.2.5):**
* **[PERF-19]** **X-Axis Spatial Memory Logic:** Rewrote the primary rendering loop algorithm (`visibleLeftMs`). It now dynamically tracks the temporal scroll coordinate limit on the horizontal plane. The very first Major Tick to clear this scrolling boundary is mathematically granted the full date string (`isFirstVisibleMajor`), guaranteeing one persistent chronological label is always visible without crashing into surrounding labels.
* **[UI-144]** **Minor Tick Kill-Zone Reduction:** Compressed the rendering threshold mask for minor ticks from `75px` to a localized `35px` radius (`distCurrent < 35 || distNext < 35`). This guarantees unsuppressed hours and minutes gracefully render deep within day-level zoom hierarchies, seamlessly avoiding the full-date major tick strings.
* **[UI-145]** **Active Drop-Line CSS Re-Architecture:** Abrogated volatile relative JS pixel math determining the vertical length of the timeline drop-indicator. The drop-line and the triangle vector are now bound to pure absolute coordinates (`bottom: 0`). The `.event-group` parent itself is mathematically pushed to `bottom: 28px`—effectively locking the lower bound of every active event perfectly to the absolute top pixel edge of the 28px horizontal Axis strip.
* **[UI-146]** Lifted the `.hasMedia` SVG indicator outside of the typographical flex-flow entirely, assigning it absolute coordinates (`left: 6px; top: 50%`) to let it optically center within the inner-left triangular point of the `.event-block` geometric hexagon.

### [v6.8.7] - Timeline Fluidity Expansion & Global CSS Variables

**TimelineScrubber (v24.2.4):**
* **[UI-134]** **X-Axis Padding Buffer:** The `.timeline-track-container` now applies explicit `padding-bottom: 33px;` physics. This mathematically forces the bottom-most swimlane to rest exactly 5px above the sticky chronological `timeline-axis`, restoring perfect visual hierarchy and preventing event geometry from touching the background numbers.

**AppOrchestrator (v1.54.2):**
* **[UI-135]** **Global CSS Boot Stabilization:** Refactored the DOM boot sequence to prevent initial frame flickering on the `timeline-pane` wrapper. The global `--primary-split`, `--secondary-split`, and `--timeline-height` CSS variables are now physically hardcoded inside a `useEffect` hook that executes immediately after the main `appRef` is attached to the DOM, explicitly bypassing CSS parsing latency and guaranteeing accurate initial spatial math.

### [v6.8.6] - Hotfix: Omni-Parser Crash
* **[CRASH-05]** **ReferenceError Eradicated:** Corrected a fatal syntax typo (`newSearchParams` to `new URLSearchParams`) inside the `getOmniParam` function in `AppOrchestrator`, preventing the engine from crashing during the deep-link initialization sequence.

### [v6.8.5] - Timeline Fluidity Restoration & Telemetry Polish

**TimelineScrubber (v24.2.3):**
* **[PERF-16]** **Structural Reversion (Swimlane Height):** Deprecated the mathematical height division equation. Reverted `laneHeight` to a hardcoded constant (`24px`). Restored native CSS `min-height` wrapping to the `.timeline-pane`, allowing the drawer to hug the data organically without generating distorted, oversized lane geometries.
* **[UI-126]** **X-Axis Spatial Decluttering:** 
    * Deployed a strict proximity-collision clamp (`distCurrent < 55`). The renderer calculates the absolute pixel distance between minor ticks and surrounding Major Ticks, completely suppressing minor strings before they overlap the full Date string.
    * Overhauled the `minorLabel` output matrix. If the active scale is `hour`, the algorithm detects on-the-hour marks (`getMinutes() === 0`) and truncates the string from `22:00` to just `22`. This eliminates redundancy and massively declutters the horizontal axis during localized viewing.

**ContentSlider (v4.2.3):**
* **[UI-127]** Refined the Global Back SVG icon (`[↺]`). Re-plotted the mathematical arc to `a8.5 8.5` and terminated the path early, generating a wide geometric gap that distinctly reads as a "Rewind Arrow" rather than a broken circle.
* **[UI-128]** Upgraded the Status Bar `CarTiMapperLogo` bounds. Hard-locked the SVG wrapper to `22px` height and enforced `align-items: baseline` on the adjacent text block, creating a pristine lockup that matches the top of the 'C' to the descender of the 'p'.
* **[UI-129]** Restructured the 'About Modal' separators. Stripped the `border-bottom` beneath the logo and injected a `border-top: 1px solid #eee` immediately *above* it, physically sealing the Dataset Overview block from the Application Telemetry block.

**AppOrchestrator (v1.54.0):**
* **[UI-130]** Purged the dynamic `aboutData.title` string injection from the Splash Screen boots sequence, ensuring the `CarTiMapper` brand identity commands visual presence regardless of upstream data latency.

### [v6.8.4] - Hotfix: Timeline Physics Rescue

**TimelineScrubber (v24.2.2):**
* **[CRASH-04]** **ReferenceError Eradicated:** The `v6.8.3` structural reversion accidentally orphaned the `onScroll` event definition while leaving the listener attached to the `.timeline-scroll-wrapper` DOM node, triggering a fatal ReferenceError on initialization. The `onScroll` math function has been re-injected, restoring passive view-edge coordinate tracking without crashing the application boot sequence.

### [v6.8.3] - State Resurrection & Timeline Rollback Patch

**AppOrchestrator (v1.53.0):**
* **[UI-109]** Resurrected the decoupled Settings Modal (`#settings-modal`).
* **[UI-110]** Re-injected the `showButtonText` state variable (Icon-Only Minimalist Mode), binding it to `localStorage` and a new checkbox within the Settings Modal. Ensures text toggles seamlessly across the global navigation bar and Map HUD.
* **[MAP-91]** Engineered global `polygonOpacity` React state. Bound the slider directly into the Settings Modal and piped it into the `MapViewer` ingestion loop to allow dynamic transparency scrubbing (`0.1` to `1.0`) on spatial layers.
* **[UI-111]** Architecturally split the About Modal into semantic modules (Dataset Overview, Core Engine Identity, Usage Parameters). Injected `dangerouslySetInnerHTML` for the Dataset Title.
* **[UI-112]** Re-colored the SVG Logo `viewBox`. Abandoned `#222` absolute black for `#2c3e50` (Slate Blue) and `#546e7a` (Compass Muted Blue) to achieve professional contrast depth. Massively scaled up the 'About' logo block width to `180px` and applied a subtle drop-shadow.
* **[UI-113]** Stripped the "Core Engine" string from the CarTiMapper logo lockup to establish a cleaner typographical hierarchy. Bound the Status Bar logo width exactly to `18px` to guarantee physical alignment with the adjacent `.status-btn-text` font height.

**TimelineScrubber (v24.2.1):**
* **[PERF-14]** **Structural Reversion:** Reverted internal DOM calculating physics to the stable `v6.7.5` architecture (`.timeline-track-container` `min-width: 100%`, `height: 100%`) to eliminate the rendering collapse bug, while explicitly preserving the modernized `v6.8.2` UI window control clusters and SVG vectors.
* **[UI-114]** SVGs within control clusters are forced to `display: flex`, `align-items: center`, `padding: 0` to banish typographical baselines and guarantee absolute centering within the `.status-btn` bounds.
* **[UI-115]** Abstracted the SVG Media indicator (`hasMedia`) and mathematically repositioned it *before* the narrative string, injecting a `6px` right-margin breather to improve visual scanning.

**VibeMonitor (v2.1.3):**
* **[UI-116]** Decoupled the Telemetry Window spawn point from absolute window bounds. Injected a physical geometry check (`window.innerWidth * 0.5` on desktop) inside the `useEffect` boot sequence, causing the monitor to spawn safely over the lower right quadrant of the *Text Pane* rather than the Map/Media viewports, without disrupting the top/left drag mechanics.

**MediaViewer (v2.11.3):**
* **[UI-117]** Upgraded the aesthetic of the "Empty State" photo pane. The `#111` flat black void is replaced with a `#1e1e1e` soft slate utilizing a CSS `radial-gradient(#333 1px, transparent 1px)` dot-matrix pattern. The `<img>` node wrapper applies a subtle `radial-gradient(circle, rgba(255,255,255,0.05) 0%, transparent 70%)` spotlight, preventing high-aspect-ratio portraits from floating in absolute darkness.

### [v6.8.2] - Core Physics & UI Refinement Patch

**TimelineScrubber (v24.2.0):**
* **[UI-99]** Bound the `.timeline-axis` strictly to `position: sticky; bottom: 0;`. This magnetically anchors the time-ruler to the viewport glass, permanently preventing it from scrolling out of bounds on desktop.
* **[UI-100]** Implemented horizontal responsive hiding for minor ticks. If internal gap math evaluates to `< 28px` between minor ticks on Android/Mobile, the text nodes are natively stripped, preventing overlapping typographical illegibility while preserving the graphical ticks.
* **[UI-101]** Applied `display: flex; flex-grow: 1` to the track wrapper, forcing the swimlanes to claim 100% of available height on boot, eliminating the "top-stacking" collapse bug.
* **[UI-102]** Extracted the SVG Media indicator (`hasMedia`) and mathematically repositioned it *before* the narrative string, injecting a localized `6px` right-breather to improve cognitive scanning velocity.

**AppOrchestrator (v1.52.0) & MapViewer (v4.1.1):**
* **[UI-103]** Reconstructed the decoupled Settings Modal (`#settings-modal`).
* **[MAP-91]** Engineered global `polygonOpacity` React state. Bound the slider directly into the `MapViewer` ingestion loop to allow dynamic transparency scrubbing (`0.1` to `1.0`) on spatial layers, optimizing visual analysis.
* **[UI-104]** Overhauled VibeMonitor trajectory bounds. Hard-coded `useEffect` to spawn monitor strictly at `window.innerWidth - 340` by `window.innerHeight - 300` on boot, safely forcing it to the bottom-right corner without disrupting the `top/left` absolute drag vectors.

**ContentSlider (v4.2.0):**
* **[UI-105]** Compressed `.unified-status-bar` vertical height from `40px` to `32px`. Shrunk interactive `.status-btn` parameters to `28x28px`.
* **[UI-106]** Architecturally partitioned the About Modal into semantic modules (Dataset Overview, Core Engine Telemetry, Usage & Parameters). Injected `dangerouslySetInnerHTML` for the `aboutData.title`.
* **[UI-107]** Reconstructed the Logo-Lockup Typography. Utilized `align-items: baseline` to perfectly lock the `CarTiMapper` logotype and version integer. Stripped native bold tags from global UI.
* **[UI-108]** Rewrote the Back/Rewind (`↺`) SVG vector path to shorten the radial arc, preventing optical confusion.

### [v6.8.1] - DOM Collision & UI Standardization Patch

**TimelineScrubber (v24.1.0):**
* **[UI-89]** Swapped spatial window control order to standard OS paradigm (Minimize `[_]` ➔ Maximize/Restore `[□]`).
* **[UI-90]** Implemented strict responsive `@media (max-height: 500px)` query for Android landscape orientation. Automatically un-stacks temporal zoom controls into a horizontal flex-row to prevent bottom-axis clipping.
* **[UI-91]** Repositioned the minimized Timeline Floating Action Button (FAB) to the absolute bottom-right. Injected `env(safe-area-inset-bottom)` to guarantee OS-level chrome (Safari URL bars, Android navigation) never occludes the touch target.
* **[UI-92]** Applied `line-height: 0` and `display: block` to all SVG button containers, mathematically neutralizing phantom typographical baselines and achieving perfect pixel centering.
* **[UI-93]** Restored full-height spatial consumption for the timeline track. The outer wrapper reverts to `height: 100%`, while the inner `.timeline-track-container` dynamically scales via `min-height` based on active swimlane counts.

**MapViewer (v4.1.0):**
* **[MAP-87]** Repositioned the dynamic radar Minimap to absolute `bottom-left` (`left: 15px`), acting as a geometric counter-weight to the right-aligned zoom/layer controls.
* **[MAP-88]** Hardened the Layers overlay menu against viewport decapitation. Injected `max-height: 50vh; overflow-y: auto;`, forcing internal scrolling rather than clipping behind the `overflow: hidden` map bounds.
* **[MAP-89]** Stripped `stroke` rendering from WKT Polygons to render pure, borderless fills. 
* **[MAP-90]** Recalibrated Polyline `dashArray` to `8, 8`, enforcing a perfect 1:1 pixel/gap ratio for maximum contrast over complex basemaps.

**ContentSlider (v4.1.0) & AppOrchestrator (v1.51.0):**
* **[UI-94]** Upgraded the Splash Screen data injector. Replaced generic hardcoded text with active parsing of the Headless CMS payload (`aboutData.title`). Massively scaled the SVG logo to `500px` (clamped to `80vw`).
* **[UI-95]** Architecturally partitioned the About Modal into three semantic hierarchies: Dataset Overview, Core Engine Telemetry, and Usage & Parameters (restoring Deep-Link URL instructions).
* **[UI-96]** Re-engineered the Back (`↺`) SVG navigation icon. Shortened the geometric path arc to widen the white-space gap, ensuring it reads distinctly as a directional arrow at mobile scales.
* **[UI-97]** Purged legacy `|` CSS border pipes from the temporal Span readout in the Status Bar.
* **[UI-98]** Stripped all native `font-weight` (bolding) from the global Status Bar About button. Flex-anchored the version integer to the bottom (`align-items: flex-end`).

**System Telemetry (VibeMonitor v2.1.1):**
* **[PERF-13]** Overhauled spatial drag math. Deprecated `bottom` calculation vectors and anchored the monitor strictly to `top` and `left` viewport client coordinates, permanently neutralizing the mathematical inversion bug that launched the HUD off-screen during upward drags.

### [v6.8.0] - The Architectural Consolidation Compile
*   **Core UI / Engine:**
    *   **[UI-80]** Purged custom/local overlays from the `DEFAULT_BASEMAPS` registry. Standardized global WebGIS basemaps (Carto, Esri, OSM, Protomaps).
    *   **[UI-82]** Ripped out all OS-dependent emojis across the entire platform. Replaced with raw, color-inheriting SVGs for cross-platform contrast and dimensional stability.
    *   **[UI-87]** Deployed strict CSS resets (`-webkit-appearance: none`) and "phantom hitboxes" to all interactive buttons to prevent Android text-scaling bloat while preserving 44px+ mobile touch targets.
*   **MapViewer (v4.0.0):**
    *   **[MAP-85]** Integrated dynamic, on-demand loading for MapLibre GL JS to support WebGL rendering of Protomaps vector tiles.
    *   **[MAP-86]** Rerouted vector rendering to consume a local `style.json` to enable advanced cartographic layer casing and dynamic zoom interpolation.
*   **TimelineScrubber (v24.0.0):**
    *   **[UI-85]** Refactored control clusters. Split spatial window controls (Minimize/Maximize) from temporal navigation (Zoom/Lock).
    *   **[UI-86]** Engineered "Drawer" collapse mechanics. Added a Floating Action Button (FAB) to restore the timeline when minimized to `0px`.
    *   **[UI-84]** Added an SVG media indicator to timeline event blocks if the associated data contains photos or video.
*   **MediaViewer (v2.11.0):**
    *   **[UI-83]** Extracted external source links and the active image counter from individual carousel nodes. Locked them to a floating, top-right spatial axis for consistent accessibility.
    *   **[PERF-12]** Implemented passive `onScroll` tracking to update the active media index, allowing the browser GPU to handle CSS scroll-snapping natively.
*   **System Telemetry:**
    *   **[UI-81]** Upgraded the `VibeMonitor` into a persistent, draggable HUD. Replaced absolute coordinates with fixed z-indexing to prevent clipping beneath the map canvas. Added a standard `[ X ]` close control.

### [v6.7.5]
* **Style Engine (style.json v1.0.0) [MAP-86]:** Engineered and deployed a custom MapLibre-compatible stylesheet for Protomaps vector data. 
* **Cartographic Upgrade:** Implemented Layer Casing for minor roads and major highways, allowing for dynamic pixel-width scaling across zoom levels 8 through 18.
* **Safety & Versioning:** Embedded a `metadata` object block at the root and layer levels to provide in-line documentation and version tracking without violating strict JSON syntax rules.

### [v6.7.2]
* **AppOrchestrator (v1.50.1) [MAP-81]:** Deployed a native URI decoding mechanism (`decodeURIComponent`) within the `Papa.parse` Web Map Service (WMS) extraction matrix. This intercepts and cleans double-encoded URL characters (e.g., converting `%3A` back to `:`) originating from user-sniffed Network payloads. This sanitization prevents literal string collisions within the Leaflet `L.tileLayer.wms()` WebGL rendering engine.

### [v6.7.1]
* **AppOrchestrator (v1.50.0) [MAP-80]:** Updated the `DEFAULT_BASEMAPS` schema and the `Papa.parse` block to ingest `format` and `wmsLayer` metadata. Injected the Dipylon 'Karten von Attika (Kaupert)' map configuration into the default registry.
* **MapViewer (v3.30.0) [MAP-80]:** Refactored the `activeOverlays` rendering loop. Engineered a conditional router that intercepts WMS definitions and redirects them to the `L.tileLayer.wms` method, enabling real-time, bounding-box-driven institutional tile generation alongside standard XYZ overlays.

### [v6.7.0]
* **AppOrchestrator (v1.49.0) [UI-72]:** Deployed `maxPane` and `expandedTimelineHeight` global states. Added a heavily scoped `<style>` block to execute state-driven CSS Flexbox overrides for maximum layout expansion, replacing the need for JS-based width calculations. Disabled pane resizers when a maximization state is active.
* **MapViewer (v3.29.0) [UI-72]:** Injected the `[⛶]` expansion SVG into the Unified HUD, mapping directly to the `setMaxPane` toggle.
* **MediaViewer (v2.10.0) [UI-72]:** Added the expansion SVG to the absolute-positioned top-right floating array.
* **ContentSlider (v3.20.0) [UI-72]:** Added the expansion SVG to the top-left status bar next to the Settings toggle.
* **TimelineScrubber (v23.18.0) [UI-72]:** Injected the `isTimelineExpanded` boolean toggle into the bottom-left map controls. Deployed the dynamic `useEffect` math calculation to multiply active lanes by lane-height, pushing the result to the Orchestrator's `expandedTimelineHeight` state.

### [v6.6.8]
* **AppOrchestrator (v1.48.0) [UI-71]:** Upgraded the CMS registry parser to ingest a `DefaultOpacity` column, defaulting to `1.0` if null or malformed.
* **MapViewer (v3.28.0) [UI-71]:** Added the `overlayOpacities` state dictionary. Injected an isolated range slider into the active overlay HUD. Bound the Leaflet `setOpacity()` method to a `useEffect` synchronization loop, granting users physical sub-pixel control over layer transparency.

### [v6.6.7]
* **AppOrchestrator (v1.47.0) [CMS-06]:** Expanded the Google Sheets CMS parser to ingest three new columns: `Active`, `AttrText`, and `AttrLink`. Deployed a Lazy Boolean regex evaluator to safely parse empty CMS cells into inactive layer states.
* **MapViewer (v3.27.0) [CMS-06]:** Rewrote the initialization `useEffect` to dynamically set `activeBasemap` and `activeOverlays` strictly from the incoming CMS state flags. Restructured the Layers Menu DOM to place `AttrText` outside the interactive `<label>`, injecting `e.stopPropagation()` into the anchor tags to prevent layer-toggling event collisions.

### ChangeLog [v6.6.6]
* **MapViewer (v3.26.0) [CMS-05]:** Deprecated the vertically stacked attribution UI layout. Deployed an inline DOM structure, combining Map Labels and Attribution Hyperlinks onto a unified horizontal axis to reduce the Map HUD's overall vertical pixel consumption by ~40%.

### ChangeLog [v6.6.4]
* **MapViewer (v3.24.1) [CRASH-01]:** Fixed a fatal Leaflet initialization crash caused by `MarkerCluster` querying a missing `maxZoom` property. Deployed the `maxGlobalZoom` integer calculation to scan the CMS array and lock the map's absolute zoom ceiling. Upgraded all `L.tileLayer` injections to utilize `maxNativeZoom`, unlocking native tile-stretching for global basemaps beneath deep historical overlays.

### ChangeLog [v6.6.3]
* **MapViewer (v3.24.0) [UI-70]:** Deployed the vertical "Sandwich" matrix for Leaflet zoom controls. Replaced the minimalist Feather layer icon with a solid isometric SVG stack. Swapped the SVG graticule back to a universal `🌐` text emoji per design specification.

### ChangeLog [v6.6.2]
* **AppOrchestrator (v1.45.0) [CMS-02]:** Upgraded the CMS URL payload handler. The secondary fetch loop now mathematically checks incoming basemap IDs against defaults, updating bounds for existing IDs and safely appending new ones without overwriting the static global defaults.
* **MapViewer (v3.23.0) [CMS-03]:** Dismantled scattered HUD artifacts. Deployed the Unified top-right control stack (Zoom Level, Focus, Grid, Layers). Engineered the dual-state tile loop to stack unchecked `base` and arrayed `overlay` layers, forcing Leaflet Z-Index priority.

* ### ChangeLog [v6.6.0]
* **AppOrchestrator (v1.44.0) [CMS-01]:** Converted the linear data fetch into a concurrent `Promise.all()` pipeline to support the `&bgid=` URL parameter. Updated `basemapsRegistry` state to dynamically overwrite the default hardcoded array if secondary CMS data is detected. Hardcoded defaults now include the georeferenced `athens-1944` layer via Allmaps.
* **MapViewer (v3.22.0) [CMS-01]:** Decoupled internal tile configs from the static `BASEMAPS` object. The component now accepts `basemapsRegistry` as a direct prop, extracting dynamic `url`, `maxZoom`, and `attribution` bounds in real-time as the user toggles settings.

### [v6.5.1]
* **AppOrchestrator (v1.43.0) [UI-67]:** Instantiated the `showButtonText` state variable and injected its toggle controller into the Settings Modal UI to support Minimalist Mode.
* **MapViewer (v3.21.0) [UI-67, UI-68]:** Replaced the Map HUD text labels with custom Globe (Grid) and Crosshair (Zoom) SVGs. Hooked the Grid label render logic into the global `showButtonText` state.
* **ContentSlider (v3.19.0) [UI-67, UI-69]:** Injected the `margin-left: auto` fluid spacer into the Micro-Scroll Ribbon, restoring the Date (Left) / Metadata (Right) split. Replaced the Back button icon with a standard UI `↺` SVG. Wired bottom navigation buttons to the `showButtonText` toggle.
* **TimelineScrubber (v23.17.0) [UI-68, UI-69]:** Compressed the dynamic telemetry output string to `Span: X`. Replaced the emoji-based zoom locks with distinct, state-driven Padlock SVGs for immediate visual feedback.

### ChangeLog [v6.5.0]
* **GlobalStyles (v4.13.0) [UI-65, UI-66]: Deployed CSS state classes for .metadata-ribbon to control horizontal scroll concealment. Implemented UI structural elements for #search-modal, inputs, and history buttons.
* **MapViewer (v3.20.0) [DATA-05]: Injected formatPlaces() to the Tooltip render loop, strictly enforcing first-comma truncation for map labeling independently from memory.
* **ContentSlider (v3.18.0) [UI-65, UI-66]: Activated the onScroll threshold sensor for the dynamic header matrix. Engineered the Omni-Search modal component, wiring it into the bottom-right status bar in a [Search] [Back] [Counter] flex layout. Activated localStorage parsing for cross-session search history persistence.

### ChangeLog [v6.4.28]
* **AppOrchestrator (v1.42.0) [MAP-11]:** Converted the legacy UI toggle into a fully descriptive `<select>` dropdown menu labeled "Map υπόβαθρο". Added rich descriptive text for the 5 curated providers to assist user decisions.
* **MapViewer (v3.19.0) [MAP-11]:** Implemented the `BASEMAPS` Core Registry array. The Leaflet engine now safely un-mounts and mounts independent tile providers in real-time, perfectly synchronizing the UI choice across both the main geographic viewport and the minimap radar.

### ChangeLog [v6.4.27]
* **MapViewer (v3.18.0) [MAP-10]:** Implemented the Minimum Projection Math clamp to the Custom Minimap. The blue aiming viewport is now allowed to expand indefinitely when zoomed out, but will mathematically halt its contraction at exactly `30px`, ensuring perfect visibility at extreme zoom depths.
* **MapViewer:** Updated UI label on the spatial overlay button from `Lat/Lon` to `Grid`.

### ChangeLog [v6.4.26]
* **MapViewer (v3.17.2) [MAP-09]:** Resolved the "dead setting" bug in the dynamic radar. Wired the `minimapOffset` to a live `useRef` and added a standalone `useEffect` that forces the `miniMapInstance` to instantly recalculate and snap to the new zoom depth the second the user adjusts the dropdown.
* **GlobalStyles (v4.12.1) [UI-64]:** Injected a mobile-exclusive `@media` query to radically shrink the minimap to `90px` by `65px` on phones, preventing DPI multiplication from artificially inflating the module into a massive obstruction.

### [v6.4.25]
* **MapViewer (v3.17.1) [MAP-08]:** Replaced the static, frozen minimap initialization with a synchronized Dynamic Radar engine. The secondary `miniMap` instance now actively tracks the main map's `getCenter()` and applies the user-selected `minimapOffset` (from `-2` to `-8`), ensuring the blue bounding rectangle never shrinks into oblivion during deep zooms.

### ChangeLog [v6.4.24]
* **MapViewer (v2.10.0) [MAP-08]:** Deployed Dynamic Radar tracking. The minimap now actively intercepts main map pan/zoom events, scaling the blue aiming rectangle proportionately instead of shrinking into oblivion.
* **AppOrchestrator (v1.41.0) [UI-63]:** Added the `minimapOffset` state array. Injected a new `<select>` dropdown into the Settings Modal allowing seamless selection of minimap radar depth from `-2` to `-8` levels.
* **GlobalStyles (v4.12.0) [UI-62]:** Injected the absolute geometric `!important` containment cage over `.leaflet-control-minimap`, permanently terminating the Android "Exploding Map" bug.

### ChangeLog [v6.4.22]
* **AppOrchestrator (v1.40.0) [URL-02]:** Engineered the Deep-Link Omni-Parser. Solved the "Android URL Parameter Bug" by actively scanning both URL queries and Hash strings, while natively correcting `&amp;` corruptions injected by mobile messaging applications.

### ChangeLog [v6.4.21]
* **AppOrchestrator (v1.39.2) [UI-61]:** Added `touch-action: none;` CSS physical override to all resizer elements. This successfully intercepts and blocks native Android browser scroll hijacking, unlocking perfectly fluid touch-drag resizing on tablet and mobile hardware.

### ChangeLog [v6.4.18]
* **ContentSlider (v3.17.2) [UI-58]:** Compressed the visual boundary between the sticky header metadata and the primary description body by reducing top padding to `0.2rem`.
* **MediaViewer (v2.9.0) [MED-25]:** Enhanced the native CSS media gallery swiping by injecting a `touchMove` telemetry lock. Sliding an image firmly blocks the Left/Right click-zones from triggering an accidental double-jump navigation.

### ChangeLog [v6.4.16]
* **AppOrchestrator (v1.38.0) [MED-11]:** Replaced legacy comma-based `.split(/[;,]\s+/)` logic with the Omni-Splitter (`/[\r\n]+|\\n/`). Media, Captions, and Credits now strictly delimit via new-lines, preventing URLs containing commas from fracturing.
* **AppOrchestrator:** Resolved the persistent metadata loss bug by physically mapping `media caption` and `media credit` to `mediaCaption` and `mediaCredit` inside the compiled JSON array, perfectly matching the required prop schema for the `MediaViewer` rendering loop.
* **AppOrchestrator:** Fully restored the original, mathematically complex SVG vector for the `CarTiMapperLogo`, abandoning the primitive triangle placeholder. Reapplied the 4px aesthetic spacing.

### [v6.4.15]
* **Full Application (Baseline Reconciliation):** Performed a forensic state-reconciliation against the `v6.3.10` baseline file. Successfully integrated the "Reading Room" layout architecture (v6.4.12), the Hero Overhang text pane (v6.4.11), and the Same-Day Smart Dates (v6.4.9) while completely restoring all original internal logic that was dropped during layout rewrites.
* **AppOrchestrator (v1.37.0):** Restored the `status.isFading` class injection to reinstate smooth Splash Screen transitions. Corrected CSV mapping keys from `caption/credit` to `media caption/media credit` to match the exact v6.3.10 CSV schema and revive media text. Remounted the physical `SettingsModal` and `VibeMonitor` DOM nodes. Re-bound all 15 missing state variables and navigation props (`slideHistory`, `goBack`, `isAboutOpen`, etc.) to the `ContentSlider` execution node.
* **ContentSlider (v3.17.0):** Refined the Smart Date logic, officially merging the legacy year/month deduplication logic (`15 - 18 Mar 1944`) with the new Same-Day time delta math (`15:45 — 16:00`). Restored the physical HTML blocks for the About Modal overlay, resolving the broken button trigger.

### [v6.4.14]
* **AppOrchestrator (v1.36.2) [DATA-09]:** Restored missing `caption` and `credit` extraction logic inside the CSV mapping loop. Media metadata now correctly parses and renders alongside images.
* **AppOrchestrator [DIAG-02]:** Repaired the About button visibility bug. Restored the `setAboutData` manifest injection that occurs post-fetch, ensuring the modal overlay correctly populates and renders.
* **AppOrchestrator [URL-01]:** Restored the Deep-Linking Engine. The URL interceptor once again actively reads `?slide=` and `?date=` parameters upon boot, mathematically jumping the user to the requested index before the loading screen fades.

### [v6.4.13]
* **AppOrchestrator (v1.36.1) [UI-52]:** Patched the rotation glitch. The application now actively tracks the `1024px` CSS boundary and mechanically resets all resizer variables to `50%` upon crossing it, preventing the panes from crushing during rotation or window-snapping.
* **AppOrchestrator [UI-53]:** Fixed missing `activeSlide` prop assignment that was causing media to render as undefined. Engineered the Dynamic Collapse architecture. The Media pane and secondary drag-bar now entirely vanish when no media is present, granting `100%` of the quadrant to the Map.
* **AppOrchestrator [UI-54]:** Restored the missing Timeline resizer bar, injecting "Bottom-Up" delta math to perfectly calculate container height changes.

### [v6.4.12]
* **AppOrchestrator (v1.36.0) [UI-51]:** Deployed the "Reading Room" architectural layout. Replaced legacy hardcoded grid wrappers with dynamic CSS Flexbox media queries (`<style>` block injection). On screens wider than 1024px, the text pane dynamically snaps to the left column, while the Map and Media panes stack in the right column, maximizing screen real-estate.
* **AppOrchestrator [UI-51]:** Engineered Fluid Dynamic Resizers. Primary and Secondary drag-bars instantly detect the browser's portrait/landscape mode and mathematically invert their axis tracking (X-delta vs Y-delta) on the fly, preventing navigation failure during responsive window scaling.

### [v6.4.11]
* **ContentSlider (v3.16.0) [UI-49]:** Deployed the "Hero Overhang" aesthetic. Wrapped the Sticky Header in a `max-width: 90ch` container, keeping the Date and Metadata elements visually anchored to the `75ch` narrative text column, while allowing long titles to elegantly expand past the reading margins.
* **ContentSlider [UI-50]:** Restored the physical HTML DOM nodes for the `aboutModal` overlay, fixing a UI break where the About state triggered successfully but had no physical overlay to render.

### [v6.4.10]
* **Documentation [PROT-01]:** Decoupled the ChangeLog back into a dedicated file. Embedded a strict protocol directive requiring all architectural and historical tracking to be delivered exclusively in isolated `.md` syntax blocks to prevent UI formatting corruption.
* **ContentSlider (v3.15.0) [UI-39]:** **CRITICAL FIX:** Resolved the Sticky Header failure. Removed the infinitely stretching `.content-scroll-area` intermediate wrapper. The header is now a direct child of the `overflow-y` parent container, mechanically guaranteeing it freezes at `top: 0` during active scrolling.
* **ContentSlider [UI-48]:** Refined typographical and geometric metadata hierarchies. The Date string was stripped of bold styling (`font-weight: 400`). Places and Tags were relocated into a dedicated Flexbox column governed by `align-items: flex-end`, forcing them to stack perfectly flush against the right-hand boundary.

### [v6.4.9]
* **Documentation [PROT-01]:** Decoupled documentation into two distinct files (`Master Blueprint` and `ChangeLog`). Appended a strict directive requiring all documentation to be delivered exclusively in `.md` format.
* **ContentSlider (v3.14.0) [UI-39]:** Reordered the Sticky Header. The visual hierarchy now explicitly presents Date, Places, and Tags *above* the Event Title. Compressed padding to shrink-wrap the header and maximize reading space.
* **ContentSlider [UI-47]:** Deployed the `75ch` Readability Clamp. Narrative descriptions dynamically center and restrict their maximum width on large desktop screens to prevent eye-tracking fatigue, keeping vertical scrolling intact.
* **ContentSlider [UI-32]:** Patched the same-day Smart Date bug. `15:45 — 16:00` deltas now render cleanly without duplicating the calendar date.
* **ContentSlider [UI-46]:** Shifted the `☰ Menu` button to the absolute left edge of the status bar. 
* **AppOrchestrator (v1.35.1) [UI-46]:** Removed the hardcoded CSS gap from `CarTiMapperLogo` to align the version number flush with the text.

#### [v6.4.8]
ContentSlider (v3.11.0): * [FIX: UI-39] Consolidated the Title, Date, Place, and Tags into a unified Sticky Header. Right-aligned the Place and Tag metadata to save vertical space.

[FIX: UI-40] Injected Golden SVG vector icons for Tags.

[FIX: UI-46] Condenses Settings and Monitor triggers into a space-saving ☰ popover menu to accommodate portrait/mobile aspect ratios. Left the Arrow navigation and About buttons completely untouched.

---

### [v6.4.7] 
* **Merged and normalized

---

### [v6.4.7]
* **Project Management [PROT-02]:** Appended the "Discuss First, Code Later" directive to the Master Blueprint. All future interactions will strictly adhere to a two-step process: diagnostic strategy agreement, followed by code execution upon explicit user approval. Mechanically locks the developer AI into a diagnostic-first loop to halt version fragmentation and UI drift.

### [v6.4.6]
* **AppOrchestrator [UI-44]:** High-precision Universal Binary Translation deployed. The CSV data parser actively intercepts GitHub `/blob/` strings and mathematically forces them to `raw.githubusercontent.com` binaries, bypassing HTML wrapper page loading and serving raw image data directly to the DOM.
* **AppOrchestrator [PERF-08]:** High-precision millisecond date parsing (`ss.000`) added to strictly preserve dataset ordering during simultaneous events.

### [v6.4.5]
* **Full File:** Consolidated all experimental performance patches into a single, highly stable build.
* **MapViewer [UI-42]:** Injected a mandatory `invalidateSize()` forcing mechanism, effectively resolving the white-map tile bug by demanding Leaflet calculate its true container bounds before requesting HTTP raster data.
* **MapViewer [UI-43]:** Hardcoded strict `160px` geometric locks on the Minimap container to eliminate Flexbox aspect-ratio explosion on tablet portrait displays.
* **Architecture [PERF-07]:** Scoped `safeStripHTML` directly into map and timeline rendering loops. Eliminated external utility dependencies, resolving silent global `ReferenceError` crashes during DOM construction.

### [v6.4.4]
* **Project Management [PROT-01]:** Appended a strict Developer Protocol section to the Master Blueprint (Documentation Supremacy), legally binding the AI assistant to provide Markdown changelogs and architectural updates with every single code deployment.

### [v6.4.3]
* **TimelineScrubber (v23.17.0) [PERF-06]:** **CRITICAL FIX:** Eliminated the massive initialization freeze. Diagnosed a severe Out-Of-Memory crash caused by the repeated generation of HTML `<canvas>` objects. Hoisted the `document.createElement('canvas')` call completely out of the `formatLabelSmart` React lifecycle. The engine now uses one pre-warmed, globally immutable memory singleton (`_globalTmCtx`) to measure all 500+ timeline labels instantly.
* **ContentSlider (v3.11.0) [UI-32]:** Deployed the `formatSmartDate` engine to natively deduplicate time strings (e.g., removing redundant years/months for multi-day events and mathematically stripping `00:00` midnight signatures).
* **ContentSlider [UI-39]:** Pinned the Title and Date to the top of the UI via `position: sticky`. Moved the Metadata Dock directly below the header to establish strict geographic-first narrative hierarchy.
* **ContentSlider [UI-40]:** Injected the golden-yellow `<svg>` tag icon directly into the mapping loop so every Tag pill renders flawlessly, overriding unpredictable OS-dependent Emoji rendering.

### [v6.4.2] 
* **Map Engine Rewrite (v4.0.0):** Completely upgraded the Map architecture by combining three absolute performance safeguards:
    * **[PERF-05] Bulk Ingestion (The Boot Fix):** Instead of feeding the MarkerCluster one pin at a time, WKT arrays are collected in a temporary, invisible JavaScript array (`const bulkCluster = []`). Once the loop finishes, the array is handed to Leaflet in a single `clusterLayer.addLayers(bulkCluster)` command. The collision math runs exactly once instead of $O(N^2)$ times, dropping load times to milliseconds and resolving the CPU hang.
    * **[PERF-02] O(1) Spatial Tracker (The Memory Fix):** Re-implemented the delta tracker (`prevActiveIndexRef`). Changing slides updates exactly two mathematical targets on the map (promoting the new, demoting the old), leaving the remaining 500+ cluster objects untouched.
    * **[PERF-04] The Transmission Clutch (The Spam Fix):** Re-implemented the `debouncedIndex` (set to 100ms). Holding the arrow key flies the Timeline at 30fps, but the Map safely pauses before calculating heavy DOM cluster extractions and 3D flight geodesics, saving 99% of CPU overhead.
* **MapViewer [UI-38]:** Forced `miniMap.invalidateSize()` and strictly applied `fitBounds(bounds.pad(0.1), { animate: false })` to guarantee the minimap instantly and rigidly wraps around the specific geographic footprint of the dataset without aspect-ratio geometry conflicts.

### [v6.4.1]
* **MapViewer [PERF-04]:** Integrated the Transmission Clutch (`debouncedIndex`). Arrow-key events now decouple the Map engine from the UI by 100ms, entirely preventing event-spam from queuing hundreds of heavy DOM manipulations per second.
* **MapViewer [PERF-03]:** Implemented `map.stop()` as an absolute animation brake, physically terminating previous geodesic animation frames and preventing simultaneous camera flights from overloading the CPU thread.

### [v6.4.0]
* **MapViewer (v3.18.0) [PERF-02]:** **CRITICAL FIX:** Resolved the major memory leak and UI freeze caused by Leaflet marker thrashing. Rewrote map interaction logic from an $O(N)$ brute-force array destruction loop to a precise $O(1)$ delta tracker. Map navigation is now mathematically instantaneous.
* **MapViewer [UI-38]:** Bound the `miniMap.fitBounds()` strictly to the dataset's geographic footprint, ensuring the miniature orientation map always contextualizes the user's actual theater of operations.

---

### [v6.3.12] (Rollback Baseline)
* **AppOrchestrator (v1.35.2) [PERF-01]:** Patched a severe memory stack overflow. Keyboard arrow listeners now trigger a pure `jumpToSlide` function, preventing runaway React/Preact state loops from crashing browser tabs.
* **AppOrchestrator [UI-36]:** Ripped out the accidentally duplicated top header that was breaking the flex-grid and pushing the Map/Media panes downward.
* **ContentSlider (v3.10.0) [UI-37]:** Successfully migrated aesthetic polish (Sticky Title/Date, CSS Metadata Pills, Smart Date Deduplication) into the text rendering component.
* **ContentSlider:** Injected the mathematical SVG tag icon (`<svg>`) directly into the `slide.tags.map()` loop to ensure each individual CSS pill receives its own crisp vector path. Replaced the fuzzy ⚙️ text emoji with pristine SVG gear paths.

### [v6.3.11]
* **AppOrchestrator (v1.35.0) [UI-30]:** Injected a global event listener mapping the keyboard's Left/Right arrows to the `setActiveIndex` timeline state for hands-free carousel navigation.
* **AppOrchestrator [UI-31]:** Replaced OS-dependent "⚙️" text emoji with a resolution-independent SVG. Removed unpredictable `&nbsp;` spacing in favor of mathematical Flexbox gaps.
* **EventDetails (v3.4.0) [UI-32]:** Restored the v6.0.14 date-formatting engine to smartly collapse identical days, months, and years across temporal ranges.
* **EventDetails [UI-33 & UI-34]:** Applied the Omni-Splitter regex (`/[\r\n]+|\\n/`) to `activeSlide.tags`. Pinned the Event Title and Date to the top of the pane.
* **EventDetails [UI-35]:** Built the Metadata Dock. Rendered locations as a singular unified tag block, generating discrete CSS pill badges for temporal tags at the bottom.

### [v6.3.10]
* **TimelineScrubber (v23.16.0) [TL-17]:** Injected the `getParsedTags()` utility to intercept and flatten incoming tag arrays using the Omni-Splitter regex (`/[\r\n]+|\\n/`).
* **TimelineScrubber:** Fixed a bug where newline-delimited tags generated single, broken lane labels. The engine now correctly generates discrete background lanes.
* **TimelineScrubber:** Restored vertical spanning engine. Events with multiple tags accurately calculate their Y-axis coordinates to stretch visually across all assigned categories.

### [v6.3.9]
* **MediaViewer (v2.8.0) [MED-24]:** Refactored slides to use Flexbox Column layout. Captions sit at the absolute bottom; Images scale upward to perfectly fill space via `object-fit: contain`.
* **MediaViewer [MED-23]:** Transferred click-zone geometry to the image wrapper. Bound `pointer-events: none` to the physical image to prevent drag-ghosting during navigation clicks. Re-anchored the multi-image HUD counter via `position: absolute`.

### [v6.3.8]
* **MediaViewer (v2.7.0) [MED-20]:** Removed invasive diagnostic HTML HUD. Piped array readouts purely into the `addLog` prop for global monitoring.
* **MediaViewer [MED-21]:** Attached mathematical click zones directly to the rendered image. Clicking the left half scrolls left; right half scrolls right. Changed mouse cursor to horizontal arrows (`ew-resize`).
* **MediaViewer [MED-22]:** Natively hid the scrollbar track via inline CSS, perfectly preserving the ability to physically swipe on touch screens.

### [v6.3.7]
* **MediaViewer (v2.6.3) [MED-18]:** Upgraded the array flattening matrix to utilize the Omni-Splitter regex (`/[\r\n]+|\\n/`). Resolves concatenation bugs caused by rogue carriage returns or escaped line-feeds.
* **MediaViewer [MED-19]:** Restored native anchor (`<a>`) wrappers to `mediaCaption` and `mediaCredit`. Kept the central `<img>` element unlinked to preserve carousel left/right navigation clicks.
* **Diagnostics:** Deployed a high-contrast HUD to track rawMediaData string parsing artifacts before flattening matrices.

### [v6.3.5]
* **MediaViewer (v2.6.1) [MED-14]:** Reverted a fatal prop hallucination (`data/activeIndex` to `activeSlide`) that caused absolute void renders. Implemented safe line-break (`\n, \r\n`) delimiter execution to preserve embedded comma structures.
* **MediaViewer [MED-15]:** Synchronized metadata array indices natively 1:1 with media loop instances. Stripped `<a>` wrapper from visual renders to restore unblocked prev/next DOM telemetry.

### [v6.3.4]
* **MediaViewer (v2.5.4) [MED-11]:** Simplified delimiter parsing regex to exclusively target line-breaks (`/\r\n|\n|\r/`). Resolves critical bug where legitimate commas inside image filenames triggered destructive URL array splits (404 errors).

### [v6.3.2]
* **MediaViewer (v2.5.2) [MED-07]:** Deployed aggressive inline dimensional bounds to `<img>` renderer to mathematically prevent flex-child DOM collapse.
* **MediaViewer [MED-08]:** Upgraded the global array delimiter RegExp to `/\||\r?\n/`. Explicitly identifies and nukes trailing Windows CRLF carriage returns generated by `CHAR(10)` exports.

### [v6.3.1]
* **MediaViewer (v2.5.1) [MED-06]:** Stripped `loading="lazy"` from `<img>` generation to prevent horizontal scroll-snap intersection calculation failures. Rewrote variable interpolations to ensure proper Preact htm VDOM mapping.

### [v6.3.0]
* **MediaViewer (v2.5.0) [MED-03]:** Injected `\n` logic into parsing loop to support `CHAR(10)`. Separated Media, Captions, and Credits into synchronized parallel arrays.
* **MediaViewer [MED-04]:** Stripped HTML anchor (`<a>`) wrappers from dynamically rendered image targets to unblock invisible navigation click-zones.
* **MediaViewer [MED-05]:** Deployed dedicated Flexbox layout row, routing raw URLs into an isolated `[↗]` external link icon.

### [v6.2.8]
* **TimelineScrubber (v23.15.0) [TL-UI-16]:** Implemented the 60px Safe-Threshold algorithm. Dynamically assigns absolute date context strictly to the first major tick that physically clears 60 pixels from the left viewport edge.

### [v6.2.6]
* **TimelineScrubber (v23.13.0) [TL-UI-14]:** Recalculated `distanceToAxis`. Reduced active single-point anchor dot to 6px and offset it to center perfectly on the axis floor.
* **TimelineScrubber [TL-UI-12]:** Injected debounced `onScroll` state trigger into the wrapper element to wake React up following a manual viewport drag.
* **TimelineScrubber [TL-UI-13]:** Built collision-avoidance sub-routine. Left-aligns the `firstVisibleMajorTick` and institutes a 120-pixel rendering block for minor ticks.

### [v6.2.5]
* **TimelineScrubber (v23.12.0) [TL-ANIM-06]:** Detached Manual zooming from Auto-centering constraints. Scrolling mouse-wheel dynamically assigns cursor's coordinate as CSS stretch origin.
* **TimelineScrubber [TL-UI-11]:** Recalculated timeline geometry variables (`topPos + 5`) to integrate 5px structural top breather.
* **TimelineScrubber [TL-UI-10]:** Upgraded `isFirstRenderedTick` gate. Computes an `expectedVisibleMin` derived from active event focus.

### [v6.2.4]
* **Imports & Globals (v1.0.52) [CORE-01]:** Injected `useLayoutEffect` hook into global scope to support synchronous DOM painting.
* **TimelineScrubber (v23.11.0) [TL-ANIM-05]:** Transferred Cluster Auto-Zoom state to synchronous `useLayoutEffect`. Width stretch and scrollTo re-centering now execute in the exact same millisecond, eliminating stretch-flicker.
* **TimelineScrubber [TL-UI-09]:** Engineered `isFirstRenderedTick` gate inside the axis loop to strictly enforce full absolute date context on leading edge of viewport.
* **TimelineScrubber [UI-NUM-02]:** Wrapped active zoomLevel readout in `Math.round()`.

### [v6.2.3]
* **MapViewer (v3.17.0) [MAP-UI-01]:** Dropped mathematically inconsistent spatial multipliers from zoom indicator. HUD natively reports absolute zoom scale.
* **MapViewer [MAP-GRID-01]:** Engineered a dependency-free Micro-Graticule Engine. Parses absolute bounds and dynamically injects `L.polyline` grids synced to Leaflet `moveend` camera trigger.

### [v6.2.2]
* **GlobalStyles (v4.11.0) [TL-UI-05]:** Retained flat-edge `.event-block` boundary and preserved 8px internal vertical padding expansion to strictly support native 3-line string wrapping.
* **TimelineScrubber (v23.10.0) [TL-UI-07]:** Injected a symmetrical `top: 5px` offset into internal lane layout boundary for positive visual breather.
* **TimelineScrubber [TL-UI-08]:** Engineered Infinite Calendar Scale Matrix. Major/Minor axes calculated via dynamic Gregorian interpolation across 16 context thresholds.
* **TimelineScrubber [TL-ANIM-03]:** Deleted sub-second micro-pan `useEffect` hook. Limit transitions to native CSS width expansion post-pan to prevent DOM stutter.

### [v6.2.1]
* **GlobalStyles (v4.11.0) [TL-UI-05]:** Restored flat-edge structural geometry to `.event-block` class.
* **TimelineScrubber (v23.9.0) [TL-ANIM-01]:** Implemented 3-step delayed state machine (Highlight ➔ Smooth Pan ➔ 400ms Delay ➔ Cluster Zoom & Snap) mathematically eliminating visual stretch-whiplash.
* **TimelineScrubber [TL-UI-06]:** Rewrote timeline ruler generation loop utilizing Semantic Gregorian Calendar Engine.
* **TimelineScrubber [TL-UI-04]:** Integrated spatial collision detection to format contextual minor tick labels.

### [v6.2.0]
* **GlobalStyles (v4.10.0) [TL-UI-03]:** Recalibrated `.event-block` clip-paths and elevated `.timeline-track-container` 5px.
* **GlobalStyles [UI-TYPO-02]:** Scrubbed bold styling application-wide for neutral professional UI.
* **GlobalStyles [UI-HUD-02]:** Deployed absolute centering (`transform: translateX(-50%)`) for navigation cluster.
* **AppOrchestrator (v1.34.1) [CRASH-02]:** Passed `jumpToSlide` into ContentSlider to prevent ReferenceErrors from Modal interactions.
* **AppOrchestrator [SUB-02]:** Upgraded logic to intercept `CHAR(10)` line breaks (`\n`) and truncate sublabels at first comma.
* **MapViewer (v3.16.3) [CRASH-01.5]:** Engineered micro-parser polyfill to manually construct geometries when Wicket silently fails on `GEOMETRYCOLLECTION`.
* **MapViewer [GEO-02]:** Reduced LINESTRING weights to 2px with dashed strokes; stripped borders from POLYGON shapes.
* **MapViewer [UI-NUM-01]:** Converted zoom percentages to clean `<times>x` floats.
* **MediaViewer (v2.4.0) [MED-02]:** Bypassed anchor-wrapping for `<iframe` strings, executing dynamically as HTML.
* **MediaViewer [MED-UI-03]:** Engineered regex extraction to pull raw URLs from `<iframe src="...">` for hyperlink routing.
* **ContentSlider (v3.9.2) [DIAG-02]:** Reorganized About Modal to separate project description from active telemetry.
* **TimelineScrubber (v23.8.0) [TL-AUTO-03]:** Replaced nearest-neighbor auto-zoom with 5-event Cluster Window enforcing a 30-minute minimal span.
* **TimelineScrubber [TL-UI-04]:** Injected spatial collision detection for minor axis ticks.

### [v6.1.5]
* **MapViewer (v3.16.3) [SUB-02]:** Inserted `\n` into RegExp delimiter block to support `CHAR(10)` and dynamically truncate at first comma.

### [v6.1.4]
* **ContentSlider (v3.9.2) [CRASH-02]:** Added missing `jumpToSlide` prop assignment.
* **AppOrchestrator (v1.34.1) [CRASH-02]:** Wired `jumpToSlide` method into injection.
* **MapViewer (v3.16.1) [CRASH-01]:** Implemented `parseGeometryCollection()` polyfill to natively support non-compliant nested WKT geometries.

### [v6.1.3-2]
* **GlobalStyles (v4.9.0) [UI-TYPO-02]:** Scrubbed bold application-wide.
* **GlobalStyles [UI-HUD-02]:** Reprogrammed `.status-center` with absolute CSS positioning.
* **VibeMonitor (v2.0.0) [DIAG-01]:** Implemented Active Sensor HUD displaying location text/system version.
* **ContentSlider (v3.9.1) [DIAG-02]:** Restructured About modal flow. Injected dynamic `${APP_VERSION}` into status bar.

### [v6.1.3]
* **MediaViewer (v2.4.0) [MED-02]:** Engineered raw HTML interception loop for entire iframe tags.
* **MediaViewer [MED-UI-03]:** Built `getCleanUrl()` extractor. Captions bound to iframe snippets correctly link to source.

### [v6.2.0] (*Legacy Identifier*)
* **GlobalStyles (v4.8.0) [MED-UI-01]:** Styled `.media-meta-box a` to inherit standard weights.
* **AppOrchestrator (v1.33.0) [MED-01]:** Upgraded `parsedMedia` regex to explicitly target comma-space and semicolon-space signatures.
* **MediaViewer (v2.2.0) [MED-UI-01]:** Extracted `<img>` tags into `<a>` wrappers. Injected `.media-meta-box` container directly inside carousel items.

### [v6.1.1]
* **MapViewer (v3.16.0) [GEO-02]:** Segregated polygon and linestring styling blocks.
* **MapViewer [UI-NUM-01]:** Converted map zoom HUD to report relative scaling using `x` notation.
* **TimelineScrubber (v23.7.0) [TL-AUTO-02]:** Removed `gap > 0` exclusionary logic. Autozoom engine constructs visual cascades instead of zooming out.

### [v6.1.0]
* **GlobalStyles (v4.7.0):** Injected `.minimap-container` CSS footprint.
* **AppOrchestrator (v1.32.0):** Configured central `zoomLock` and `visibleTimeSpan` HUD properties.
* **MapViewer (v3.15.0) [MAP-12]:** Instantiated synchronized Overview Minimap bounded explicitly to dataset scope.
* **MapViewer [MAP-13]:** Deployed `L.control.scale()`. Engineered dynamic 100% calculation based on relative deviation.
* **TimelineScrubber (v23.6.0) [TL-AUTO-01]:** Remodeled Auto-Zoom engine enforcing 10px spacing with 10-minute cascade floor.
* **TimelineScrubber [TL-LOCK-01]:** Implemented Soft/Hard tracking states.
* **ContentSlider (v3.9.0) [UI-HUD-01]:** Formatted unified status bar to display semantic timeline extent readout.

### [v6.0.26]
* **GlobalStyles (v4.6.0) [MAP-UI-02]:** Overrode default Leaflet Cluster CSS to deploy Warm Segregation Palette.
* **GlobalStyles [UI-TYPO-01]:** Reconfigured `.slide-place-badge` constraints to allow dynamic multi-line text wrapping.
* **MapViewer (v3.14.0) [MAP-UI-01]:** Restored native Leaflet zoom controls.
* **MapViewer [SUB-01]:** Added dash and ano teleia to sublabels RegEx split logic.
* **MapViewer [MAP-09]:** Enabled hot-swapping between English Esri BaseMap and Local CartoDB map.
* **MapViewer [MAP-10]:** Implemented Elevation hook. Active marker removed from cluster group to guarantee visibility.
* **MapViewer [MAP-11]:** Bound `getAllChildMarkers()` to hover state to render list of swallowed location names.
* **AppOrchestrator (v1.31.0) [MAP-SET-01]:** Injected `maxAutoZoom` and `mapLocale` state variables into Settings Modal.

### [v6.0.25]
* **MapViewer (v3.13.0) [MAP-UI-01]:** Restored native Leaflet zoom controls.
* **MapViewer [MAP-09]:** Swapped CartoDB for Esri World Street Map to force English labeling globally.
* **MapViewer [MAP-10]:** Implemented Elevation hook.
* **MapViewer [MAP-11]:** Bound `getAllChildMarkers()` mapping logic.

### [v6.0.24]
* **AppOrchestrator (v1.30.1) [BOOT-CRASH-01]:** Patched critical syntax typo in Stage 1 data fetch (`new URLSearchParams`). Resolves catastrophic halting bug on Initialization.
* **ContentSlider (v3.8.1) [UI-NAV-01]:** Restored missing `slideHistory` and `goBack` properties.
* **TimelineScrubber (v23.5.0) [TL-CLAMP-01]:** Deployed mathematical span floor (minimum 24 hours).
* **TimelineScrubber [TL-CLAMP-02]:** Deployed Infinity Clamp (locks minimum time gap to 60 seconds).

### [v6.0.23]
* **AppOrchestrator (v1.30.1) [BOOT-CRASH-01]:** Patched syntax typo `new URLSearchParams`.
* **ContentSlider (v3.8.1) [UI-NAV-01]:** Restored `slideHistory`.

### [v6.0.22]
* **ContentSlider (v3.8.0) [UI-SET-01]:** Injected Settings trigger button into Status Bar.
* **ContentSlider [DATE-13]:** Upgraded `formatSmartDate` to conditionally render `HH:mm`.
* **TimelineScrubber (v23.5.0) [TL-CLAMP-01/02]:** Span Floor and Infinity Clamp logic deployed.
* **AppOrchestrator (v1.30.0) [ARCH-01]:** Implemented Two-Stage Data Pipeline caching raw PapaParse rows.
* **AppOrchestrator [DATE-11 & 12]:** Replaced `parseEuroDate` with `dynamicDateParse`, routing HH:mm:ss payloads safely.
* **AppOrchestrator [UI-SET-01]:** Injected Settings Modal UI overlay.

### [v6.0.21]
* **AppOrchestrator (v1.29.0) [DATA-08]:** Replaced fuzzy `smartGet` with high-performance `exactGet` mapper.
* **AppOrchestrator [DATA-09]:** Activated extraction for media caption/credit.
* **AppOrchestrator [DATA-10]:** Pruned unused fields (Source, Web Page) to optimize memory. Pointed subLabels logic directly at Place column.

### [v6.0.18]
* **AppOrchestrator (v1.28.1) [DATA-03]:** Expanded normalization fallbacks. Implemented rigorous `.filter()` chain to obliterate falsy arrays.
* **TimelineScrubber (v23.2.0) [UI-TL-02]:** Encapsulated Absolute Zoom Controls and Scroll Wrapper to restore architectural integrity against flexbox crushes.

### [v6.0.17]
* **MapViewer (v3.12.0) [GEO-01]:** Resolved GeoJSON inversion by deleting custom `coordsToLatLng` override. Engine trusts Leaflet's native parser.
* **ContentSlider (v3.7.0) [DATE-02]:** Augmented `formatSmartDate` logic to include `weekday: 'short'`.
* **TimelineScrubber (v23.1.0) [UI-TL-01]:** Restored complete multi-lane visualizer logic. Redesigned Zoom Controls container.

### [v6.0.16]
* **AppOrchestrator [DATE-01]:** Strict Euro/ISO Date Parser. Replaced generic `new Date()` with manual `parseEuroDate` to guarantee US-localized browsers no longer silently invert European dates.

### [v6.0.15]
* **Map Engine:** Removed redundant `flipLeafletGeometry` function.
* **Map Engine:** Fixed Sub-Label mapping inside nested WKT LayerGroups.
* **UI/UX:** Increased Splash Screen logo width to 300px. Re-introduced full-size branding logo into About modal.

### [v6.0.14]
* **Map Engine [MAP-06]:** Resolved Multipoint Sub-Label duplication bug via recursive geometry tunneling (`extractLayers`).
* **Map Engine:** Increased Y-offset of custom map tooltips to `-48px`.

### [v6.0.13]
* **Map Engine [UI-12]:** Permanently resolved double-offset CSS bug pushing Map Pins away from coordinates.
* **Branding Layout:** Replaced legacy text button in status bar with CarTiMapper Logo icon.
* **Typography Hierarchy [UI-13]:** Moved `📍 Place` metadata badge to right-hand column beneath Tags.

### [v6.0.12]
* **Branding:** Officially integrated Dark Film Hex-Frame logo. Dynamically embedded version (`v6.0.12`) into splash loader. Hex-Frame SVG added as URL-encoded Favicon.

### [v6.0.11]
* **Map Engine:** Deployed hotfix for fatal `ReferenceError` (`new URLSearchParams` typo).

### [v6.0.10]
* **Data Schema:** Expanded CSV ingestor to capture `Place` column.
* **Map Engine:** Overhauled Map Tooltip UI labeling hierarchy (`Sub-Label` -> `Place Name` -> `Event Title`).
* **UI/UX:** Added `📍 [Place Name]` spatial context badge.

### [v6.0.9]
* **Architecture:** Bumped `APP_VERSION` to `v6.0.9`.
* **Map Engine:** Diagnosed and fixed catastrophic WKT inversion bug by restoring missing `wicket.min.js` to `<head>`.
* **Architecture:** Fixed boot freeze by defaulting to Master Database URL if `?source=` is omitted.
* **Diagnostics:** Refined `VibeMonitor` telemetry to catch WKT parsing stack traces.

### [v6.0.8]
* **Map Engine [MAP-05]:** Deployed Recursive Leaflet Geometry Flipper (`flipLeafletGeometry`).
* **Diagnostics:** Wired map parser directly into `VibeMonitor` for verbosity.

### [v6.0.7]
* **Map Engine:** Removed Regex coordinate flipper.
* **UI/UX:** Added `?source=URL` parameter documentation into About modal.

### [v6.0.6]
* **Map Engine:** Deployed ultra-fast Regex Pre-Parser string flipper (Reverted in v6.0.7).
* **UI/UX:** Rebuilt `about-modal` to render reference card explaining `[URL-01]` routing parameters.

### [v6.0.5]
* **Navigation [URL-01]:** Built URL Routing Engine intercepting `?slide=X`, `?date=YYYY-MM-DD`, `?theme=dark`, `?mapzoom=X`.

### [v6.0.4]
* **Architecture:** Routed parsed WKT through `.toJson()` into `.geoJSON()` natively (Reverted in v6.0.7).
* **UI/UX:** Added `.custom-div-icon` CSS override to strip Leaflet white bounding boxes.
* **Physics:** Raised bounding box max-zoom tolerances to `16`.

### [v6.0.3]
* **Google Sheets ETL Pipeline:** Formula brought under versioning. Enforced Cartesian schema (`POINT(Lon Lat)`). Injected Two-Tier REF-TAG documentation via `LET` dummy variables (`_ref_etl`).

### [v6.0.2]
* **Google Sheets ETL Pipeline:** Wrapped GeoJSON/WKT array builders in `UNIQUE(FILTER(...))` logic to purge redundant nodes.

### [v6.0.1]
* **UI/UX:** Reassigned mapping hierarchy colors.
* **Data Schema:** Smartened ETL `col_idx=11` formula to conditionally map raw Lat/Lon into `GeometryCollection` or `GEOMETRYCOLLECTION`.

### [v6.0.0]
* **Architecture:** Major version rewrite. Replaced basic Leaflet plotting with WKT parsing (`Wicket`) and R-Tree spatial indexing (`MarkerCluster`).
* **Logic:** Built $O(1)$ memory dictionary (`markersRef`) to handle "State-Based Layer Swapping" for VIP slide focus.

### [v5.23.0]
* **Data Schema:** Updated PapaParse fuzzy ingestor to capture `clean_geo`, `sub_labels`, `priority`.
* **Media:** Hardened Media Agnosticism pipeline natively supporting YouTube iframes, HTTP links, and images within unified flex container.

### [v1.0.0 – v5.13.0] - Legacy Foundation Rollup
* **Core Layout:** Established strict Flexbox boundaries with a Unified Status Bar and 15% Ergonomic Touch Zones.
* **Timeline:** Established foundation temporal visualization replacing list navigation.
* **Cloud Data:** Hardcoded datasets replaced with live Google Sheets API Proxy fetching.
* **Genesis:** Initial concept deployment via basic Leaflet map instantiation reading hardcoded Lat/Lon arrays.
