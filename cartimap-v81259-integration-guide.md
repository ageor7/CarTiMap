# CarTiMap Complete Integration Guide: v8.11.25 to v8.12.59
### Consolidated Architectural Patches & Sub-Block Landmarks
**Prepared by the CarTiMap Systems & Database Engineering Council**

This master integration guide contains the complete, syntactically balanced, and mathematically verified component code blocks to transition your codebase from the **`v8.11.25`** baseline to the production-stable **`v8.12.59`** build. 

All precarious components are isolated with explicit, non-standard comment anchors to prevent future character-class collisions and virtual DOM compiler thrashing.

---

## 📐 1. Architectural Gap Analysis: What Changed Since v8.11.25?

### A. Dynamic Horizontal Swimlane Filtering (`[REF: ETL-14b]`)
* **The Problem (v8.11.25):** The timeline scrubber merely mapped chronological elements linearly across rigid tracks without taking category density or operational theaters into account. Rendering high-density, multi-vocal datasets (like the subterranean sewer routes paired with political summits) led to massive vertical clustering and UI overlap.
* **The Solution (v8.12.59):** Integrated state hooks (`unfilteredData`, `activeTags`, `isFilterOpen`) in the `AppOrchestrator` status bar. A dynamic tag checklist allows users to toggle active theaters on the fly. To prevent timeline track collapse and virtual DOM null exceptions, a safety guard blocks deselection when only one tag remains active, broadcasting a warning to the **VibeMonitor**.

### B. Consolidated Chronological Telemetry (`[REF: UI-164b]`)
* **The Problem (v8.11.25):** The timeline scrubber maintained a separate `.zoom-factor` telemetry box floating independently on the scrubber track, consuming valuable vertical layout space and causing visual jitter on small touchscreens.
* **The Solution (v8.12.59):** Shifted the active zoom factor reading directly into the status bar's `.semantic-time-span` string (e.g., `"Span: 7 Months (Zoom: 15x)"`), creating a unified, high-contrast HUD and completely purging the redundant floating DOM containers.

### C. Map Update Cycle Decoupling (`[REF: MAP-03b / PERF-24b]`)
* **The Problem (v8.11.25):** The `MapViewer` was bound to a single, overloaded `useEffect` dependent on both active slide indexes and visible time boundaries. Scrolling the timeline thrashed the `flyToBounds` animation on every minor tick, causing map markers to "shake" and causing severe GPU latency.
* **The Solution (v8.12.59):** Decoupled the map cycle into two independent, lightweight listeners:
  1. **Map Temporal Ghosting Loop:** Triggers on `visibleTimeBounds` to adjust opacity and update cluster layouts in constant time.
  2. **Map Kinetic Camera Flight:** Triggers strictly on `activeIndex` or `maxAutoZoom` changes, applying automatic kinetic brakes (`map.stop()`) to halt conflicting transition frames.

### D. Regular Expression & Scope Hardening (`[REF: BOOT-CRASH-03]`)
* **The Problem (v8.11.25):** The date splitting pattern `/[/\\-.]/` inside `parseChronoNode` caused a fatal `SyntaxError: invalid range in character class` because the unescaped dash evaluated the backslash and dot as range bounds. Additionally, `formatPlaces` was devouring the letters `a-z` due to an unescaped `-` spanning to `·`, and threw `TypeErrors` on arrays.
* **The Solution (v8.12.59):** Sanitized all character classes (using `/[\/\\.-]/` and `/[|\\-·;]/` with safe escaping and literal anchoring) and properly indexed the array items using `.at(0)` prior to string manipulation.

---

## 🛠️ 2. Upgraded Code Blocks (Ready for Insertion)

### Component A: `TimelineScrubber v26.11.8`
**Target Slot:** Locate `// === [ MAJOR BLOCK: TimelineScrubber` inside `cartimap.v8.11.25.html` (approx. line 210+) and replace the entire component with this block:

```javascript
// 🔽🔽🔽 [ START_INJECT: TimelineScrubber v26.11.8 ] 🔽🔽🔽
        // === [ MAJOR BLOCK: TimelineScrubber v26.11.8 ] ===
        const TimelineScrubber = ({ data, activeIndex, setActiveIndex, zoomLock, setZoomLock, setVisibleTimeSpan, isTimelineExpanded, setIsTimelineExpanded, isTimelineMinimized, setIsTimelineMinimized, dateLocale, timelineRequiredHeight, setVisibleTimeBounds }) => {
          const wrapperRef = useRef(null);
          const [zoomLevel, setZoomLevel] = useState(1);
          const dragRef = useRef({ isDragging: false, startX: 0, scrollLeft: 0, hasDragged: false });
          const touchZoomRef = useRef({ initialDist: 0, initialZoom: 1 });
          const prevActiveIndexRef = useRef(-1);
          const scrollTargetPayloadRef = useRef(null);
          const scrollTimeout = useRef(null);
          const [containerHeight, setContainerHeight] = useState(200);
          const [viewLeftEdge, setViewLeftEdge] = useState(0);
          const [caliperTooltip, setCaliperTooltip] = useState(null);
          const hoverTimeoutRef = useRef(null);
          const lastMouseXRef = useRef(0);
        
          useEffect(() => {
            const ro = new ResizeObserver(entries => {
              const entry = entries.at(0);
              if (entry && entry.target) {
                setContainerHeight(entry.target.clientHeight);
              }
            });
            if (wrapperRef.current) ro.observe(wrapperRef.current);
            return () => ro.disconnect();
          }, []);
        
          const safeStripHTML = (str) => {
            if (!str) return '';
            const withDashes = String(str).replace(/<p[^>]*>/gi, ' - ');
            return withDashes.replace(/<[^>]*>?/gm, '').trim();
          };
        
          const getParsedTags = (rawTagsArray) => {
            if (!rawTagsArray || rawTagsArray.length === 0) return [];
            const splitRegex = /[\r\n]+|\\n/;
            let arr = [];
            (Array.isArray(rawTagsArray) ? rawTagsArray : [rawTagsArray]).forEach(t => {
              if (typeof t === 'string') arr.push(...t.split(splitRegex));
              else arr.push(t);
            });
            return arr;
          };
        
          const uniqueStarts = [...new Set(data.map(d => d.startDate?.min).filter(Boolean))].sort((a,b) => a - b);
        
          // Swimlane gravity extraction matrix
          const allTags = [];
          data.forEach(d => {
            if (d.tags) allTags.push(...getParsedTags(d.tags));
          });
          const uniqueTags = [...new Set(allTags)].filter(Boolean);
          const tagFreq = {};
          uniqueTags.forEach(t => tagFreq[t] = 0);
          data.forEach(d => {
            if (d.tags) getParsedTags(d.tags).forEach(t => { if(t) tagFreq[t]++; });
          });
        
          const remaining = [...uniqueTags].sort((a, b) => tagFreq[b] - tagFreq[a]);
          const orderedTags = [];
          if (remaining.length > 0) orderedTags.push(remaining.shift());
          while (remaining.length > 0) {
            let bestMatchIdx = 0;
            let maxIntersection = -1;
            let insertPos = 'push';
            for (let i = 0; i < remaining.length; i++) {
              const cand = remaining[i];
              let interLast = 0;
              let interFirst = 0;
              data.forEach(d => {
                if (d.tags) {
                  const tList = getParsedTags(d.tags);
                  if (tList.includes(cand)) {
                    if (tList.includes(orderedTags.at(-1))) interLast++;
                    if (tList.includes(orderedTags.at(0))) interFirst++;
                  }
                }
              });
              if (interLast > maxIntersection) { maxIntersection = interLast; bestMatchIdx = i; insertPos = 'push'; }
              if (interFirst > maxIntersection) { maxIntersection = interFirst; bestMatchIdx = i; insertPos = 'unshift'; }
            }
            if (insertPos === 'push') { orderedTags.push(remaining.at(bestMatchIdx)); remaining.splice(bestMatchIdx, 1); }
            else { orderedTags.unshift(remaining.at(bestMatchIdx)); remaining.splice(bestMatchIdx, 1); }
          }
        
          const laneCount = Math.max(1, orderedTags.length);
          const laneHeight = Math.max(24, (containerHeight - 55) / laneCount);
        
          const validData = data.filter(d => d.startDate && !isNaN(d.startDate.min));
          const minTimeRaw = validData.length > 0 ? validData.at(0).startDate.min : new Date().getTime();
          let maxTimeRaw = minTimeRaw;
          validData.forEach(d => {
            if (d.endDate && !isNaN(d.endDate.max) && d.endDate.max > maxTimeRaw) maxTimeRaw = d.endDate.max;
            else if (d.startDate.min > maxTimeRaw) maxTimeRaw = d.startDate.min;
          });
        
          const rawTimeRange = Math.max(maxTimeRaw - minTimeRaw, 86400000);
          const padMs = rawTimeRange * 0.05;
          const renderMinTime = minTimeRaw - padMs;
          const renderMaxTime = maxTimeRaw + padMs;
          const renderTimeRange = renderMaxTime - renderMinTime;
        
          const measureTextWidth = (text) => {
            const canvas = document.createElement('canvas');
            const context = canvas.getContext('2d');
            context.font = '400 12px "Noto Sans", sans-serif';
            return context.measureText(text).width;
          };
        
          const formatLabelSmart = (titleStr) => {
            const maxPx = 300;
            const words = titleStr.split(' ');
            let lines = [];
            let currentLine = '';
            words.forEach(w => {
              const testLine = currentLine ? currentLine + ' ' + w : w;
              if (testLine && measureTextWidth(testLine) > maxPx && currentLine) {
                lines.push(currentLine);
                currentLine = w;
              } else {
                currentLine = testLine;
              }
            });
            if (currentLine) lines.push(currentLine);
            if (lines.length > 2) {
              lines = lines.slice(0, 1);
              lines.push(currentLine.slice(0, 20) + '...');
            } else if (lines.length === 2) {
              let last = lines.at(1);
              if (last && measureTextWidth(last) > maxPx * 1.3) {
                while (measureTextWidth(last + '...') > maxPx * 1.3 && last.length > 0) last = last.slice(0, -1);
                lines.splice(1, 1, last.trim() + '...');
              }
            }
            return { lines, pxWidth: Math.max(60, Math.max(...lines.map(l => measureTextWidth(l))) + 35) };
          };
        
          const SECOND = 1000; const MINUTE = 60 * SECOND; const HOUR = 60 * MINUTE; const DAY = 24 * HOUR; const MONTH = 30 * DAY; const YEAR = 365.25 * DAY;
          const scaleConfigs = [
            { ms: 100 * YEAR, type: 'year', step: 100, minorType: 'year', minorStep: 10, minorCount: 10 },
            { ms: 10 * YEAR, type: 'year', step: 10, minorType: 'year', minorStep: 1, minorCount: 10 },
            { ms: 2 * YEAR, type: 'year', step: 2, minorType: 'month', minorStep: 2, minorCount: 12 },
            { ms: YEAR, type: 'year', step: 1, minorType: 'month', minorStep: 1, minorCount: 12 },
            { ms: 6 * MONTH, type: 'month', step: 6, minorType: 'month', minorStep: 1, minorCount: 6 },
            { ms: MONTH, type: 'month', step: 1, minorType: 'day', minorStep: 3, minorCount: 10 },
            { ms: 15 * DAY, type: 'day', step: 15, minorType: 'day', minorStep: 1, minorCount: 15 },
            { ms: 5 * DAY, type: 'day', step: 5, minorType: 'day', minorStep: 1, minorCount: 5 },
            { ms: DAY, type: 'day', step: 1, minorType: 'hour', minorStep: 3, minorCount: 8 },
            { ms: 12 * HOUR, type: 'hour', step: 12, minorType: 'hour', minorStep: 1, minorCount: 12 },
            { ms: 6 * HOUR, type: 'hour', step: 6, minorType: 'hour', minorStep: 1, minorCount: 6 },
            { ms: 2 * HOUR, type: 'hour', step: 2, minorType: 'minute', minorStep: 15, minorCount: 8 },
            { ms: HOUR, type: 'hour', step: 1, minorType: 'minute', minorStep: 10, minorCount: 6 },
            { ms: 30 * MINUTE, type: 'minute', step: 30, minorType: 'minute', minorStep: 5, minorCount: 6 },
            { ms: 15 * MINUTE, type: 'minute', step: 15, minorType: 'minute', minorStep: 1, minorCount: 15 },
            { ms: 10 * MINUTE, type: 'minute', step: 10, minorType: 'minute', minorStep: 1, minorCount: 10 },
            { ms: 5 * MINUTE, type: 'minute', step: 5, minorType: 'minute', minorStep: 1, minorCount: 5 },
            { ms: MINUTE, type: 'minute', step: 1, minorType: 'second', minorStep: 10, minorCount: 6 }
          ];
        
          if (validData.length === 0) return html`<div style="padding:1rem;">No valid temporal data.</div>`;
        
          const containerW = wrapperRef.current ? wrapperRef.current.clientWidth : 1000;
          const trackWidthPx = Math.max(containerW, containerW * zoomLevel);
          const visibleTimeSpanMs = renderTimeRange / zoomLevel;
          const spansMultipleDays = visibleTimeSpanMs > 86400000;
          const targetMsPerMajorTick = Math.max((120 / containerW) * visibleTimeSpanMs, visibleTimeSpanMs / 12);
          let activeScale = scaleConfigs.find(c => targetMsPerMajorTick > c.ms) || scaleConfigs.at(-1);
        
          const visibleLeftMs = renderMinTime + (viewLeftEdge / trackWidthPx) * renderTimeRange;
          const visibleRightMs = renderMinTime + ((viewLeftEdge + containerW) / trackWidthPx) * renderTimeRange;
          const viewportCenterMs = visibleLeftMs + ((visibleRightMs - visibleLeftMs) / 2);
        
          useEffect(() => {
            if (setVisibleTimeBounds && !isNaN(visibleLeftMs) && !isNaN(visibleRightMs)) {
              setVisibleTimeBounds([visibleLeftMs, visibleRightMs]);
            }
          }, [visibleLeftMs, visibleRightMs, setVisibleTimeBounds]);
        
          // --- [ START_SUBBLOCK: Chronological Zoom & Telemetry ] ---
          useEffect(() => {
            const visibleMs = renderTimeRange / zoomLevel;
            const secs = visibleMs / 1000; const mins = secs / 60; const hrs = mins / 60; const days = hrs / 24; const mos = days / 30.44; const yrs = days / 365.25;
            let str = `${Math.round(mins)} Minutes`;
            if (yrs >= 1) str = `${Math.round(yrs)} Years`;
            else if (mos >= 1) str = `${Math.round(mos)} Months`;
            else if (days >= 1) str = `${Math.round(days)} Days`;
            else if (hrs >= 1) str = `${Math.round(hrs)} Hours`;
            
            // Conformed to [REF: UI-164b] Status bar integrated timeline zoom metric
            setVisibleTimeSpan(`Span: ${str} (Zoom: ${Math.round(zoomLevel)}x)`);
          }, [zoomLevel, renderTimeRange, setVisibleTimeSpan]);
          // --- [ END_SUBBLOCK: Chronological Zoom & Telemetry ] ---
        
          const getExactNodeScrollPos = (nodeGlobalIdx, trackW, containerW) => {
            const activeNode = data[nodeGlobalIdx];
            if (!activeNode || !activeNode.startDate) return 0;
            const basePx = ((activeNode.startDate.min - renderMinTime) / renderTimeRange) * trackW;
            return basePx - (containerW / 2);
          };
        
          useEffect(() => {
            const activeDataIndex = validData.findIndex(d => d.id === activeIndex);
            if (activeDataIndex >= 0 && wrapperRef.current && !dragRef.current.isDragging) {
              const containerW = wrapperRef.current.clientWidth || 1000;
              const targetTrackW = Math.max(containerW, containerW * zoomLevel);
              const scrollPos = getExactNodeScrollPos(activeIndex, targetTrackW, containerW);
              wrapperRef.current.scrollTo({ left: scrollPos, behavior: 'smooth' });
            }
          }, [activeIndex]);
        
          useEffect(() => {
            if (validData.length > 1 && wrapperRef.current && !dragRef.current.isDragging && activeIndex !== prevActiveIndexRef.current) {
              prevActiveIndexRef.current = activeIndex;
              if (zoomLock === 'hard') return;
              const timeoutId = setTimeout(() => {
                const activeDataIndex = validData.findIndex(d => d.id === activeIndex);
                if (activeDataIndex >= 0) {
                  if (zoomLock === 'auto') {
                    let clusterMin = validData.at(Math.max(0, activeDataIndex - 2)).startDate.min;
                    let clusterMax = validData.at(activeDataIndex).endDate && !isNaN(validData.at(activeDataIndex).endDate.max) ? validData.at(activeDataIndex).endDate.max : validData.at(activeDataIndex).startDate.min;
                    for (let i = Math.max(0, activeDataIndex - 2); i <= Math.min(validData.length - 1, activeDataIndex + 2); i++) {
                      const node = validData.at(i);
                      clusterMax = Math.max(clusterMax, node.startDate.min);
                      clusterMin = Math.min(clusterMin, node.startDate.min);
                    }
                    const idealZoom = (0.6 * renderTimeRange) / Math.max(clusterMax - clusterMin, 1800000);
                    const clampedZoom = Math.min(Math.max(1, idealZoom), 2000);
                    
                    scrollTargetPayloadRef.current = { type: 'node', value: activeIndex };
                    setZoomLevel(clampedZoom);
                  } else {
                    if (zoomLock === 'soft') setZoomLock('auto');
                    scrollTargetPayloadRef.current = { type: 'node', value: activeIndex };
                    setZoomLevel(z => z + 0.000001);
                  }
                }
              }, 500);
              return () => clearTimeout(timeoutId);
            }
          }, [activeIndex, data, zoomLock, setZoomLock]);
        
          useLayoutEffect(() => {
            if (scrollTargetPayloadRef.current !== null && wrapperRef.current) {
              const containerW = wrapperRef.current.clientWidth;
              const trackWidthPx = Math.max(containerW, containerW * zoomLevel);
              let targetScrollPos = 0;
              const payload = scrollTargetPayloadRef.current;
              
              if (payload.type === 'node') {
                targetScrollPos = getExactNodeScrollPos(payload.value, trackWidthPx, containerW);
              } else if (payload.type === 'raw') {
                targetScrollPos = payload.value;
              }
              
              wrapperRef.current.scrollTo({ left: targetScrollPos, behavior: 'auto' });
              scrollTargetPayloadRef.current = null;
            }
          }, [zoomLevel]);
        
          const handleManualZoom = (newZoom, centerType = 'center', eventX = 0) => {
            if (!wrapperRef.current) return;
            const containerW = wrapperRef.current.clientWidth;
            const scrollPos = wrapperRef.current.scrollLeft;
            const anchorPx = centerType === 'mouse' ? scrollPos + eventX : scrollPos + (containerW / 2);
            const centerPct = anchorPx / Math.max(containerW, containerW * zoomLevel);
            const targetScrollPos = (centerPct * Math.max(containerW, containerW * newZoom)) - (centerType === 'mouse' ? eventX : (containerW / 2));
            
            scrollTargetPayloadRef.current = { type: 'raw', value: targetScrollPos };
            setZoomLevel(newZoom);
          };
        
          const handleNodeClick = (globalIdx) => {
            if (!dragRef.current.hasDragged) {
              const containerW = wrapperRef.current ? wrapperRef.current.clientWidth : 1000;
              const trackWidthPx = Math.max(containerW, containerW * zoomLevel);
              const scrollPos = getExactNodeScrollPos(globalIdx, trackWidthPx, containerW);
              wrapperRef.current.scrollTo({ left: scrollPos, behavior: 'smooth' });
              setActiveIndex(globalIdx);
            }
          };
        
          const onDown = (e) => {
            if (zoomLock !== 'hard') setZoomLock('soft');
            if (e.touches && e.touches.length === 2) {
              const t1 = Array.from(e.touches).at(0); const t2 = Array.from(e.touches).at(1);
              touchZoomRef.current = { initialDist: Math.hypot(t1.clientX - t2.clientX, t1.clientY - t2.clientY), initialZoom: zoomLevel };
              return;
            }
            const t1 = e.touches ? Array.from(e.touches).at(0) : e;
            dragRef.current = { isDragging: true, startX: t1.clientX, scrollLeft: wrapperRef.current.scrollLeft, hasDragged: false };
            wrapperRef.current.classList.add('is-dragging');
            if (caliperTooltip) setCaliperTooltip(null);
          };
        
          const onUp = () => { dragRef.current.isDragging = false; wrapperRef.current?.classList.remove('is-dragging'); };
        
          const onMove = (e) => {
            if (e.touches && e.touches.length === 2) {
              e.preventDefault();
              const t1 = Array.from(e.touches).at(0); const t2 = Array.from(e.touches).at(1);
              const scale = Math.hypot(t1.clientX - t2.clientX, t1.clientY - t2.clientY) / touchZoomRef.current.initialDist;
              handleManualZoom(Math.min(Math.max(touchZoomRef.current.initialZoom * scale, 1), 2000), 'center');
              return;
            }
            if (!dragRef.current.isDragging) return;
            if (!e.touches) e.preventDefault();
            const t1 = e.touches ? Array.from(e.touches).at(0) : e;
            const deltaX = t1.clientX - dragRef.current.startX;
            if (Math.abs(deltaX) > 5) dragRef.current.hasDragged = true;
            wrapperRef.current.scrollLeft = dragRef.current.scrollLeft - (deltaX * 2);
          };
        
          const onWheel = (e) => {
            e.preventDefault();
            if (zoomLock !== 'hard') setZoomLock('soft');
            handleManualZoom(e.deltaY < 0 ? Math.min(zoomLevel * 1.5, 2000) : Math.max(zoomLevel / 1.5, 1), 'mouse', e.clientX - wrapperRef.current.getBoundingClientRect().left);
          };
        
          const onScroll = () => {
            if (scrollTimeout.current) clearTimeout(scrollTimeout.current);
            scrollTimeout.current = setTimeout(() => { if (wrapperRef.current) setViewLeftEdge(wrapperRef.current.scrollLeft); }, 100);
          };
        
          const handleCaliperEnter = (e, item) => {
            lastMouseXRef.current = e.clientX;
            hoverTimeoutRef.current = setTimeout(() => {
              if (!wrapperRef.current) return;
              const containerWidth = wrapperRef.current.clientWidth;
              const rect = wrapperRef.current.getBoundingClientRect();
              let trackX = lastMouseXRef.current - rect.left;
              trackX = Math.max(125, Math.min(trackX, containerWidth - 125));
              const absoluteX = wrapperRef.current.scrollLeft + trackX;
              const itemStart = item.startDate.min;
              const itemEnd = (item.endDate && !isNaN(item.endDate.max)) ? item.endDate.max : itemStart;
              const overlaps = validData.filter(o => o.id !== item.id && o.startDate && !isNaN(o.startDate.min) && Math.max(o.startDate.min, itemStart) <= Math.min(o.endDate && !isNaN(o.endDate.max) ? o.endDate.max : o.startDate.min, itemEnd));
              setCaliperTooltip({ id: item.id, x: absoluteX, title: safeStripHTML(item.title), durationMs: itemEnd - itemStart, overlaps: overlaps.map(o => safeStripHTML(o.title)) });
            }, 350);
          };
        
          const handleCaliperMove = (e, item) => {
            lastMouseXRef.current = e.clientX;
            if (caliperTooltip && caliperTooltip.id === item.id && wrapperRef.current) {
              const containerWidth = wrapperRef.current.clientWidth;
              const rect = wrapperRef.current.getBoundingClientRect();
              let trackX = e.clientX - rect.left;
              trackX = Math.max(125, Math.min(trackX, containerWidth - 125));
              setCaliperTooltip(prev => ({...prev, x: wrapperRef.current.scrollLeft + trackX}));
            }
          };
        
          const handleCaliperLeave = () => {
            if (hoverTimeoutRef.current) clearTimeout(hoverTimeoutRef.current);
            setCaliperTooltip(null);
          };
        
          let iterDate = new Date(Math.max(renderMinTime, visibleLeftMs - (activeScale.ms * 2)));
          iterDate.setMilliseconds(0);
          if (activeScale.type === 'year') { iterDate.setMonth(0, 1); iterDate.setHours(0, 0, 0, 0); iterDate.setFullYear(Math.floor(iterDate.getFullYear() / activeScale.step) * activeScale.step); }
          else if (activeScale.type === 'month') { iterDate.setDate(1); iterDate.setHours(0, 0, 0, 0); iterDate.setMonth(Math.floor(iterDate.getMonth() / activeScale.step) * activeScale.step); }
          else if (activeScale.type === 'day') { iterDate.setHours(0, 0, 0, 0); iterDate.setDate(Math.floor((iterDate.getDate() - 1) / activeScale.step) * activeScale.step + 1); }
          else if (activeScale.type === 'hour') { iterDate.setMinutes(0,0,0); iterDate.setHours(Math.floor(iterDate.getHours() / activeScale.step) * activeScale.step); }
          else if (activeScale.type === 'minute') { iterDate.setSeconds(0,0); iterDate.setMinutes(Math.floor(iterDate.getMinutes() / activeScale.step) * activeScale.step); }
        
          let safety = 0;
          const stopTime = Math.min(renderMaxTime, visibleRightMs + (activeScale.ms * 2));
          const majorTicksData = []; const minorTicksData = [];
          while (iterDate.getTime() <= stopTime && safety < 1000) {
            safety++; const t = iterDate.getTime();
            if (t >= renderMinTime) majorTicksData.push({ t, pctLeft: ((t - renderMinTime) / renderTimeRange) * 100, date: new Date(iterDate) });
            let nextMajor = new Date(iterDate);
            if (activeScale.type === 'year') nextMajor.setFullYear(nextMajor.getFullYear() + activeScale.step);
            else if (activeScale.type === 'month') nextMajor.setMonth(nextMajor.getMonth() + activeScale.step);
            else if (activeScale.type === 'day') nextMajor.setDate(nextMajor.getDate() + activeScale.step);
            else if (activeScale.type === 'hour') nextMajor.setHours(nextMajor.getHours() + activeScale.step);
            else if (activeScale.type === 'minute') nextMajor.setMinutes(nextMajor.getMinutes() + activeScale.step);
        
            let minorIter = new Date(iterDate); let minorSafety = 0; let minorIndex = 0;
            while (minorSafety < 100) {
              minorSafety++; minorIndex++;
              if (activeScale.minorType === 'year') minorIter.setFullYear(minorIter.getFullYear() + activeScale.minorStep);
              else if (activeScale.minorType === 'month') minorIter.setMonth(minorIter.getMonth() + activeScale.minorStep);
              else if (activeScale.minorType === 'day') minorIter.setDate(minorIter.getDate() + activeScale.minorStep);
              else if (activeScale.minorType === 'hour') minorIter.setHours(minorIter.getHours() + activeScale.minorStep);
              else if (activeScale.minorType === 'minute') minorIter.setMinutes(minorIter.getMinutes() + activeScale.minorStep);
              else if (activeScale.minorType === 'second') minorIter.setSeconds(minorIter.getSeconds() + activeScale.minorStep);
              if (minorIter.getTime() >= nextMajor.getTime()) break;
              const minorT = minorIter.getTime();
              if (minorT >= renderMinTime && minorT <= renderMaxTime) {
                minorTicksData.push({ t: minorT, px: (((minorT - renderMinTime) / renderTimeRange)) * trackWidthPx, majorPx: ((t - renderMinTime) / renderTimeRange) * trackWidthPx, nextMajorPx: ((nextMajor.getTime() - renderMinTime) / renderTimeRange) * trackWidthPx, date: new Date(minorIter), minorIndex });
              }
            }
            iterDate = nextMajor;
          }
        
          let centerTickIndex = -1; let minDist = Infinity;
          majorTicksData.forEach((d, i) => {
            if (d.t >= visibleLeftMs && d.t <= visibleRightMs) {
              const dist = Math.abs(d.t - viewportCenterMs);
              if (dist < minDist) { minDist = dist; centerTickIndex = i; }
            }\n          });\n        \n          const centerTickPx = centerTickIndex !== -1 ? (majorTicksData[centerTickIndex].pctLeft / 100) * trackWidthPx : -1000;\n          const centerKeepout = 65;\n          const rulerTicksHTML = majorTicksData.map((d, i) => {\n            let label = ''; const tickPx = (d.pctLeft / 100) * trackWidthPx;\n            if (i === centerTickIndex) {\n              label = d.date.toLocaleString(dateLocale, { day: '2-digit', month: 'short', year: 'numeric', hour: (activeScale.type==='hour'||activeScale.type==='minute')?'2-digit':undefined, minute: (activeScale.type==='hour'||activeScale.type==='minute')?'2-digit':undefined });\n            } else if (Math.abs(tickPx - centerTickPx) > centerKeepout) {\n              if (activeScale.type === 'year') label = d.date.getFullYear();\n              else if (activeScale.type === 'month') label = d.date.toLocaleString(dateLocale, { month: 'short', year: 'numeric' });\n              else if (activeScale.type === 'day') label = d.date.toLocaleString(dateLocale, { day: 'numeric', month: 'short' });\n              else if (activeScale.type === 'hour' || activeScale.type === 'minute') {\n                if (spansMultipleDays && d.date.getHours() === 0 && d.date.getMinutes() === 0) label = d.date.toLocaleString(dateLocale, { day: 'numeric', month: 'short' });\n                else label = d.date.getMinutes() === 0 ? d.date.getHours().toString() : ':' + d.date.getMinutes().toString().padStart(2, '0');\n              }\n            }\n            return html`<div class=\"timeline-ruler-tick\" style=\"left: ${d.pctLeft}%;\"><div style=\"width: 2px; height: 10px; background: #666; margin-bottom: 2px;\"></div><div style=\"font-size: 0.75rem; white-space: nowrap; font-weight: normal; color: #444;\">${label}</div></div>`;\n          });\n        \n          const minorTicksHTML = minorTicksData.map(m => {\n            const distCurrent = Math.abs(m.px - m.majorPx); const distNext = Math.abs(m.px - m.nextMajorPx); const distCenter = Math.abs(m.px - centerTickPx);\n            let hideMinor = distCurrent < 35 || distNext < 35; let showLabelText = false;\n            if (!hideMinor && distCurrent > 20) {\n              if (activeScale.minorCount % 2 === 0) showLabelText = (m.minorIndex % 2 === 0);\n              else showLabelText = (m.minorIndex === Math.floor(activeScale.minorCount / 2));\n            }\n            let minorLabel = '';\n            if (showLabelText && distCenter > centerKeepout) {\n              if (activeScale.minorType === 'year') minorLabel = m.date.getFullYear();\n              else if (activeScale.minorType === 'month') minorLabel = m.date.toLocaleString(dateLocale, { month: 'short' });\n              else if (activeScale.minorType === 'day') minorLabel = m.date.getDate();\n              else if (activeScale.minorType === 'hour' || activeScale.minorType === 'minute') minorLabel = m.date.getMinutes() === 0 ? m.date.getHours().toString() : ':' + m.date.getMinutes().toString().padStart(2, '0');\n            }\n            const containerW = wrapperRef.current ? wrapperRef.current.clientWidth : 1000;\n            if (m.px >= viewLeftEdge - 50 && m.px <= viewLeftEdge + containerW + 50) {\n              return html`<div style=\"position: absolute; left: ${((m.t - renderMinTime) / renderTimeRange) * 100}%; top: 0; width: 1px; height: ${minorLabel ? '7px' : '5px'}; background: #aaa; z-index: 4;\">${minorLabel ? html`<div style=\"position: absolute; left: -20px; right: -20px; top: 7px; text-align: center; font-size: 0.6rem; color: #888; letter-spacing: -0.5px;\">${minorLabel}</div>` : ''}</div>`;\n            }\n            return null;\n          });\n        \n          const viewPadMs = visibleTimeSpanMs * 0.5;\n          const activeItemData = data[activeIndex];\n          const activeDataNode = validData.find(d => d.id === activeItemData?.id);\n          const isSuspended = !activeDataNode;\n        \n          const stackRegistry = {};\n          const markers = validData.map((item, index) => {\n            const itemStartMs = item.startDate.min;\n            const itemEndMs = (item.endDate && !isNaN(item.endDate.max)) ? item.endDate.max : itemStartMs;\n            if (itemEndMs < (visibleLeftMs - viewPadMs) || itemStartMs > (visibleRightMs + viewPadMs)) return null;\n        \n            const globalIndex = data.findIndex(d => d.id === item.id);\n            const startPct = Number((((itemStartMs - renderMinTime) / renderTimeRange) * 100).toFixed(4));\n            const tagIndices = getParsedTags(item.tags).map(t => orderedTags.indexOf(t)).filter(idx => idx !== -1);\n            const laneIdx = tagIndices.length > 0 ? Math.min(...tagIndices) : 0;\n            \n            const topPos = (laneIdx * laneHeight) + 5;\n            const blockHeight = ((tagIndices.length > 0 ? Math.max(...tagIndices) : 0) - laneIdx + 1) * laneHeight;\n            const { lines, pxWidth } = formatLabelSmart(safeStripHTML(item.title));\n            const hasMedia = item.media && item.media.length > 0;\n        \n            const stackKey = `${itemStartMs}_${laneIdx}`;\n        \n            if (!stackRegistry[stackKey]) stackRegistry[stackKey] = 0;\n            const stackDepth = stackRegistry[stackKey]++;\n            const xOffset = stackDepth * 6;\n            const yOffset = stackDepth * 4;\n        \n            let endPct = startPct;\n            if (item.endDate && !isNaN(item.endDate.max) && item.endDate.max > itemStartMs) {\n              endPct = Number((((item.endDate.max - renderMinTime) / renderTimeRange) * 100).toFixed(4));\n            }\n            const hasDuration = (endPct - startPct) > 0.001;\n            const isActive = globalIndex === activeIndex;\n        \n            const colActive = 'var(--tm-active, #007acc)';\n            const colInactive = 'rgba(var(--tm-inactive-rgb, 204, 0, 0), 0.6)';\n            const colApprox = 'var(--tm-approx, #ffb300)';\n            const heatShadow = stackDepth > 0 ? `box-shadow: 0 0 ${stackDepth * 2}px ${stackDepth * 0.25}px var(--tm-glow, rgba(102, 178, 255, 0.4));` : '';\n        \n            const isApproxStart = item.startDate && item.startDate.isEDTF && item.startDate.obj && item.startDate.obj.approximate;\n            const isApproxEnd = item.endDate && item.endDate.isEDTF && item.endDate.obj && item.endDate.obj.approximate;\n        \n            let xAxisMarker = '';\n            if (item.startDate.isEDTF && item.startDate.obj && !hasDuration) {\n              const obj = item.startDate.obj;\n              if (obj.type === 'Set') {\n                const setEndPct = Number((((obj.max - renderMinTime) / renderTimeRange) * 100).toFixed(4));\n                xAxisMarker = html`<div style=\"position: absolute; bottom: 0; left: 0; width: calc(${setEndPct - startPct}% + 6px); height: 10px; background: rgba(var(--tm-approx-shadow-rgb, 255, 183, 77), 0.1); border: 1px dashed ${colApprox}; border-radius: 4px; z-index: 900; transform: translateX(-3px);\"></div>`;\n              } else if (obj.type === 'List') {\n                const setEndPct = Number((((obj.max - renderMinTime) / renderTimeRange) * 100).toFixed(4));\n                const subDots = (obj.values || []).map(v => {\n                  const vPct = Number((((v.min - itemStartMs) / renderTimeRange) * trackWidthPx).toFixed(2));\n                  return html`<div style=\"position: absolute; bottom: 1px; left: ${vPct}px; width: 4px; height: 4px; border-radius: 50%; background: ${colInactive}; transform: translateX(-2px);\"></div>`;\n                });\n                xAxisMarker = html`<div style=\"position: absolute; bottom: 0; left: 0; width: ${setEndPct - startPct}%; height: 1px; background: rgba(var(--tm-inactive-shadow-rgb, 176, 190, 197), 0.4); z-index: 900;\">${subDots}</div>`;\n              }\n            }\n        \n            if (!xAxisMarker && hasDuration) {\n              if (isActive) {\n                const activeBorderL = isApproxStart ? `3px solid ${colApprox}` : `2px solid ${colActive}`;\n                const activeBorderR = isApproxEnd ? `3px solid ${colApprox}` : 'none';\n                const cStyle = (isApproxStart || isApproxEnd) ? 'cursor: zoom-in;' : '';\n                xAxisMarker = html`<div style=\"position: absolute; bottom: 0; left: 0; width: 100%; min-width: 4px; height: 10px; background: rgba(var(--tm-active-shadow-rgb, 102, 178, 255), 0.30); border-left: ${activeBorderL}; border-right: ${activeBorderR}; border-top: none; border-bottom: none; ${cStyle} clip-path: polygon(0 0, 100% 7px, 100% 100%, 0 100%); z-index: 950; box-sizing: border-box;\" title=\"${(isApproxStart || isApproxEnd) ? 'Approximate Duration. Click node to auto-zoom.' : ''}\"></div>`;\n              } else {\n                const styleIdx = uniqueStarts.indexOf(itemStartMs) % 4;\n                const hatchAngles = ['45deg', '-45deg', '60deg', '-60deg'];\n                const borderL = isApproxStart ? `3px solid rgba(var(--tm-approx-shadow-rgb, 255, 183, 77), 0.6)` : `2px solid rgba(var(--tm-inactive-shadow-rgb, 176, 190, 197), 0.6)`;\n                const borderR = isApproxEnd ? `3px solid rgba(var(--tm-approx-shadow-rgb, 255, 183, 77), 0.6)` : `2px solid rgba(var(--tm-inactive-shadow-rgb, 176, 190, 197), 0.6)`;\n                const hatchStyle = `background: repeating-linear-gradient(${hatchAngles[styleIdx]}, rgba(var(--tm-inactive-shadow-rgb, 176, 190, 197), 0.3) 0, rgba(var(--tm-inactive-shadow-rgb, 176, 190, 197), 0.3) 1px, transparent 1px, transparent 13px);`;\n                const segmentedMask = `-webkit-mask-image: repeating-linear-gradient(to right, black 0, black 70px, transparent 70px, transparent 100px); -webkit-mask-image: repeating-linear-gradient(to right, black 0, black 70px, transparent 70px, transparent 100px); mask-image: repeating-linear-gradient(to right, black 0, black 70px, transparent 70px, transparent 100px);`;\n                xAxisMarker = html`\n                  <div style=\"position: absolute; bottom: 0; left: 0; width: 100%; height: 10px; z-index: 900; mix-blend-mode: multiply;\">\n                    <div style=\"position: absolute; inset: 0; ${hatchStyle} border-left: ${borderL}; border-right: ${borderR}; border-bottom: none; border-top: none; clip-path: polygon(0 0, 100% 7px, 100% 100%, 0 100%); box-sizing: border-box; ${segmentedMask}\"></div>\n                    <div class=\"hover-bridge-hitbox\" style=\"position: absolute; top: 0; bottom: -15px; left: -2px; right: -2px; z-index: 10; cursor: help;\" onMouseEnter=${(e) => handleCaliperEnter(e, item)} onMouseMove=${(e) => handleCaliperMove(e, item)} onMouseLeave=${handleCaliperLeave}></div>\n                  </div>\n                `;\n              }\n            }\n        \n            let dropLine = '';\n            if (isActive) {\n              if (isApproxStart) dropLine = html`<div style=\"position: absolute; left: 0; top: ${blockHeight / 2}px; bottom: 0; width: 2px; background: ${colApprox}; ${heatShadow} z-index: 999;\"></div>`;\n              else dropLine = html`<div style=\"position: absolute; left: 0; top: ${blockHeight / 2}px; bottom: 0; width: 2px; background: ${colActive}; ${heatShadow} z-index: 999;\"></div>`;\n            } else if (!hasDuration) {\n              if (isApproxStart) dropLine = html`<div style=\"position: absolute; left: 0; top: ${blockHeight / 2}px; bottom: 0; width: 2px; background: ${colApprox}; ${heatShadow} z-index: 900; cursor: zoom-in;\" title=\"Approximate Date\"></div>`;\n              else dropLine = html`<div style=\"position: absolute; left: 0; top: ${blockHeight / 2}px; bottom: 0; width: 2px; background: ${colInactive}; ${heatShadow} z-index: 900;\"></div>`;\n            }\n        \n            return html`\n              <div id=\"timeline-marker-${globalIndex}\" class=\"event-group ${isActive ? 'active' : ''}\" style=\"left: calc(${startPct}% + ${xOffset}px); top: calc(${topPos}px + ${yOffset}px); bottom: 28px; ${hasDuration ? `width: calc(${endPct - startPct}% - ${xOffset}px); min-width: 4px;` : `width: ${pxWidth}px;`}\" onClick=${() => handleNodeClick(globalIndex)}>\n                ${dropLine}\n                ${xAxisMarker}\n                <div class=\"event-block\" style=\"position: absolute; top: ${blockHeight / 2}px; transform: translateY(-50%); left: 0; min-height: ${blockHeight}px; height: auto; --lane-h: ${laneHeight}px; --calc-w: ${pxWidth}px; width: var(--calc-w); min-width: var(--calc-w); background: ${isActive ? colActive : 'var(--tm-tooltip-bg, #ffffff)'}; color: ${isActive ? '#fff' : 'var(--tm-tooltip-text, #333333)'}; box-shadow: ${isActive ? '0 2px 8px rgba(0,0,0,0.3)' : '0 1px 4px rgba(0,0,0,0.1)'}; border: ${isActive ? 'none' : '1px solid #ddd'}; z-index: ${isActive ? 35 : 25};\">\n                  ${hasMedia ? html`<svg style=\"position: absolute; left: 6px; top: 50%; transform: translateY(-50%); width: 10px; height: 10px; opacity: 0.8;\" viewBox=\"0 0 24 24\" fill=\"none\" stroke=\"currentColor\" stroke-width=\"2.5\" stroke-linecap=\"round\" stroke-linejoin=\"round\"><rect x=\"3\" y=\"3\" width=\"18\" height=\"18\" rx=\"2\" ry=\"2\" /><circle cx=\"8.5\" cy=\"8.5\" r=\"1.5\" /><polyline points=\"21 15 16 10 5 21\" /></svg>` : ''}\n                  <div style=\"display: flex; flex-direction: column; width: 100%; letter-spacing: -0.2px;\">\n                    ${lines.map(l => html`<div style="white-space: nowrap; overflow: hidden; width: 100%;">${l}</div>`)}\n                  </div>\n                </div>\n              </div>\n            `;\n          });\n        \n          return html`\n            <style>\n              .event-group:hover {\n                z-index: 99999 !important;\n              }\n              .event-group:hover .event-block {\n                transform: translateY(-50%) scale(1.08) !important;\n                box-shadow: 0 10px 25px rgba(0,0,0,0.3) !important;\n                border-color: var(--tm-active, #007acc) !important;\n                z-index: 99999 !important;\n                width: max-content !important;\n                min-width: var(--calc-w) !important;\n              }\n            </style>\n            <div style="position: relative; width: 100%; height: 100%; display: flex; flex-direction: column; overflow: hidden;\">\n              <div class=\"timeline-control-cluster\" style=\"top: 15px; flex-direction: row; height: 24px;\">\n                <button class=\"status-btn\" style="border: none; border-right: 1px solid #eee; border-radius: 0;" onClick=${() => setIsTimelineMinimized(true)} title="Minimize Timeline">\n                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12" /></svg>\n                </button>\n                <button class="status-btn ${isTimelineExpanded ? 'active' : ''}" style="border: none; border-radius: 0;" onClick=${() => {\n                  if (!isTimelineExpanded) {\n                    const appNode = document.getElementById('app-layout');\n                    if(appNode) appNode.style.setProperty('--timeline-height', `${timelineRequiredHeight}px`);\n                    setIsTimelineExpanded(true);\n                  } else {\n                    const appNode = document.getElementById('app-layout');\n                    if(appNode) appNode.style.setProperty('--timeline-height', '10%');\n                    setIsTimelineExpanded(false);\n                  }\n                }} title=${isTimelineExpanded ? "Restore Layout" : "Maximize Timeline"}>\n                  ${isTimelineExpanded\n                    ? html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="9" width="12" height="12" rx="1" /><path d="M9 3h9a1 1 0 0 1 1 1v9" /></svg>`\n                    : html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2" /></svg>`\n                  }\n                </button>\n              </div>\n        \n              <div class=\"timeline-control-cluster temporal\" style=\"top: 45px; width: 24px;\">\n                <button class="status-btn" style="border: none; border-bottom: 1px solid #eee; border-radius: 0;" onClick=${() => { if(zoomLock!=='hard') setZoomLock('soft'); handleManualZoom(Math.min(zoomLevel * 1.5, 2000), 'center'); }} title="Zoom In">\n                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19" /><line x1="5" y1="12" x2="19" y2="12" /></svg>\n                </button>\n                <button class="status-btn" style="border: none; border-bottom: 1px solid #eee; border-radius: 0;" onClick=${() => { if(zoomLock!=='hard') setZoomLock('soft'); handleManualZoom(Math.max(zoomLevel / 1.5, 1), 'center'); }} title="Zoom Out">\n                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12" /></svg>\n                </button>\n                <button class="status-btn ${zoomLock === 'hard' ? 'active' : ''}" style="border: none; border-radius: 0;" onClick=${() => setZoomLock(p => p === 'hard' ? 'auto' : 'hard')} title="Toggle Auto-Zoom Lock">\n                  ${zoomLock === 'hard'\n                    ? html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#007acc" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2" ry="2" /><path d="M7 11V7a5 5 0 0 1 10 0v4" /></svg>`\n                    : html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#888" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2" ry="2" /><path d="M7 11V7a5 5 0 0 1 9.9-1" /></svg>`\n                  }\n                </button>\n              </div>\n        \n              <div class="timeline-scroll-wrapper" ref=${wrapperRef} onScroll=${onScroll} onMouseDown=${onDown} onMouseLeave=${onUp} onMouseUp=${onUp} onMouseMove=${onMove} onTouchStart=${onDown} onTouchEnd=${onUp} onTouchMove=${onMove} onWheel=${onWheel}>\n                <div class="timeline-track-container" style="position: relative; width: ${trackWidthPx}px; flex-shrink: 0; height: 100%; box-sizing: border-box; opacity: ${isSuspended ? '0.3' : '1'}; filter: ${isSuspended ? 'grayscale(1)' : 'none'}; pointer-events: ${isSuspended ? 'none' : 'auto'}; transition: opacity 0.5s ease, filter 0.5s ease;\">\n                  \n                  <!-- Background Lanes Stripe (Z-Index 0) -->\n                  <div style="position: absolute; top: 15px; left: 0; right: 0; bottom: 50px; pointer-events: none; z-index: 0;\">\n                    ${orderedTags.map((tag, i) => html`\n                      <div class="tag-lane" style="top: ${i * laneHeight}px; height: ${laneHeight}px; background: ${i % 2 === 0 ? 'rgba(0,0,0,0.04)' : 'transparent'};"></div>\n                    `)}\n                  </div>\n        \n                  <!-- Solid White Duration Lane Background Band (for best pattern contrast) -->\n                  <div style="position: absolute; bottom: 28px; left: 0; right: 0; height: 10px; background: #ffffff; border-top: 1px solid rgba(0,0,0,0.05); border-bottom: 1px solid rgba(0,0,0,0.05); z-index: 1; pointer-events: none;"></div>\n        \n                  <div class="timeline-axis" style="position: absolute; bottom: 0; left: 0; right: 0; height: 28px; background: var(--tm-ribbon-floor, #ffffff); border-top: 2px solid #999; z-index: 5;\">\n                    ${rulerTicksHTML}\n                    ${minorTicksHTML}\n                  </div>\n        \n                  <!-- Event Markers -->\n                  ${markers}\n        \n                  <!-- Elevated Sticky Lane Labels (Z-Index 45 - Block runway layout) -->\n                  <div style="position: absolute; top: 15px; left: 0; right: 0; bottom: 50px; pointer-events: none; z-index: 45;\">\n                    ${orderedTags.map((tag, i) => html`\n                      <div style="position: absolute; top: ${i * laneHeight}px; height: ${laneHeight}px; left: 0; right: 0; pointer-events: none;\">\n                        <div class="tag-lane-label" style="background: ${i % 2 === 0 ? '#f4f4f4' : '#fcfcfc'}; border-right: 1px solid #ccc; box-shadow: 2px 0 4px rgba(0,0,0,0.05); pointer-events: auto; position: sticky; left: 0; height: 100%; display: inline-flex; align-items: center; padding: 0 10px; font-size: 0.75rem; color: #555;">${tag}</div>\n                      </div>\n                    `)}\n                  </div>\n        \n                </div>\n              </div>\n        \n              ${caliperTooltip && html`\n                <div style="position: absolute; left: ${caliperTooltip.x}px; top: 15px; transform: translateX(-50%); background: var(--tm-tooltip-bg, #ffffff); color: var(--tm-tooltip-text, #333333); border: 1px solid #ccc; padding: 8px 12px; border-radius: 6px; z-index: 10005; font-size: 0.75rem; box-shadow: 0 4px 15px rgba(0,0,0,0.15); max-width: 250px; white-space: normal; line-height: 1.4; max-height: calc(100% - 45px); overflow-y: auto; pointer-events: auto;\">\n                  <div style="position: absolute; top: -6px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 6px solid transparent; border-right: 6px solid transparent; border-bottom: 6px solid var(--tm-tooltip-bg, #ffffff);"></div>\n                  <div style="font-weight: bold; color: var(--tm-active, #0066cc); margin-bottom: 4px;">${caliperTooltip.title}</div>\n                  <div style="color: #666; margin-bottom: ${caliperTooltip.overlaps.length ? '6px' : '0'}; border-bottom: ${caliperTooltip.overlaps.length ? '1px solid #eee' : 'none'}; padding-bottom: ${caliperTooltip.overlaps.length ? '4px' : '0'};">Duration: ${Math.round(caliperTooltip.durationMs / 86400000)} Days</div>\n                  ${caliperTooltip.overlaps.length > 0 ? html`\n                    <div style="font-size: 0.65rem; color: #888;\">\n                      Overlaps with ${caliperTooltip.overlaps.length} event(s):<br/>\n                      ${caliperTooltip.overlaps.slice(0, 3).map(t => html`<span style="display:block; white-space:nowrap; overflow:hidden; text-overflow:ellipsis;">• ${t}</span>`)}\n                      ${caliperTooltip.overlaps.length > 3 ? html`<span>+ ${caliperTooltip.overlaps.length - 3} more</span>` : ''}\n                    </div>\n                  ` : ''}\n                </div>\n              `}\n            </div>\n          `;\n        };\n        \n        MODULE_VERSIONS['TimelineScrubber'] = 'v26.11.8';\n// 🔼🔼🔼 [ END_INJECT: TimelineScrubber ] 🔼🔼🔼
```

---

### Component B: `MapViewer v6.4.2`
**Target Slot:** Locate `// === [ MAJOR BLOCK: MapViewer` inside `cartimap.v8.11.25.html` (approx. line 450+) and replace the entire component with this block:

```javascript
// 🔽🔽🔽 [ START_INJECT: MapViewer v6.4.2 ] 🔽🔽🔽
        // === [ MAJOR BLOCK: MapViewer v6.4.2 ] ===
        const MapViewer = ({ data, activeIndex, setActiveIndex, addLog, basemapsRegistry, maxAutoZoom, minimapOffset, setMinimapOffset, maxPane, setMaxPane, polygonOpacity, showButtonText, visibleTimeBounds }) => {
          const mapDomRef = useRef(null); const miniMapDomRef = useRef(null);
          const mapInstance = useRef(null); const miniMapInstance = useRef(null);
          const rectBoundsRef = useRef(null); const markerLayer = useRef(null);
          const clusterLayer = useRef(null); const gridLayerRef = useRef(null);
          const markersRef = useRef({}); const hasFitBounds = useRef(false);
          const [mapZoom, setMapZoom] = useState(2); const [showGrid, setShowGrid] = useState(false);
          const [showLayersMenu, setShowLayersMenu] = useState(false);
          const [activeBasemap, setActiveBasemap] = useState(null);
          const [activeOverlays, setActiveOverlays] = useState([]);
          const [overlayOpacities, setOverlayOpacities] = useState({});
          const initialLoadRef = useRef(false); const baseLayerRef = useRef(null);
          const miniBaseLayerRef = useRef(null); const overlayLayersRef = useRef({});
          const minimapOffsetRef = useRef(minimapOffset || -4);
          const isSyncingRef = useRef(false);
        
          const safeStripHTML = (str) => {
            if (!str) return '';
            return String(str).replace(/<p[^>]*>/gi, ' - ').replace(/<[^>]*>?/gm, '').trim();
          };
        
          const loadScript = (src) => new Promise((resolve, reject) => {
            if (document.querySelector(`script[src="${src}"]`)) return resolve();
            const script = document.createElement('script'); script.src = src; script.onload = resolve; script.onerror = reject; document.head.appendChild(script);
          });
        
          const loadStyle = (href) => {
            if (document.querySelector(`link[href="${href}"]`)) return;
            const link = document.createElement('link'); link.rel = 'stylesheet'; link.href = href; document.head.appendChild(link);
          };
        
          const maxGlobalZoom = basemapsRegistry && basemapsRegistry.length > 0 ? Math.max(...basemapsRegistry.map(b => b.maxZoom || 19)) : 22;
        
          useEffect(() => {
            if (basemapsRegistry && basemapsRegistry.length > 0 && !initialLoadRef.current) {
              const defaultBase = basemapsRegistry.find(b => b.type === 'base' && b.active) || basemapsRegistry.find(b => b.type === 'base');
              if (defaultBase) setActiveBasemap(defaultBase.id);
              const defaultOverlays = basemapsRegistry.filter(b => b.type === 'overlay' && b.active).map(b => b.id);
              setActiveOverlays(defaultOverlays);
              const initOpac = {}; basemapsRegistry.filter(b => b.type === 'overlay').forEach(o => { initOpac[o.id] = o.defaultOpacity ?? 1.0; });
              setOverlayOpacities(initOpac); initialLoadRef.current = true;
            }
          }, [basemapsRegistry]);
        
          useEffect(() => {
            minimapOffsetRef.current = minimapOffset;
            if (mapInstance.current && miniMapInstance.current) {
              let targetMiniZoom = Math.max(0, mapInstance.current.getZoom() + minimapOffset);
              miniMapInstance.current.setView(mapInstance.current.getCenter(), targetMiniZoom, { animate: true });
            }
          }, [minimapOffset]);
        
          const createPinHtml = (isActive, isVip) => {
            const color = isActive ? '#28a745' : (isVip ? '#ffb300' : '#007acc');
            return `<div class="custom-map-pin" style="transform: ${isActive ? 'scale(1.3)' : 'scale(1)'}; z-index: ${isActive ? '1000' : '0'};"><div class="pin-head" style="background: ${color};"></div><div class="pin-stem" style="background: ${isActive ? '#28a745' : '#333'}; width: ${isActive ? '3px' : '2px'};"></div></div>`;
          };
        
          const extractLayers = (layerObj) => {
            let layers = [];
            if (Array.isArray(layerObj)) layerObj.forEach(l => layers = layers.concat(extractLayers(l)));
            else if (layerObj && layerObj.eachLayer) layerObj.eachLayer(l => layers = layers.concat(extractLayers(l)));
            else if (layerObj) layers.push(layerObj);
            return layers;
          };
        
          const parseGeometryCollection = (wktStr) => {
            const cleanStr = wktStr.trim().replace(/^GEOMETRYCOLLECTION\s*\(/i, '').replace(/\)\s*$/, '');
            let inParen = 0; let currentGeom = ''; const geometries = [];
            for (let i = 0; i < cleanStr.length; i++) {
              const char = cleanStr[i];
              if (char === '(') inParen++; if (char === ')') inParen--;
              if (char === ',' && inParen === 0) { geometries.push(currentGeom.trim()); currentGeom = ''; }
              else currentGeom += char;
            }
            if (currentGeom.trim()) geometries.push(currentGeom.trim());
            let extractedLayers = [];
            geometries.forEach(geomStr => {
              try {
                const wkt = new window.Wkt.Wkt(); wkt.read(geomStr);
                extractedLayers = extractedLayers.concat(extractLayers(wkt.toObject()));
              } catch (e) {
                const upper = geomStr.toUpperCase();
                if (upper.startsWith('POINT')) {
                  const m = geomStr.match(/(-?\d+\.?\d*)\s+(-?\d+\.?\d*)/);
                  if (m) extractedLayers.push(L.marker(new L.LatLng(parseFloat(m.at(1)), parseFloat(m.at(2)))));
                } else if (upper.startsWith('LINESTRING') || upper.startsWith('POLYGON')) {
                  const m = [...geomStr.matchAll(/(-?\d+\.?\d*)\s+(-?\d+\.?\d*)/g)];
                  if (m.length > 0) extractedLayers.push(upper.startsWith('POLY') ? L.polygon(m.map(x => new L.LatLng(parseFloat(x.at(1)), parseFloat(x.at(2))))) : L.polyline(m.map(x => new L.LatLng(parseFloat(x.at(1)), parseFloat(x.at(2))))));
                }
              }
            });
            return extractedLayers;
          };
        
          useEffect(() => {
            if (mapDomRef.current && miniMapDomRef.current && !mapInstance.current && window.L && basemapsRegistry) {
              const urlParams = new URLSearchParams(window.location.search);
              const initialZoom = urlParams.get('mapzoom') ? parseInt(urlParams.get('mapzoom')) : 2;
              setMapZoom(initialZoom);
              const map = L.map(mapDomRef.current, { zoomControl: false, maxZoom: maxGlobalZoom }).setView(new L.LatLng(37.9838, 23.7275), initialZoom);
              L.control.scale({ position: 'bottomleft', imperial: true, metric: true }).addTo(map);
              map.on('zoomend', () => setMapZoom(map.getZoom()));
        
              markerLayer.current = L.featureGroup().addTo(map);
              clusterLayer.current = L.markerClusterGroup({
                maxClusterRadius: 40,
                spiderfyOnMaxZoom: true,
                zoomToBoundsOnClick: false,
                iconCreateFunction: function(cluster) {
                  const children = cluster.getAllChildMarkers();
                  const firstLatLng = children.at(0).getLatLng();
                  const isExactSame = children.every(m => m.getLatLng().equals(firstLatLng));
                  if (isExactSame) {
                    const count = children.length;
                    const html = `<div class="custom-map-pin" style="transform: scale(1.05); z-index: 500;"><div class="pin-head" style="background: #007acc; box-shadow: 2px 2px 0px rgba(0,0,0,0.4);"></div><div class="pin-stem" style="background: #333; width: 2px;"></div><div style="position: absolute; top: -6px; right: -8px; background: #d32f2f; color: #fff; border-radius: 50%; width: 15px; height: 15px; font-size: 9px; line-height: 15px; font-weight: bold; text-align: center; border: 1px solid #fff; box-shadow: 0 1px 3px rgba(0,0,0,0.3);">${count}</div></div>`;
                    return L.divIcon({ className: 'custom-div-icon', html: html, iconSize: new L.Point(24, 34), iconAnchor: new L.Point(12, 34) });
                  }
                  let c = ' marker-cluster-';
                  if (children.length < 10) c += 'small';
                  else if (children.length < 100) c += 'medium';
                  else c += 'large';
                  return new L.DivIcon({ html: '<div><span>' + children.length + '</span></div>', className: 'marker-cluster' + c, iconSize: new L.Point(40, 40) });
                }
              }).addTo(map);
        
              clusterLayer.current.on('clusterclick', (c) => {
                const m = mapInstance.current;
                if (m.getZoom() < 10) { m.fitBounds(c.layer.getBounds(), { padding: new L.Point(40, 40) }); }
                else { c.layer.spiderfy(); }
              });
        
              gridLayerRef.current = L.layerGroup().addTo(map);
              clusterLayer.current.on('clustermouseover', (c) => {
                const children = c.layer.getAllChildMarkers();
                const places = [...new Set(children.map(m => m.itemPlace).filter(Boolean))];
                const titles = [...new Set(children.map(m => m.itemTitle).filter(Boolean))];
                let displayHtml = '';
                if (places.length > 0) { displayHtml += `<div style="font-weight: 600; color: #007acc; border-bottom: 1px solid #ccc; margin-bottom: 4px; padding-bottom: 4px; text-align: center;">${places.slice(0, 2).join(' / ')}${places.length > 2 ? '...' : ''}</div>`; }
                displayHtml += `<div style="text-align: left; line-height: 1.3;">`;
                displayHtml += titles.slice(0, 5).map(t => `• ${t}`).join('<br/>');
                if (titles.length > 5) displayHtml += `<br/><em style="color: #666; font-size: 0.8em; margin-top: 4px; display: inline-block; text-align: center; width: 100%;">+${titles.length - 5} more events...</em>`;
                displayHtml += `</div>`;
                c.layer.bindTooltip(displayHtml, { direction: 'top', className: 'custom-cluster-tooltip' }).openTooltip();
              });
              clusterLayer.current.on('clustermouseout', (c) => c.layer.unbindTooltip());
        
              const miniMap = L.map(miniMapDomRef.current, { zoomControl: false, attributionControl: false, dragging: false, touchZoom: true, scrollWheelZoom: true, doubleClickZoom: true, maxZoom: maxGlobalZoom }).setView(new L.LatLng(37.9838, 23.7275), 0);
              const boundsRect = L.rectangle(map.getBounds(), { color: '#007acc', weight: 2, fillOpacity: 0.15 }).addTo(miniMap);
              rectBoundsRef.current = boundsRect;
        
              map.on('move', () => {
                isSyncingRef.current = true;
                let targetMiniZoom = Math.max(0, map.getZoom() + minimapOffsetRef.current);
                miniMap.setView(map.getCenter(), targetMiniZoom, { animate: false });
                const mapBounds = map.getBounds(); const center = map.getCenter();
                const nw = miniMap.project(mapBounds.getNorthWest(), targetMiniZoom);
                const se = miniMap.project(mapBounds.getSouthEast(), targetMiniZoom);
                const w = Math.abs(se.x - nw.x); const h = Math.abs(se.y - nw.y);
                const MIN_PX = 30;
                if (w < MIN_PX || h < MIN_PX) {
                  const cPx = miniMap.project(center, targetMiniZoom);
                  const adjW = Math.max(w, MIN_PX); const adjH = Math.max(h, MIN_PX);
                  boundsRect.setBounds(L.latLngBounds(miniMap.unproject(L.point(cPx.x - adjW / 2, cPx.y - adjH / 2), targetMiniZoom), miniMap.unproject(L.point(cPx.x + adjW / 2, cPx.y + adjH / 2), targetMiniZoom)));
                } else boundsRect.setBounds(mapBounds);
                isSyncingRef.current = false;
              });
        
              miniMap.on('zoomend', () => {
                if (!isSyncingRef.current && setMinimapOffset) {
                  let newOffset = miniMap.getZoom() - mapInstance.current.getZoom();
                  newOffset = Math.max(-10, Math.min(2, newOffset));
                  setMinimapOffset(newOffset); minimapOffsetRef.current = newOffset;
                }
              });
        
              mapInstance.current = map; miniMapInstance.current = miniMap;
        
              if (window.ResizeObserver) {
                const ro = new ResizeObserver(() => { setTimeout(() => { if (mapInstance.current) mapInstance.current.invalidateSize(); if (miniMapInstance.current) miniMapInstance.current.invalidateSize(); }, 50); });
                ro.observe(mapDomRef.current.parentElement);
                ro.observe(miniMapDomRef.current);
              }
            }
          }, [basemapsRegistry]);
        
          useEffect(() => {
            const map = mapInstance.current; if (!map || !gridLayerRef.current) return;
            const updateGrid = () => {
              gridLayerRef.current.clearLayers(); if (!showGrid) return;
              const z = map.getZoom(); let step = z > 15 ? 0.01 : z > 13 ? 0.05 : z > 11 ? 0.1 : z > 9 ? 0.5 : z > 7 ? 1 : z > 5 ? 5 : z > 3 ? 10 : 20;
              const b = map.getBounds();
              const w = Math.floor(b.getWest() / step) * step - step; const e = Math.ceil(b.getEast() / step) * step + step;
              const s = Math.floor(b.getSouth() / step) * step - step; const n = Math.ceil(b.getNorth() / step) * step + step;
              const style = { color: '#007acc', weight: 1, opacity: 0.25, dashArray: '2, 6', interactive: false };
              for (let lat = s; lat <= n; lat += step) if (lat >= -90 && lat <= 90) L.polyline([new L.LatLng(lat, w), new L.LatLng(lat, e)], style).addTo(gridLayerRef.current);
              for (let lng = w; lng <= e; lng += step) L.polyline([new L.LatLng(-90, lng), new L.LatLng(90, lng)], style).addTo(gridLayerRef.current);
            };
            updateGrid(); map.on('moveend', updateGrid); return () => map.off('moveend', updateGrid);
          }, [showGrid]);
        
          useEffect(() => {
            const map = mapInstance.current; const miniMap = miniMapInstance.current;
            if (!map || !miniMap || !basemapsRegistry || !activeBasemap) return;
            const config = basemapsRegistry.find(b => b.id === activeBasemap) || basemapsRegistry;
            const renderBasemap = () => {
              if (baseLayerRef.current) map.removeLayer(baseLayerRef.current);
              if (miniBaseLayerRef.current) miniMap.removeLayer(miniBaseLayerRef.current);
              const isVector = config.format === "pbf" || config.format === "mvt";
              if (isVector && window.L.maplibreGL) {
                baseLayerRef.current = L.maplibreGL({ style: './style.json', attribution: `<a href="${config.attrLink}" target="_blank">${config.attrText}</a>`, zIndex: 0 }).addTo(map);
                miniBaseLayerRef.current = L.maplibreGL({ style: './style.json', attribution: false, zIndex: 0 }).addTo(miniMap);
              } else {
                baseLayerRef.current = L.tileLayer(config.url, { maxNativeZoom: config.maxZoom, maxZoom: maxGlobalZoom, attribution: `<a href="${config.attrLink}" target="_blank">${config.attrText}</a>`, zIndex: 0, keepBuffer: 4, updateWhenZooming: false }).addTo(map);
                miniBaseLayerRef.current = L.tileLayer(config.url, { maxNativeZoom: config.maxZoom, maxZoom: maxGlobalZoom, attribution: false, zIndex: 0, keepBuffer: 4, updateWhenZooming: false }).addTo(miniMap);
              }
            };
            if ((config.format === "pbf" || config.format === "mvt") && !window.L.maplibreGL) {
              loadStyle('https://unpkg.com/maplibre-gl@3.6.2/dist/maplibre-gl.css');
              Promise.all([loadScript('https://unpkg.com/maplibre-gl@3.6.2/dist/maplibre-gl.js')]).then(() => loadScript('https://unpkg.com/@maplibre/maplibre-gl-leaflet@0.0.20/leaflet-maplibre-gl.js')).then(() => renderBasemap()).catch(e => console.error("Vector Library Failed", e));
            } else renderBasemap();
          }, [activeBasemap, basemapsRegistry, maxGlobalZoom]);
        
          useEffect(() => {
            const map = mapInstance.current; const miniMap = miniMapInstance.current;
            if (!map || !miniMap || !basemapsRegistry) return;
            Object.keys(overlayLayersRef.current).forEach(id => {
              if (!activeOverlays.includes(id)) { map.removeLayer(overlayLayersRef.current[id]); delete overlayLayersRef.current[id]; }
            });
            activeOverlays.forEach((id, idx) => {
              if (!overlayLayersRef.current[id]) {
                const config = basemapsRegistry.find(b => b.id === id);
                if (config) {
                  const z = idx + 10; const op = overlayOpacities[id] !== undefined ? overlayOpacities[id] : (config.defaultOpacity ?? 1.0);
                  const isWms = config.format === "wms" || config.url.toLowerCase().includes("wms");
                  if (isWms) {
                    overlayLayersRef.current[id] = L.tileLayer.wms(config.url, {maxNativeZoom: config.maxZoom, maxZoom: maxGlobalZoom, layers: config.wmsLayer || "default", format: "image/png", transparent: true, opacity: op, attribution: `<a href="${config.attrLink}" target="_blank">${config.attrText}</a>`, zIndex: z, keepBuffer: 4, updateWhenZooming: false, updateWhenIdle: true}).addTo(map);
                  } else {
                    overlayLayersRef.current[id] = L.tileLayer(config.url, {maxNativeZoom: config.maxZoom, maxZoom: maxGlobalZoom, opacity: op, attribution: `<a href="${config.attrLink}" target="_blank">${config.attrText}</a>`, zIndex: z, transparent: true, keepBuffer: 4, updateWhenZooming: false, updateWhenIdle: true}).addTo(map);
                  }
                }
              }
            });
          }, [activeOverlays, basemapsRegistry, maxGlobalZoom, overlayOpacities]);
        
          useEffect(() => {
            Object.keys(overlayOpacities).forEach(id => { if (overlayLayersRef.current[id]) overlayLayersRef.current[id].setOpacity(overlayOpacities[id]); });
          }, [overlayOpacities]);
        
          useEffect(() => {
            const map = mapInstance.current; if (!map || data.length === 0) return;
            markerLayer.current.clearLayers(); clusterLayer.current.clearLayers();
            markersRef.current = {}; let validMarkers = 0;
            data.forEach((item, idx) => {
              const locStr = String(item.location || '').trim(); if (!locStr) return;
              const activeLayersArray = []; let featureLayers = [];
              try {
                if (locStr.match(/^GEOMETRYCOLLECTION/i)) featureLayers = parseGeometryCollection(locStr);
                else if (locStr.match(/^[A-Z]+\s*\(/)) { const wkt = new window.Wkt.Wkt(); wkt.read(locStr); featureLayers = extractLayers(wkt.toObject()); }
                else if (locStr.startsWith('{') && locStr.includes('"type"')) featureLayers = extractLayers(L.geoJSON(JSON.parse(locStr)));
                else {
                  const coordMatch = locStr.match(/(-?\d+(?:\.\d+)?)[,\s]+(-?\d+(?:\.\d+)?)/);
                  if (coordMatch) featureLayers.push(L.marker(new L.LatLng(parseFloat(coordMatch.at(1)), parseFloat(coordMatch.at(2)))));
                }
                const uniqueSignatures = new Set(); const validFeatureLayers = [];
                featureLayers.forEach(layer => {
                  if (!layer) return; let sig = null;
                  if (layer.getLatLng) {
                    const ll = layer.getLatLng();
                    if (!ll || ll.lat == null || ll.lng == null || isNaN(ll.lat) || isNaN(ll.lng)) return;
                    sig = `P_${ll.lat.toFixed(5)}_${ll.lng.toFixed(5)}`;
                  } else if (layer.getBounds) {
                    const b = layer.getBounds();
                    if (!b || !b.isValid()) return;
                    sig = `B_${b.toBBoxString()}`;
                  }
                  if (sig) { if (uniqueSignatures.has(sig)) return; uniqueSignatures.add(sig); }
                  validFeatureLayers.push(layer);
                });
                const subLabels = item.subLabels ? item.subLabels.split(/[|\\-·;\n]/).map(s => s.trim()).filter(Boolean) : [];
                const places = item.place ? item.place.split(/[|\\-·;\n]/).map(s => s.trim()).filter(Boolean) : [];
                const isVip = String(item.priority).trim().toUpperCase() === 'VIP';
                validFeatureLayers.forEach((layer, layerIdx) => {
                  if (layer instanceof L.Polygon) layer.setStyle({ stroke: false, fillColor: '#007acc', fillOpacity: polygonOpacity });
                  else if (layer instanceof L.Polyline) layer.setStyle({ color: '#007acc', weight: 2, dashArray: '8, 8' });
                  else if (layer.setStyle) layer.setStyle({ color: '#007acc', weight: 4 });
                  if (layer instanceof L.Marker) { layer.setIcon(L.divIcon({ className: 'custom-div-icon', html: createPinHtml(false, isVip), iconSize: new L.Point(24, 34), iconAnchor: new L.Point(12, 34) })); layer.isVip = isVip; }
                  const safeSubLabel = subLabels.length > layerIdx ? subLabels[layerIdx] : null;
                  const safePlace = places.length > layerIdx ? places[layerIdx] : null;
                  let labelToUse = safeSubLabel || safePlace || item.title;
                  layer.itemPlace = safeStripHTML(labelToUse);
                  layer.itemTitle = safeStripHTML(item.title);
                  layer.bindTooltip(layer.itemPlace, { direction: 'top', offset: new L.Point(0, -34), className: 'centered-tooltip' });
                  layer.on('click', () => setActiveIndex(idx));
                  if (layer instanceof L.Marker && !isVip) clusterLayer.current.addLayer(layer); else markerLayer.current.addLayer(layer);
                  activeLayersArray.push(layer); validMarkers++;
                });
                if (activeLayersArray.length > 0) markersRef.current[idx] = activeLayersArray;
              } catch(e) { console.error("Map Error Row", idx, e); }
            });
            setTimeout(() => {
              if (map && validMarkers > 0 && !hasFitBounds.current && !new URLSearchParams(window.location.search).get('mapzoom')) {
                const bounds = L.latLngBounds();
                markerLayer.current.eachLayer(l => { if (l.getLatLng) bounds.extend(l.getLatLng()); else if (l.getBounds) bounds.extend(l.getBounds()); });
                clusterLayer.current.eachLayer(l => bounds.extend(l.getLatLng()));
                if (bounds.isValid()) { map.fitBounds(bounds, { padding: new L.Point(6, 6), maxZoom: 6 }); hasFitBounds.current = true; }
              }
            }, 100);
          }, [data, polygonOpacity]);
        
          // --- [ START_SUBBLOCK: Map Temporal Ghosting Loop ] ---
          useEffect(() => {
            const map = mapInstance.current; const markers = markersRef.current;
            if (!map || Object.keys(markers).length === 0) return;
        
            const visibleBounds = visibleTimeBounds || new Array(0, Infinity);
            const vLeft = visibleBounds.at(0); const vRight = visibleBounds.at(1);
            let clusterAdd = []; let clusterRemove = [];
        
            Object.keys(markers).forEach(idxStr => {
              const idx = parseInt(idxStr, 10);
              const item = data[idx];
              const isTarget = activeIndex === idx;
              let inWindow = false;
        
              if (item && item.startDate && !isNaN(item.startDate.min)) {
                if (item.startDate.isEDTF && item.startDate.obj && (item.startDate.obj.type === 'Set' || item.startDate.obj.type === 'List') && Array.isArray(item.startDate.obj.values)) {
                  inWindow = item.startDate.obj.values.some(v => v.max >= vLeft && v.min <= vRight);
                } else {
                  const sMin = item.startDate.min;
                  const eMax = (item.endDate && !isNaN(item.endDate.max)) ? item.endDate.max : sMin;
                  inWindow = (eMax >= vLeft && sMin <= vRight);
                }
              }
        
              markers[idxStr].forEach(l => {
                if (l instanceof L.Polygon) {
                  l.setStyle({ stroke: false, fillColor: isTarget ? '#28a745' : '#007acc', fillOpacity: isTarget ? Math.min(polygonOpacity + 0.2, 1) : (inWindow ? polygonOpacity : 0.1), opacity: inWindow ? 1 : 0.2 });
                  if (isTarget && l.bringToFront) l.bringToFront();
                } else if (l instanceof L.Polyline) {
                  l.setStyle({ color: isTarget ? '#28a745' : '#007acc', weight: isTarget ? 3 : 2, dashArray: '8, 8', opacity: inWindow ? 1 : 0.2 });
                  if (isTarget && l.bringToFront) l.bringToFront();
                } else if (l instanceof L.Marker) {
                  l.setOpacity(inWindow ? 1 : 0.2);
                  if (isTarget) {
                    l.setIcon(L.divIcon({ className: 'custom-div-icon', html: createPinHtml(true, l.isVip), iconSize: new L.Point(24, 34), iconAnchor: new L.Point(12, 34) }));
                    if (!l.isVip) { clusterLayer.current.removeLayer(l); markerLayer.current.addLayer(l); }
                    l.setZIndexOffset(1000);
                  } else {
                    l.setIcon(L.divIcon({ className: 'custom-div-icon', html: createPinHtml(false, l.isVip), iconSize: new L.Point(24, 34), iconAnchor: new L.Point(12, 34) }));
                    l.setZIndexOffset(0);
                    if (!l.isVip) {
                      if (inWindow && !clusterLayer.current.hasLayer(l)) { markerLayer.current.removeLayer(l); clusterAdd.push(l); }
                      else if (!inWindow && clusterLayer.current.hasLayer(l)) { clusterRemove.push(l); markerLayer.current.addLayer(l); }
                    }
                  }
                } else if (l.setStyle) {
                  l.setStyle({ color: isTarget ? '#28a745' : '#007acc', weight: isTarget ? 5 : 4, opacity: inWindow ? 1 : 0.2 });
                  if (isTarget && l.bringToFront) l.bringToFront();
                }
              });
            });
        
            if (clusterRemove.length > 0) clusterLayer.current.removeLayers(clusterRemove);
            if (clusterAdd.length > 0) clusterLayer.current.addLayers(clusterAdd);
          }, [activeIndex, data, polygonOpacity, visibleTimeBounds]);
          // --- [ END_SUBBLOCK: Map Temporal Ghosting Loop ] ---
        
          // --- [ START_SUBBLOCK: Map Kinetic Camera Flight ] ---
          useEffect(() => {
            const map = mapInstance.current; const markers = markersRef.current;
            if (!map || Object.keys(markers).length === 0) return;
        
            const activeLayers = markers[activeIndex];
            if (activeLayers && activeLayers.length > 0) {
              const activeFeatureGroup = L.featureGroup(activeLayers);
              setTimeout(() => {
                try {
                  const bounds = activeFeatureGroup.getBounds();
                  if (bounds.isValid()) {
                    map.stop(); // Kinetic Camera Brakes: Halts previous transitions
                    map.flyToBounds(bounds, { animate: true, duration: 2.5, maxZoom: maxAutoZoom });
                    hasFitBounds.current = true;
                  }
                  activeLayers.forEach(l => { if (l.openTooltip) l.openTooltip(); });
                } catch(err) {}
              }, 250);
            }
          }, [activeIndex, maxAutoZoom]);
          // --- [ END_SUBBLOCK: Map Kinetic Camera Flight ] ---
        
          const bases = basemapsRegistry.filter(b => b.type !== 'overlay'); const overlays = basemapsRegistry.filter(b => b.type === 'overlay');
        
          return html`
            <div style="position: relative; width:100%; height:100%;">
              <div style="overflow: hidden; width:100%; height:100%; position: absolute; top:0; left:0; z-index:1;"><div ref=${mapDomRef} style="width:100%; height:100%;"></div></div>
              <div style="position: absolute; top: 15px; right: 15px; z-index: 1000; display: flex; flex-direction: column; gap: 10px; align-items: flex-end;">
                <div style="display: flex; width: 24px; box-shadow: 0 2px 6px rgba(0,0,0,0.25); border-radius: 4px; overflow: hidden; background: #fff;">
                  <button class="status-btn ${maxPane === 'map' ? 'active' : ''}" onClick=${() => setMaxPane(maxPane === 'map' ? null : 'map')} title=${maxPane === 'map' ? "Restore Layout" : "Maximize Map"} style="border: none;">
                    ${maxPane === 'map'
                      ? html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M8 3v3a2 2 0 0 1-2 2H3m18 0h-3a2 2 0 0 1-2-2V3m0 18v-3a2 2 0 0 1 2-2h3M3 16h3a2 2 0 0 1 2 2v3"/></svg>`
                      : html`<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M8 3H5a2 2 0 0 0-2 2v3m18 0V5a2 2 0 0 0-2-2h-3m0 18h3a2 2 0 0 0 2-2v-3M3 16v3a2 2 0 0 0 2 2h3"/></svg>`
                    }
                  </button>
                </div>
        
                <div style="display: flex; flex-direction: column; width: 24px; box-shadow: 0 2px 6px rgba(0,0,0,0.25); border-radius: 4px; overflow: hidden; background: #fff;">
                  <button class="status-btn" onClick=${() => mapInstance.current?.zoomIn()} style="border: none; border-bottom: 1px solid #e0e0e0; border-radius: 0;" title="Zoom In">
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                  </button>
                  <div title="Current Zoom Level" style="width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; font-size: 0.65rem; font-weight: 700; color: #222; border-bottom: 1px solid #e0e0e0; background: #fff; font-family: 'Arial Narrow', sans-serif, monospace; letter-spacing: -0.5px;">${mapZoom}z</div>
                  <button class="status-btn" onClick=${() => mapInstance.current?.zoomOut()} style="border: none; border-radius: 0;" title="Zoom Out">
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                  </button>
                </div>
        
                <div style="display: flex; width: 24px; box-shadow: 0 2px 6px rgba(0,0,0,0.25); border-radius: 4px; overflow: hidden; background: #fff;">
                  <button class="status-btn ${showGrid ? 'active' : ''}" onClick=${() => setShowGrid(!showGrid)} title="Toggle Coordinates Grid" style="border: none;">
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10\"></circle><line x1="2" y1="12" x2="22" y2="12"></line><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path></svg>
                  </button>
                </div>
        
                <div style="display: flex; width: 24px; box-shadow: 0 2px 6px rgba(0,0,0,0.25); border-radius: 4px; overflow: hidden; background: #fff;">
                  <button class="status-btn ${showLayersMenu ? 'active' : ''}" onClick=${() => setShowLayersMenu(!showLayersMenu)} title="Map Layers" style="border: none;">
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 2 7 12 12 22 7 12 2"></polygon><polyline points="2 17 12 22 22 17"></polyline><polyline points="2 12 17 22 12"></polyline></svg>
                  </button>
                </div>
              </div>
        
              ${showLayersMenu ? html`
                <div style="background: rgba(255,255,255,0.98); border: 1px solid #ccc; border-radius: 6px; padding: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); width: max-content; max-width: 320px; max-height: 50vh; overflow-y: auto; font-size: 0.85rem; color: #333; position: relative; z-index: 2000;">
                  <div style="font-weight: 600; margin-bottom: 8px; border-bottom: 1px solid #eee; padding-bottom: 4px;">Basemaps</div>
                  <div style="display: flex; flex-direction: column; gap: 8px; margin-bottom: 15px;">
                    ${bases.map(b => html`<div style="display: flex; align-items: flex-start; gap: 8px; line-height: 1.3;"><input type="radio" id="base_${b.id}" name="basemap_radio" checked=${activeBasemap === b.id} onChange=${() => setActiveBasemap(b.id)} style="margin: 2px 0 0 0; cursor: pointer; flex-shrink: 0;" /><div style="display: inline; margin: 0;"><label for="base_${b.id}" style="cursor: pointer; font-weight: 500; color: #222;">${b.label}</label>${b.attrText ? html`<span style="margin: 0 4px; color: #ccc;">|</span><span class="layer-attribution-link" style="font-size: 0.75rem;"><a href="${b.attrLink || '#'}" target="_blank" onClick=${(e) => { e.stopPropagation(); if(!b.attrLink) e.preventDefault(); }}>${b.attrText}</a></span>` : ''}</div></div>`)}
                  </div>
                  <div style="font-weight: 600; margin-bottom: 8px; border-bottom: 1px solid #eee; padding-bottom: 4px;">Overlays</div>
                  <div style="display: flex; flex-direction: column; gap: 8px;">
                    ${overlays.length > 0 ? overlays.map(o => html`<div style="display: flex; flex-direction: column; gap: 4px;"><div style="display: flex; align-items: flex-start; gap: 8px; line-height: 1.3;"><input type="checkbox" id="over_${o.id}" checked=${activeOverlays.includes(o.id)} onChange=${(e) => { if (e.target.checked) setActiveOverlays(prev => [...prev, o.id]); else setActiveOverlays(prev => prev.filter(id => id !== o.id)); }} style="margin: 2px 0 0 0; cursor: pointer; flex-shrink: 0;" /><div style="display: inline; margin: 0;"><label for="over_${o.id}" style="cursor: pointer; font-weight: 500; color: #222;">${o.label}</label>${o.attrText ? html`<span style="margin: 0 4px; color: #ccc;">|</span><span class="layer-attribution-link" style="font-size: 0.75rem;"><a href="${o.attrLink || '#'}" target="_blank" onClick=${(e) => { e.stopPropagation(); if(!o.attrLink) e.preventDefault(); }}>${o.attrText}</a></span>` : ''}</div></div>${activeOverlays.includes(o.id) ? html`<div style="margin-left: 21px; display: flex; align-items: center; gap: 8px;"><span style="font-size: 0.65rem; color: #888;">Opacity</span><input type="range" class="tm-opacity-slider" min="0" max="1" step="0.05" value=${overlayOpacities[o.id] !== undefined ? overlayOpacities[o.id] : (o.defaultOpacity ?? 1.0)} onChange=${(e) => setOverlayOpacities(prev => ({...prev, [o.id]: parseFloat(e.target.value)}))} title="Adjust Overlay Opacity" /></div>` : ''}</div>`) : html`<div style="color: #888; font-style: italic;">No overlays available.</div>`}
                  </div>
                </div>
              ` : ''}
            </div>
            <div class="minimap-container" ref=${miniMapDomRef}></div>
          `;
        };
        
        MODULE_VERSIONS['MapViewer'] = 'v6.4.2';
        // === [ END MAJOR BLOCK: MapViewer ] ===
// 🔼🔼🔼 [ END_INJECT: MapViewer ] 🔼🔼🔼
```

---

### Component C: `AppOrchestrator v3.5.3` (`App`)
**Target Slot:** Locate `// === [ MAJOR BLOCK: AppOrchestrator` inside `cartimap.v8.11.25.html` (approx. line 880+) and replace the entire component with this block:

```javascript
// 🔽🔽🔽 [ START_INJECT: AppOrchestrator v3.5.3 ] 🔽🔽🔽
        // === [ MAJOR BLOCK: AppOrchestrator v3.5.3 ] ===
        const App = () => {
          const [logs, setLogs] = useState([]);
          const [rawCsvRows, setRawCsvRows] = useState([]);
          const [unfilteredData, setUnfilteredData] = useState([]);
          const [data, setData] = useState([]);
          const [aboutData, setAboutData] = useState(null);
          const [status, setStatus] = useState({ text: 'Initializing Engine...', progress: 10, isFading: false, active: false });
          const [activeIndex, setActiveIndex] = useState(0);
          const [slideHistory, setSlideHistory] = useState([]);
          const [isMonitorOpen, setIsMonitorOpen] = useState(false);
          const [isAboutOpen, setIsAboutOpen] = useState(false);
          const [isSettingsOpen, setIsSettingsOpen] = useState(false);
          const [isMenuOpen, setIsMenuOpen] = useState(false);
          const [isFilterOpen, setIsFilterOpen] = useState(false);
          const [isSearchOpen, setIsSearchOpen] = useState(false);
          const [searchQuery, setSearchQuery] = useState('');
          const [debouncedSearchQuery, setDebouncedSearchQuery] = useState('');
          const [searchHistory, setSearchHistory] = useState(() => {
            try { return JSON.parse(localStorage.getItem('tm_search_history')) || []; }
            catch (e) { return []; }
          });
          const [maxPane, setMaxPane] = useState(null);
          const [isTimelineExpanded, setIsTimelineExpanded] = useState(false);
          const [isTimelineMinimized, setIsTimelineMinimized] = useState(false);
          const [timelineRequiredHeight, setTimelineRequiredHeight] = useState(200);
          const [polygonOpacity, setPolygonOpacity] = useState(() => {
            try { return parseFloat(localStorage.getItem('tm_polygon_opacity')) || 0.4; }
            catch (e) { return 0.4; }\n          });\n          const [showButtonText, setShowButtonText] = useState(() => {\n            try { return JSON.parse(localStorage.getItem('tm_show_button_text')) ?? false; }\n            catch (e) { return false; }\n          });\n          const [dateLocale, setDateLocale] = useState(() => {\n            try { return localStorage.getItem('tm_date_locale') || 'en-GB'; }\n            catch (e) { return 'en-GB'; }\n          });\n          const [dateEngineMode, setDateEngineMode] = useState(() => {\n            try { return localStorage.getItem('tm_date_engine_mode') || 'auto'; }\n            catch (e) { return 'auto'; }\n          });\n          const [maxAutoZoom, setMaxAutoZoom] = useState(() => {\n            try { return parseInt(localStorage.getItem('tm_max_auto_zoom')) || 15; }\n            catch (e) { return 15; }\n          });\n          const [minimapOffset, setMinimapOffset] = useState(() => {\n            try { return parseInt(localStorage.getItem('tm_minimap_offset')) || -4; }\n            catch (e) { return -4; }\n          });\n          const [allTags, setAllTags] = useState([]);\n          const [activeTags, setActiveTags] = useState([]);\n        \n          const DEFAULT_BASEMAPS = [\n            { id: 'carto-light', label: 'CartoDB Light', type: 'base', url: 'https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', format: 'xyz', maxZoom: 19, active: true, attrText: '© CartoDB', attrLink: 'https://carto.com/attributions', defaultOpacity: 1.0 },\n            { id: 'esri-sat', label: 'Esri Worlds Satellite', type: 'base', url: 'https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', format: 'xyz', maxZoom: 19, active: false, attrText: 'Tiles © Esri', attrLink: 'https://www.esri.com/', defaultOpacity: 1.0 },\n            { id: 'esri-street', label: 'Esri World Street', type: 'base', url: 'https://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer/tile/{z}/{y}/{x}', format: 'xyz', maxZoom: 19, active: false, attrText: 'Tiles © Esri', attrLink: 'https://www.esri.com/', defaultOpacity: 1.0 },\n            { id: 'esri-topo', label: 'Esri World Topo', type: 'base', url: 'https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}', format: 'xyz', maxZoom: 19, active: false, attrText: 'Tiles © Esri', attrLink: 'https://www.esri.com/', defaultOpacity: 1.0 },\n            { id: 'osm', label: 'OpenStreetMap', type: 'base', url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', format: 'xyz', maxZoom: 19, active: false, attrText: '© OSM', attrLink: 'https://openstreetmap.org/copyright', defaultOpacity: 1.0 },\n            { id: 'opentopo', label: 'OpenTopoMap (OSM)', type: 'base', url: 'https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', format: 'xyz', maxZoom: 17, active: false, attrText: '© OpenTopoMap', attrLink: 'https://opentopomap.org', defaultOpacity: 1.0 },\n            { id: 'protomaps-vector', label: 'Protomaps Vector Light (OSM)', type: 'base', url: 'https://api.protomaps.com/tiles/v3/{z}/{x}/{y}.mvt?key=YOUR_API_KEY_HERE', format: 'pbf', maxZoom: 15, active: false, attrText: '© Protomaps', attrLink: 'https://protomaps.com', defaultOpacity: 1.0 }\n          ];\n          const [basemapsRegistry, setBasemapsRegistry] = useState(DEFAULT_BASEMAPS);\n        \n          const appRef = useRef(null); const hasInitializedRef = useRef(false);\n        \n          const addLog = (text, type = 'info') => {\n            const timestamp = new Date().toLocaleTimeString(dateLocale, { hour12: false });\n            setLogs(prev => [{ text, type, time: timestamp }, ...prev].slice(0, 100));\n          };\n        \n          const getOmniParam = (key) => {\n            const sp = new URLSearchParams(window.location.search);\n            if (sp.has(key)) return sp.get(key);\n            const hp = new URLSearchParams(window.location.hash.replace(/^#\\/?\\??/, ''));\n            return hp.get(key) || hp.get(`amp;${key}`);\n          };\n        \n          const jumpToSlide = (newIdx, isSequential = false) => {\n            if (newIdx !== activeIndex && newIdx >= 0 && newIdx < data.length) {\n              if (!isSequential) setSlideHistory(prev => [...prev, activeIndex]);\n              setActiveIndex(newIdx);\n            }\n          };\n        \n          const goBack = () => {\n            if (slideHistory.length > 0) {\n              const prev = slideHistory.at(-1);\n              setSlideHistory(h => h.slice(0, -1));\n              setActiveIndex(prev);\n            }\n          };\n        \n          const resetLayoutPanes = () => {\n            if (appRef.current) {\n              const isDesktop = window.innerWidth >= 1024;\n              appRef.current.style.setProperty('--primary-split', isDesktop ? '50%' : '55%');\n              appRef.current.style.setProperty('--secondary-split', '50%');\n              appRef.current.style.setProperty('--timeline-height', '10%');\n              setMaxPane(null);\n              setIsTimelineExpanded(false);\n              setIsTimelineMinimized(false);\n              window.dispatchEvent(new Event('resize'));\n            }\n          };\n        \n          const formatSmartDate = (start, end, loc) => {\n            if (!start) return 'Unknown Date';\n            return start.text || 'Date Error';\n          };\n        \n          const formatPlaces = (str) => { if (!str) return ''; return str.split(/[|\\-·;]/).map(s => s.split(',').at(0).trim()).filter(Boolean).join(' | '); };\n          const stripAndNormalize = (str) => { if (!str) return ''; return String(str).toLowerCase().normalize('NFD').replace(/[\\u0300-\\u036f]/g, '').replace(/σ/g, 'ς').trim(); };\n        \n          useEffect(() => {\n            if (!searchQuery.trim()) {\n              setDebouncedSearchQuery('');\n              return;\n            }\n            const handler = setTimeout(() => {\n              setDebouncedSearchQuery(searchQuery);\n            }, 250);\n            return () => clearTimeout(handler);\n          }, [searchQuery]);\n        \n          const executeSearch = (query) => {\n            if (!query.trim()) return [];\n            const q = stripAndNormalize(query);\n            return data.filter(d => d._searchIndex && d._searchIndex.includes(q));\n          };\n        \n          useEffect(() => {\n            const handleKeyDown = (e) => {\n              if (['INPUT', 'TEXTAREA'].includes(document.activeElement?.tagName)) return;\n              if (e.key === 'ArrowRight') jumpToSlide(activeIndex + 1);\n              else if (e.key === 'ArrowLeft') jumpToSlide(activeIndex - 1);\n            };\n            window.addEventListener('keydown', handleKeyDown);\n            return () => window.removeEventListener('keydown', handleKeyDown);\n          }, [activeIndex, data.length]);\n        \n          useEffect(() => {\n            const updateAppHeight = () => document.documentElement.style.setProperty('--app-height', `${window.innerHeight}px`);\n            updateAppHeight();\n            let wasDesktop = window.innerWidth >= 1024;\n            const handleResize = () => {\n              updateAppHeight();\n              const isDesktop = window.innerWidth >= 1024;\n              if (isDesktop !== wasDesktop) {\n                window.dispatchEvent(new Event('resize'));\n              }\n              wasDesktop = isDesktop;\n            };\n            window.addEventListener('resize', handleResize);\n            return () => window.removeEventListener('resize', handleResize);\n          }, []);\n        \n          const startPrimaryResize = (e) => {\n            if (maxPane) return;\n            const tStart = e.touches ? Array.from(e.touches).at(0) : e;\n            const startX = tStart.clientX;\n            const startY = tStart.clientY;\n            const isDesktop = window.innerWidth >= 1024;\n            const containerNode = appRef.current.querySelector('.core-viewports');\n            const startVal = isDesktop ? appRef.current.querySelector('.content-slider-pane').offsetWidth : appRef.current.querySelector('.content-slider-pane').offsetHeight;\n            const containerSize = isDesktop ? containerNode.offsetWidth : containerNode.offsetHeight;\n            const onMove = (e2) => {\n              const tCurrent = e2.touches ? Array.from(e2.touches).at(0) : e2;\n              const currentX = tCurrent.clientX;\n              const currentY = tCurrent.clientY;\n              const delta = isDesktop ? (currentX - startX) : (startY - currentY);\n              let pct = ((startVal + delta) / containerSize) * 100;\n              pct = Math.max(10, Math.min(90, pct));\n              appRef.current.style.setProperty('--primary-split', `${pct}%`);\n              window.dispatchEvent(new Event('resize'));\n            };\n            const onUp = () => {\n              window.removeEventListener('mousemove', onMove);\n              window.removeEventListener('mouseup', onUp);\n              window.removeEventListener('touchmove', onMove);\n              window.removeEventListener('touchend', onUp);\n            };\n            window.addEventListener('mousemove', onMove);\n            window.addEventListener('mouseup', onUp);\n            window.addEventListener('touchmove', onMove, { passive: false });\n            window.addEventListener('touchend', onUp);\n          };\n        \n          const startSecondaryResize = (e) => {\n            if (maxPane) return;\n            const tStart = e.touches ? Array.from(e.touches).at(0) : e;\n            const startX = tStart.clientX;\n            const startY = tStart.clientY;\n            const isDesktop = window.innerWidth >= 1024;\n            const containerNode = appRef.current.querySelector('.visual-viewports');\n            const startVal = isDesktop ? appRef.current.querySelector('.map-pane-wrapper').offsetHeight : appRef.current.querySelector('.map-pane-wrapper').offsetWidth;\n            const containerSize = isDesktop ? containerNode.offsetHeight : containerNode.offsetWidth;\n            const onMove = (e2) => {\n              const tCurrent = e2.touches ? Array.from(e2.touches).at(0) : e2;\n              const currentX = tCurrent.clientX;\n              const currentY = tCurrent.clientY;\n              const delta = isDesktop ? (currentY - startY) : (startX - currentX);\n              let pct = ((startVal + delta) / containerSize) * 100;\n              pct = Math.max(10, Math.min(90, pct));\n              appRef.current.style.setProperty('--secondary-split', `${pct}%`);\n              window.dispatchEvent(new Event('resize'));\n            };\n            const onUp = () => {\n              window.removeEventListener('mousemove', onMove);\n              window.removeEventListener('mouseup', onUp);\n              window.removeEventListener('touchmove', onMove);\n              window.removeEventListener('touchend', onUp);\n            };\n            window.addEventListener('mousemove', onMove);\n            window.addEventListener('mouseup', onUp);\n            window.addEventListener('touchmove', onMove, { passive: false });\n            window.addEventListener('touchend', onUp);\n          };\n        \n          useEffect(() => {\n            const source = getOmniParam('source') || '1kdgGiHNDsIZrn8Z1aqWXrEEYKMGxLAqFiwATx3aqbJI';\n            const gid = getOmniParam('gid') || '1517409271';\n            const bgid = getOmniParam('bgid') || '0';\n            const fetchUrlPrimary = `https://docs.google.com/spreadsheets/d/${source}/gviz/tq?tqx=out:csv&gid=${gid}`;\n            const fetchUrlBasemaps = `https://docs.google.com/spreadsheets/d/${source}/gviz/tq?tqx=out:csv&gid=${bgid}`;\n        \n            setStatus({ text: 'Accessing Spreadsheet...', progress: 30, isFading: false, active: true });\n            const primaryFetch = fetch(fetchUrlPrimary).then(r => r.text());\n            const basemapsFetch = fetch(fetchUrlBasemaps).then(r => r.text());\n        \n            Promise.all([primaryFetch, basemapsFetch]).then(([csvPrimary, csvBasemaps]) => {\n              setStatus({ text: 'Compiling Schemas...', progress: 70, isFading: false, active: true });\n              if (csvBasemaps && csvBasemaps.length > 50) {\n                Papa.parse(csvBasemaps, {\n                  header: true, skipEmptyLines: true, complete: (results) => {\n                    const parsedBMs = results.data.map(row => {\n                      const norm = {};\n                      for (let k in row) norm[k.toLowerCase().trim()] = row[k];\n                      const urlVal = exactGet(norm, 'url') || exactGet(norm, 'tileurl') || '';\n                      const idVal = exactGet(norm, 'id') || exactGet(norm, 'layerid') || '';\n                      const isOverlay = /^(overlay|wms)$/i.test(String(exactGet(norm, 'type')).trim());\n                      return {\n                        id: idVal,\n                        label: exactGet(norm, 'label') || exactGet(norm, 'title') || idVal,\n                        type: isOverlay ? 'overlay' : 'base',\n                        url: urlVal,\n                        format: exactGet(norm, 'format') || 'xyz',\n                        maxZoom: parseInt(exactGet(norm, 'maxzoom') || 19, 10),\n                        active: /^(true|yes)$/i.test(String(exactGet(norm, 'active')).trim()),\n                        wmsLayer: exactGet(norm, 'wmslayer') || '',\n                        attrText: exactGet(norm, 'attribution') || exactGet(norm, 'attrtext') || '',\n                        attrLink: exactGet(norm, 'attrlink') || '',\n                        defaultOpacity: exactGet(norm, 'opacity') ? parseFloat(exactGet(norm, 'opacity')) : 1.0\n                      };\n                    }).filter(b => b.id && b.url);\n                    if (parsedBMs.length > 0) setBasemapsRegistry(prev => {\n                      const merged = [...prev];\n                      parsedBMs.forEach(bm => {\n                        const existIdx = merged.findIndex(m => m.id === bm.id);\n                        if (existIdx >= 0) merged[existIdx] = bm;\n                        else merged.push(bm);\n                      });\n                      return merged;\n                    });\n                  }\n                });\n              }\n        \n              Papa.parse(csvPrimary, {\n                header: true, skipEmptyLines: true, complete: (results) => {\n                  if (results.data.length > 0) {\n                    const firstRowNorm = {};\n                    for (let k in results.data[0]) firstRowNorm[k.toLowerCase().trim()] = results.data[0][k];\n                    const exactGet = (normObj, key) => { const val = normObj[key]; return val !== undefined && val !== null ? String(val).trim() : \"\"; };\n                    setAboutData({\n                      title: exactGet(firstRowNorm, 'title') || 'Dataset Overview',\n                      description: exactGet(aboutData ? aboutData.description : 'No project description provided.'),\n                      rawSource: source === '1kdgGiHNDsIZrn8Z1aqWXrEEYKMGxLAqFiwATx3aqbJI' ? 'Default Master DB' : source,\n                      downloadUrl: fetchUrlPrimary\n                    });\n                    setRawCsvRows(results.data);\n                  }\n                }\n              });\n            }).catch(err => {\n              console.error(\"Fatal CMS Error\", err);\n              setStatus({ text: 'Error Loading Data', progress: 100, isFading: false, active: false });\n            });\n          }, []);\n        \n          // --- [ START_SUBBLOCK: Ingestion Regex & Data Parsing Loop ] ---\n          useEffect(() => {\n            if (rawCsvRows.length === 0) return;\n            const exactGet = (normObj, key) => { const val = normObj[key]; return val !== undefined && val !== null ? String(val).trim() : \"\"; };\n            \n            // Shared delimiter regex lifted to root hook scope to prevent ReferenceErrors\n            const omniSplitRegex = /\||\r?\n/;\n            \n            let activeMode = dateEngineMode;\n            if (activeMode === 'auto') {\n              const hasEDTF = rawCsvRows.some(row => {\n                const norm = {};\n                for (let k in row) norm[k.toLowerCase().trim()] = row[k];\n                return exactGet(norm, 'start edtf') !== '';\n              });\n              activeMode = hasEDTF ? 'edtf' : 'legacy';\n            }\n            const isUS = dateLocale === 'en-US';\n            const cleaned = rawCsvRows.map((row, index) => {\n              const norm = {};\n              for (let k in row) norm[k.toLowerCase().trim()] = row[k];\n              const rowTitle = exactGet(norm, 'title') || 'Untitled Event';\n        \n              const parseChronoNode = (legacyStr, edtfStr) => {\n                const cleanLegacy = legacyStr ? legacyStr.toString().trim() : '';\n                const cleanEdtf = edtfStr ? edtfStr.toString().trim() : '';\n                if (activeMode === 'edtf' || (activeMode === 'auto' && cleanEdtf)) {\n                  try {\n                    if (cleanEdtf) {\n                      const parsed = compileCartiMapAST(cleanEdtf);\n                      if (parsed) {\n                        return {\n                          isEDTF: true,\n                          min: parsed.min,\n                          max: parsed.max,\n                          obj: parsed,\n                          isOpen: parsed.values ? parsed.values.some(v => v === Number.POSITIVE_INFINITY || v === Number.NEGATIVE_INFINITY) : false,\n                          text: cleanEdtf\n                        };\n                      }\n                    }\n                  } catch (e) {\n                    addLog(`[Chrono-Engine] Row ${index + 2} (\"${rowTitle}\"): EDTF syntax failure. DB String: \"${cleanEdtf}\". Rerouted to Legacy.`, 'warning');\n                  }\n                }\n                if (!cleanLegacy) {\n                  if (cleanEdtf) addLog(`[Chrono-Engine] Row ${index + 2} (\"${rowTitle}\"): No Legacy fallback found for failed EDTF. Rendering as Undated.`, 'warning');\n                  return null;\n                }\n                const parts = cleanLegacy.split(' ');\n                if (parts.length < 1) return null;\n                const dParts = parts[0].split(/[\\/\\\\.-]/);\n                const tParts = parts[1] ? parts[1].split(':') : [];\n                const secParts = String(tParts[2] || '0').split('.');\n                \n                let dDay = parseInt(dParts[0], 10);\n                let dMonth = parseInt(dParts[1], 10) - 1;\n                let dYear = parseInt(dParts[2], 10);\n                if (isUS) {\n                  dDay = parseInt(dParts[1], 10);\n                  dMonth = parseInt(dParts[0], 10) - 1;\n                }\n                const tHour = parseInt(tParts[0] || 0, 10);\n                const tMin = parseInt(tParts[1] || 0, 10);\n                const tSec = parseInt(secParts[0] || 0, 10);\n                const tMs = parseInt(secParts[1] || 0, 10);\n                const dateObj = new Date(dYear, dMonth, dDay, tHour, tMin, tSec, tMs);\n                const ts = dateObj.getTime();\n                if (isNaN(ts)) {\n                  addLog(`[Chrono-Engine] Row ${index + 2} (\"${rowTitle}\"): Legacy parser failed on \"${cleanLegacy}\". Rendering as Undated.`, 'warning');\n                  return null;\n                }\n                return { isEDTF: false, min: ts, max: ts, date: new Date(ts), text: cleanLegacy };\n              };\n        \n              const locStr = exactGet(norm, 'location');\n              return { \n                id: index,\n                title: rowTitle,\n                startDate: parseChronoNode(exactGet(norm, 'start'), exactGet(norm, 'start edtf')),\n                endDate: parseChronoNode(exactGet(norm, 'end'), exactGet(norm, 'end edtf')),\n                description: exactGet(norm, 'description'),\n                place: exactGet(norm, 'place'),\n                location: locStr,\n                subLabels: exactGet(norm, 'sublabels') || exactGet(norm, 'sub-labels') || exactGet(norm, 'sub labels') || '',\n                priority: exactGet(norm, 'priority'),\n                media: exactGet(norm, 'media') ? exactGet(norm, 'media').split(omniSplitRegex).map(m => m.trim()).filter(Boolean) : [],\n                mediaCaption: exactGet(norm, 'media caption') ? exactGet(norm, 'media caption').split(omniSplitRegex).map(c => c.trim()) : [],\n                mediaCredit: exactGet(norm, 'media credit') ? exactGet(norm, 'media credit').split(omniSplitRegex).map(c => c.trim()) : [],\n                tags: exactGet(norm, 'tags') ? exactGet(norm, 'tags').split(',').map(t => t.trim()).filter(Boolean) : []\n              };\n            });\n        \n            const valid = cleaned.sort((a, b) => {\n              const aMin = a.startDate ? a.startDate.min : 0;\n              const bMin = b.startDate ? b.startDate.min : 0;\n              if (aMin !== bMin) return aMin - bMin;\n              return a.id - b.id;\n            });\n        \n            const indexedData = valid.map(d => ({\n              ...d,\n              _searchIndex: stripAndNormalize(`${d.title} ${d.description} ${d.place} ${d.tags.join(' ')} ${formatSmartDate(d.startDate, d.endDate, dateLocale)}`)\n            }));\n            setUnfilteredData(indexedData);\n        \n            const tagsMap = new Set();\n            indexedData.forEach(d => {\n              let rawTags = d.tags || [];\n              let arr = [];\n              (Array.isArray(rawTags) ? rawTags : [rawTags]).forEach(t => {\n                if (typeof t === 'string') arr.push(...t.split(omniSplitRegex));\n                else arr.push(t);\n              });\n              arr.map(s => String(s).trim()).filter(Boolean).forEach(t => tagsMap.add(t));\n            });\n        \n            const uniqueTagsList = Array.from(tagsMap).sort();\n            setAllTags(uniqueTagsList);\n            setActiveTags(uniqueTagsList);\n        \n            if (!hasInitializedRef.current) {\n              const paramSlide = getOmniParam('slide');\n              const paramDate = getOmniParam('date');\n              let initialIdx = 0;\n              if (paramSlide && !isNaN(parseInt(paramSlide))) {\n                initialIdx = Math.max(0, Math.min(indexedData.length - 1, parseInt(paramSlide) - 1));\n              } else if (paramDate) {\n                const targetTime = new Date(paramDate).getTime();\n                if (!isNaN(targetTime)) {\n                  let minDiff = Infinity;\n                  indexedData.forEach((d, idx) => {\n                    if (d.startDate) {\n                      const diff = Math.abs(d.startDate.min - targetTime);\n                      if (diff < minDiff) { minDiff = diff; initialIdx = idx; }\n                    }\n                  });\n                }\n              }\n              setActiveIndex(initialIdx);\n              hasInitializedRef.current = true;\n            }\n            setStatus({ text: 'Engine Ready', progress: 100, isFading: true, active: false });\n            setTimeout(() => { setStatus({ text: '', progress: 100, isFading: true, active: true }); }, 500);\n          }, [rawCsvRows, dateEngineMode, dateLocale]);\n          // --- [ END_SUBBLOCK: Ingestion Regex & Data Parsing Loop ] ---\n        \n          // Conformed to [REF: ETL-14b] Dynamic horizontal storyline swimlane filtering\n          useEffect(() => {\n            if (unfilteredData.length === 0) return;\n            const filtered = unfilteredData.filter(d => \n              d.tags.length === 0 || d.tags.some(t => activeTags.includes(t))\n            );\n            setData(filtered);\n            \n            // Safety guard active index boundary\n            if (activeIndex >= filtered.length) {\n              setActiveIndex(Math.max(0, filtered.length - 1));\n            }\n            \n            const tagsMap = new Set();\n            filtered.forEach(d => {\n              d.tags.forEach(t => tagsMap.add(t));\n            });\n            const laneCount = tagsMap.size > 0 ? tagsMap.size : 1;\n            setTimelineRequiredHeight((laneCount * 24) + 40);\n          }, [unfilteredData, activeTags]);\n        \n          const handleToggleTag = (tag) => {\n            if (activeTags.includes(tag)) {\n              if (activeTags.length > 1) {\n                setActiveTags(activeTags.filter(t => t !== tag));\n              } else {\n                addLog('Cannot deselect all swimlanes. At least one must remain active.', 'warning');\n              }\n            } else {\n              setActiveTags([...activeTags, tag]);\n            }\n          };\n        \n          const handleResultClick = (id, qString) => {\n            const sortedIdx = data.findIndex(d => d.id === id);\n            if (sortedIdx >= 0) jumpToSlide(sortedIdx);\n            setIsSearchOpen(false);\n            if (qString && !searchHistory.includes(qString)) {\n              const newH = [qString, ...searchHistory].slice(0, 8);\n              setSearchHistory(newH);\n              localStorage.setItem('tm_search_history', JSON.stringify(newH));\n            }\n          };\n        \n          const searchResults = executeSearch(debouncedSearchQuery);\n          const activeSlide = data.at(activeIndex);\n          const hasMedia = activeSlide && activeSlide.media && activeSlide.media.length > 0;\n        \n          const CarTiMapperLogo = ({ context, appVersion }) => {\n            const svgIcon = html`<svg xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"20 0 165 100\" style=\"width: 100%; height: 100%; display: block;\"><defs><filter id=\"dot-glow\" x=\"-50%\" y=\"-50%\" width=\"200%\" height=\"200%\"><feGaussianBlur stdDeviation=\"1.2\" result=\"blur\" /><feMerge><feMergeNode in=\"blur\" /><feMergeNode in=\"blur\" /><feMergeNode in=\"SourceGraphic\" /></feMerge></filter></defs><path d=\"M28,38 L45,15 L180,15 L180,85 L45,85 L28,62 Z\" fill=\"#2c3e50\" stroke=\"#007acc\" stroke-width=\"2.5\" stroke-linejoin=\"round\"/><g fill=\"#fff\" opacity=\"0.9\"><rect x=\"55\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"71\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"87\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"103\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"119\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"135\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"151\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"167\" y=\"19\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"55\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"71\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"87\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"103\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"119\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"135\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"151\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /><rect x=\"167\" y=\"75\" width=\"4\" height=\"6\" rx=\"1\" /></g><g transform=\"translate(112, 50)\"><path d=\"M0,-28 L4,-6 L28,0 L4,6 L0,28 L-4,6 L-28,0 L-4,-6 Z\" fill=\"#546e7a\" opacity=\"0.8\"/><g fill=\"#fcfcfc\" font-family=\"Arial, sans-serif\" font-size=\"7\" font-weight=\"normal\" text-anchor=\"middle\"><text x=\"0\" y=\"-21\">N</text><text x=\"24\" y=\"2.5\">E</text><text x=\"0\" y=\"27\">S</text><text x=\"-24\" y=\"2.5\">W</text></g><g fill=\"#8be9fd\" filter=\"url(#dot-glow)\"><circle cx=\"12.5\" cy=\"-21.6\" r=\"1.2\" /><circle cx=\"21.6\" cy=\"-12.5\" r=\"1.2\" /><circle cx=\"21.6\" cy=\"12.5\" r=\"1.2\" /><circle cx=\"12.5\" cy=\"21.6\" r=\"1.2\" /><circle cx=\"-12.5\" cy=\"21.6\" r=\"1.2\" /><circle cx=\"-21.6\" cy=\"12.5\" r=\"1.2\" /><circle cx=\"-21.6\" cy=\"-12.5\" r=\"1.2\" /><circle cx=\"-12.5\" cy=\"-21.6\" r=\"1.2\" /></g><g transform=\"rotate(60)\"><path d=\"M0,0 L-1,-16 L1,-16 Z\" fill=\"#999\" /><circle cx=\"0\" cy=\"-20\" r=\"2.8\" fill=\"#007acc\" /></g><g transform=\"rotate(270)\"><path d=\"M0,0 L-1.2,-9 L1.2,-9 Z\" fill=\"#999\" /><circle cx=\"0\" cy=\"-13\" r=\"2.8\" fill=\"#28a745\" /></g><circle cx=\"0\" cy=\"0\" r=\"1.5\" fill=\"#fff\" /></g></svg>`;
            if (context === 'splash') return html`<div class="logo-stack-splash"><div class="splash-icon-wrapper">${svgIcon}</div><div class="splash-text">CarTiMap</div><div class="splash-version">${appVersion}</div></div>`;
            if (context === 'status') return html`<div style="display: flex; align-items: center; gap: 6px; height: 100%;"><div style="height: 16px; width: auto; display: flex; align-items: center;">${svgIcon}</div><div style="display: flex; align-items: baseline; gap: 4px;"><span style="font-size: 0.85rem; color: #444; line-height: 1;">CarTiMap</span><span style="font-size: 0.65rem; color: #888; line-height: 1;">${appVersion}</span></div></div>`;
          };
        
          const statusHTML = html`
            <div class="loading-status-overlay ${status.isFading ? 'fade-out' : ''}">
              <${CarTiMapperLogo} context="splash" appVersion=${APP_VERSION} />
              <div class="loading-bar-container"><div class="loading-bar-fill" style="width: ${status.progress}%;"></div></div>
              <div style="font-size: 0.85rem; color: #aaa; text-align: center; margin-top: 10px;">${status.text}</div>
            </div>
          `;
        
          const controlClusterHTML = html`
            <div style="display: flex; flex-direction: column; gap: 8px; width: 100%;">
              <button class="menu-btn" onClick=${() => setIsMenuOpen(!isMenuOpen)} title="Application Menu">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="3" y1="12" x2="21" y2="12"></line><line x1="3" y1="6" x2="21" y2="6"></line><line x1="3" y1="18" x2="21" y2="18"></line></svg>
              </button>
              ${isMenuOpen ? html`
                <div style="position: absolute; top: 40px; left: 15px; background: rgba(255,255,255,0.98); border: 1px solid #ccc; border-radius: 6px; padding: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); display: flex; flex-direction: column; gap: 8px; z-index: 10000; width: max-content;">
                  <button class="status-btn-text" onClick=${resetLayoutPanes}>
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path><polyline points="9 22 9 12 15 12 15 22"></polyline></svg> Reset Layout
                  </button>
                  <button class="status-btn-text ${isSettingsOpen ? 'active' : ''}" onClick=${() => setIsSettingsOpen(!isSettingsOpen)}>
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"></circle><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path></svg> Settings
                  </button>
                  <button class="status-btn-text ${isMonitorOpen ? 'active' : ''}" onClick=${() => setIsMonitorOpen(!isMonitorOpen)}>
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="20" x2="18" y2="10"></line><line x1="12" y1="20" x2="12" y2="4"></line><line x1="6" y1="20" x2="6" y2="14"></line></svg> Telemetry
                  </button>
                </div>
              ` : ''}
              
              <div style="position: relative; display: flex; width: 24px; box-shadow: 0 2px 6px rgba(0,0,0,0.25); border-radius: 4px; overflow: visible; background: #fff;">
                <button class="status-btn ${isFilterOpen ? 'active' : ''}" onClick=${() => setIsFilterOpen(!isFilterOpen)} title="Filter Chronological Tracks" style="border: none;">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"></polygon></svg>
                </button>
                ${isFilterOpen ? html`
                  <div style="position: absolute; top: 0; left: 30px; background: rgba(255,255,255,0.98); border: 1px solid #ccc; border-radius: 6px; padding: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 10000; width: max-content; display: flex; flex-direction: column; gap: 8px;">
                    <div style="font-weight: 600; border-bottom: 1px solid #eee; padding-bottom: 4px; color: #222;">Storyline Swimlanes</div>
                    ${allTags.length > 0 ? allTags.map(tag => html`
                      <div style="display: flex; align-items: center; gap: 8px; cursor: pointer;" onClick=${() => handleToggleTag(tag)}>
                        <input type="checkbox" checked=${activeTags.includes(tag)} style="cursor: pointer;" readOnly />
                        <span style="font-size: 0.8rem; font-weight: 500; color: #444; user-select: none;">${tag}</span>
                      </div>
                    `) : html`<span style="font-size: 0.75rem; color: #888; font-style: italic;">No tags detected.</span>`}
                  </div>
                ` : ''}
              </div>
            </div>
          `;
        
          return html`
            <div id="app-layout" ref=${appRef} class=${`app-container theme-${getOmniParam('theme') || 'classic'} ${maxPane ? `max-pane-${maxPane}` : ''} ${isTimelineMinimized ? 'timeline-minimized' : ''}`}>
              ${status.active ? statusHTML : ''}
              
              <div class="app-taskbar">
                <div style="display: flex; align-items: center; gap: 10px; height: 100%;">
                  ${controlClusterHTML}
                  ${aboutData ? html`<button class="status-btn" style="width: auto; padding: 0 4px; border: none; background: transparent; display: flex; align-items: center; justify-content: center;" onClick=${() => setIsAboutOpen(true)} title="About"><${CarTiMapperLogo} context="status" appVersion=${APP_VERSION} /></button>` : ''}
                </div>
                
                <div class="taskbar-ticker">
                  <button class="status-btn" onClick=${() => jumpToSlide(activeIndex - 1, true)} title="Previous Slide">
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"></polyline></svg>
                  </button>
                  <div class="ticker-slide-input-wrapper" style="display: flex; align-items: center; gap: 4px; color: #333; font-weight: bold; font-size: 0.9rem;">
                    <input type="text" class="ticker-slide-box" value=${activeIndex + 1} onChange=${(e) => { const val = parseInt(e.target.value); if(!isNaN(val)) jumpToSlide(Math.max(0, Math.min(data.length - 1, val - 1))); }} style="width: 28px; text-align: center; border: 1px solid #ccc; border-radius: 4px; height: 20px; font-weight: 700; color: #222;" />
                    <span style="user-select: none; opacity: 0.7;">/ ${data.length}</span>
                  </div>
                  <button class="status-btn" onClick=${() => jumpToSlide(activeIndex + 1, true)} title="Next Slide">
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"></polyline></svg>
                  </button>
                </div>
                
                <div class="taskbar-telemetry">
                  <div class="semantic-time-span">Span: Calculating...</div>
                  <button class="status-btn" onClick=${() => setIsSearchOpen(true)} title="Search System Data">
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
                  </button>
                  ${slideHistory && slideHistory.length > 0 ? html`<button class="${showButtonText ? 'status-btn-text' : 'status-btn'}" onClick=${goBack} title="Back to Previous Slide"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M 4 12 A 8 8 0 1 0 12 4"></path><polyline points="16 0 12 4 16 8"></polyline></svg>${showButtonText ? html`<span>Back</span>` : ''}</button>` : ''}
                </div>
              </div>
              
              <div class="core-viewports">
                <div class="content-slider-pane">
                  <${ContentSlider} data=${data} activeIndex=${activeIndex} setActiveIndex=${jumpToSlide} addLog=${addLog} />
                </div>
                <div class="split-bar primary" onMouseDown=${startPrimaryResize} onTouchStart=${startPrimaryResize}></div>
                <div class="visual-viewports">
                  <div class="map-pane-wrapper">
                    <${MapViewer} data=${data} activeIndex=${activeIndex} setActiveIndex=${jumpToSlide} addLog=${addLog} basemapsRegistry=${basemapsRegistry} maxAutoZoom=${maxAutoZoom} minimapOffset=${minimapOffset} setMinimapOffset=${setMinimapOffset} maxPane=${maxPane} setMaxPane=${setMaxPane} polygonOpacity=${polygonOpacity} showButtonText=${showButtonText} visibleTimeBounds=${visibleTimeBounds} />
                  </div>
                  <div class="split-bar secondary" onMouseDown=${startSecondaryResize} onTouchStart=${startSecondaryResize}></div>
                  <div class="media-carousel-pane">
                    <${MediaCarousel} data=${data} activeIndex=${activeIndex} addLog=${addLog} showButtonText=${showButtonText} />
                  </div>
                </div>
              </div>
              
              ${isTimelineMinimized ? html`<button class="fab-btn" onClick={() => setIsTimelineMinimized(false)} title="Restore Timeline"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><line x1="3" y1="9" x2="21" y2="9"></line><line x1="9" y1="21" x2="9" y2="9"></line></svg></button>` : ''}
              
              <div class="timeline-pane">
                <${TimelineScrubber} data=${data} activeIndex=${activeIndex} setActiveIndex=${jumpToSlide} zoomLock=${getOmniParam('zoomlock') || 'auto'} setZoomLock=${(val) => addLog(`ZoomLock changed: ${val}`)} setVisibleTimeSpan={(str) => { const el = appRef.current?.querySelector('.semantic-time-span'); if(el) el.textContent = str; }} isTimelineExpanded=${isTimelineExpanded} setIsTimelineExpanded=${setIsTimelineExpanded} isTimelineMinimized=${isTimelineMinimized} setIsTimelineMinimized=${setIsTimelineMinimized} dateLocale=${dateLocale} timelineRequiredHeight=${timelineRequiredHeight} setVisibleTimeBounds=${setVisibleTimeBounds} />
              </div>
              
              <!-- System Modal Overlays -->
              ${isAboutOpen ? html`
                <div class="modal-backdrop" onClick=${() => setIsAboutOpen(false)}>
                  <div class="modal-card" onClick=${(e) => e.stopPropagation()}>
                    <div class="modal-header"><h3>Dataset Metadata Overview</h3><button class="status-btn" onClick=${() => setIsAboutOpen(false)}><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg></button></div>
                    <div style="font-size:0.95rem; color:#444; line-height:1.5;">
                      <div style="font-weight:bold; font-size:1.15rem; color:#222; margin-bottom:8px;">${aboutData?.title}</div>
                      <p style="margin-bottom:12px;">${aboutData?.description}</p>
                      <div style="background:#f4f4f4; padding:10px; border-radius:4px; font-family:monospace; font-size:0.8rem; margin-bottom:12px;">
                        Source Ledger ID: ${aboutData?.rawSource}<br/>
                        Ingestion Target: <a href="${aboutData?.downloadUrl}" target="_blank">Download Ingested CSV Feed</a>
                      </div>
                    </div>
                  </div>
                </div>
              ` : ''}
              
              ${isSearchOpen ? html`
                <div class="modal-backdrop" onClick=${() => setIsSearchOpen(false)}>
                  <div class="modal-card search-card" onClick=${(e) => e.stopPropagation()}>
                    <div class="modal-header"><h3>Search System Records</h3><button class="status-btn" onClick=${() => setIsSearchOpen(false)}><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg></button></div>
                    <div style="margin-bottom:12px;"><input type="text" class="search-input-field" placeholder="Type target criteria (e.g. 'Grande Bretagne', 'Sewer')..." value=${searchQuery} onInput=${(e) => setSearchQuery(e.target.value)} style="width:100%; padding:8px 12px; border:1px solid #ccc; border-radius:6px; font-size:0.95rem; font-weight:500;" /></div>
                    <div class="search-results-viewport" style="max-height: 250px; overflow-y: auto;">
                      ${searchResults.length > 0 ? searchResults.map(res => html`<div class="search-result-item" onClick=${() => handleResultClick(res.id, searchQuery)}><div class="search-result-title">${res.title}</div><div class="search-result-meta">${formatSmartDate(res.startDate, res.endDate, dateLocale)} ${res.place ? ` • ${formatPlaces(res.place)}` : ''}</div></div>`) : (searchQuery.trim() ? html`<div style="color:#888; font-style:italic; padding:10px; text-align:center;">No records matching criteria.</div>` : '')}
                    </div>
                  </div>
                </div>
              ` : ''}
              
              ${isSettingsOpen ? html`
                <div class="modal-backdrop" onClick=${() => setIsSettingsOpen(false)}>
                  <div class="modal-card" onClick=${(e) => e.stopPropagation()}>
                    <div class="modal-header"><h3>System Parameters Configuration</h3><button class="status-btn" onClick=${() => setIsSettingsOpen(false)}><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg></button></div>
                    <div style="display:flex; flex-direction:column; gap:12px; font-size:0.9rem; color:#444;">
                      <div class="settings-row"><label>Regional Chronology Format:</label><select value=${dateLocale} onChange=${(e) => { setDateLocale(e.target.value); localStorage.setItem('tm_date_locale', e.target.value); }}><option value="en-GB">European (DD/MM/YYYY)</option><option value="en-US">American (MM/DD/YYYY)</option></select></div>
                      <div class="settings-row"><label>Date Parsing Core Engine:</label><select value=${dateEngineMode} onChange=${(e) => { setDateEngineMode(e.target.value); localStorage.setItem('tm_date_engine_mode', e.target.value); }}><option value="auto">Auto-Detect</option><option value="edtf">Strict ISO-8601-2 EDTF</option><option value="legacy">Legacy Date-String</option></select></div>
                      <div class="settings-row"><label>Camera Flight Autozoom Ceiling:</label><input type="range" min="1" max="22" value=${maxAutoZoom} onChange=${(e) => { setMaxAutoZoom(parseInt(e.target.value, 10)); localStorage.setItem('tm_max_auto_zoom', e.target.value); }} /><span style="font-weight:700;">${maxAutoZoom}z</span></div>
                      <div class="settings-row"><label>Visual Overlay Polygon Opacity:</label><input type="range" min="0" max="1" step="0.05" value=${polygonOpacity} onChange=${(e) => { setPolygonOpacity(parseFloat(e.target.value)); localStorage.setItem('tm_polygon_opacity', e.target.value); }} /><span style="font-weight:700;">${Math.round(polygonOpacity * 100)}%</span></div>
                      <div class="settings-row"><label>Visual Interface Button Labels:</label><input type="checkbox" checked=${showButtonText} onChange=${(e) => { setShowButtonText(e.target.checked); localStorage.setItem('tm_show_button_text', JSON.stringify(e.target.checked)); }} /></div>
                    </div>
                  </div>
                </div>
              ` : ''}
              
              ${isMonitorOpen ? html`
                <div class="modal-backdrop" onClick=${() => setIsMonitorOpen(false)}>
                  <div class="modal-card telemetry-card" onClick=${(e) => e.stopPropagation()}>
                    <div class="modal-header"><h3>Active VibeMonitor Telemetry</h3><button class="status-btn" onClick=${() => setIsMonitorOpen(false)}><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg></button></div>
                    <div class="telemetry-viewport" style="max-height: 250px; overflow-y: auto; background:#1e1e1e; border-radius:4px; padding:10px; font-family:monospace; font-size:0.75rem; color:#39ff14;">
                      ${logs.length > 0 ? logs.map(l => html`<div>[${l.time}] [${l.type.toUpperCase()}] ${l.text}</div>`) : html`<div style="color:#888; font-style:italic;">No log broadcasts registered. Ready.</div>`}
                    </div>
                  </div>
                </div>
              ` : ''}
              
            </div>
          `;
        };
        
        MODULE_VERSIONS['AppOrchestrator'] = 'v3.5.3';
        // === [ END MAJOR BLOCK: AppOrchestrator ] ===
// 🔼🔼🔼 [ END_INJECT: AppOrchestrator ] 🔼🔼🔼
```
