# Motion & Animation Patterns

This document extends the microinteractions repository with **visible motion and animation patterns** that go beyond subtle feedback. Use these when the goal is to make the interface feel alive, guide attention, and reinforce hierarchy—especially in dashboards, data visualizations, and content-heavy screens.

**Principle:** Motion should be a **clarity layer**, not decoration. It explains what changed, reinforces hierarchy, and builds trust. Always respect `prefers-reduced-motion` and keep timing consistent across the product.

---

## 1. Chart build-in (from baseline)

**When to use:** Any chart (bar, column, line, area, ring) on initial load or when data is first shown.

**What it does:** The chart does **not** start at its final state. Values animate from baseline (zero or a defined start) to the final value, so the user sees the data "build" or "fill in."

**Why it matters:** Static charts feel flat. A short build-in (800–1200 ms) draws attention to the data and makes the screen feel responsive and intentional.

| Chart type     | What animates              | Duration   | Easing   |
|----------------|----------------------------|------------|----------|
| Bar / column   | Height from 0 to value     | 800–1200 ms| ease-out |
| Line / area    | Path draw or opacity/scale | 800–1200 ms| ease-out |
| Progress ring  | stroke-dashoffset          | 500–800 ms | ease-out |
| Pie / donut    | Segment sweep or scale     | 600–1000 ms| ease-out |

**Implementation notes:**
- **CSS:** Use `transform: scaleY(0)` → `scaleY(1)` with `transform-origin: bottom` for bars; use `stroke-dashoffset` for SVG lines/rings.
- **JS:** Interpolate value from 0 to target over 800–1200 ms; use requestAnimationFrame or a library. Google Charts uses `animation.startup: true`; Chart.js uses `animation.duration` (default 1000 ms).
- **Reduced motion:** Show final state immediately (no build-in).

---

## 2. Staggered reveal (sequential entrance)

**When to use:** Lists of cards, stat cards, grid items, menu items, or any set of similar elements that appear together.

**What it does:** Elements do not appear all at once. Each item enters with a small delay after the previous one (e.g. 30–80 ms), creating a cascading reveal that guides the eye and reinforces order.

**Why it matters:** A single "pop" of everything feels abrupt. Stagger creates rhythm and makes the interface feel considered. Overuse (too many items or too long a delay) causes fatigue—keep total time under ~800 ms.

| Parameter       | Recommended        | Notes                                      |
|-----------------|--------------------|--------------------------------------------|
| Delay between   | 30–80 ms (50 ms typical) | Shorter = snappier; longer = more dramatic |
| Max items       | 10–15              | After that, show rest immediately or batch |
| Total duration  | < 800 ms         | 50 ms × 15 ≈ 750 ms                        |
| Per-item motion | opacity 0→1, translateY 8–16px → 0 | Or scale 0.95 → 1                         |

**Implementation notes:**
- **CSS:** `animation-delay: calc(var(--i) * 50ms)` with a custom property or `:nth-child(n)` selectors.
- **JS:** Set `transitionDelay` or use a motion library's stagger helper. Trigger on viewport entry (Intersection Observer) for long lists so only visible items stagger.
- **Reduced motion:** Remove stagger; reveal all with a single short fade or no animation.

---

## 3. Count-up (number animation)

**When to use:** Key metrics, KPIs, stat cards, and any number that is the main focus when the screen or section appears.

**What it does:** The number does **not** appear at its final value. It animates from a start value (often 0) to the target over 1.5–2 seconds, giving weight to the metric and signaling "this is important."

**Why it matters:** Static big numbers are easy to skip. A count-up draws the eye and makes the metric feel like a result or achievement.

| Parameter   | Recommended   | Notes                    |
|-------------|---------------|--------------------------|
| Duration    | 1.5–2 s       | 2 s is a common default   |
| Start value | 0 or previous | 0 for "from scratch"      |
| Easing      | ease-out      | Slight deceleration at end|
| Trigger     | On load or in view | Use Intersection Observer for below-fold |

**Implementation notes:**
- **JS:** CountUp.js, or requestAnimationFrame loop interpolating value. Support prefix/suffix ($, %, K, M).
- **Reduced motion:** Show final number immediately.

---

## 4. Progress ring / circle fill

**When to use:** Satisfaction score, completion percentage, or any single circular progress indicator.

**What it does:** The ring is drawn from 0% to the target percentage over 500–800 ms (stroke-dashoffset or equivalent), so the user sees the ring "fill" rather than appear full.

**Why it matters:** A static full ring has no moment. A short fill animation creates a clear "this is the score" moment.

| Parameter  | Recommended | Notes                          |
|------------|-------------|---------------------------------|
| Duration   | 500–800 ms  | Slightly longer than button feedback |
| Easing    | ease-out    | Deceleration at end             |
| Direction | Clockwise from top | Rotate SVG -90deg so 0 is at 12 o'clock |

**Implementation notes:**
- **SVG:** `stroke-dasharray: circumference`, `stroke-dashoffset: circumference → circumference - (percent/100 * circumference)`. Use `pathLength="100"` to simplify (offset = 100 - percent).
- **CSS:** `transition: stroke-dashoffset 0.6s ease-out`. Rotate the SVG with `transform: rotate(-90deg)`.
- **Reduced motion:** Set ring to final state with no transition.

---

## 5. Layered reveal (hierarchy)

**When to use:** Dense dashboards, multi-panel layouts, or any screen where primary and secondary content should be understood in order.

**What it does:** Primary content (main metric, main chart, hero) appears or animates first. Secondary content (supporting cards, labels, legends) follows after a short delay (100–200 ms). Optionally, tertiary elements appear last.

**Why it matters:** Animating everything equally flattens hierarchy and can feel noisy. Revealing in layers guides attention and makes the layout easier to parse.

| Layer     | Timing example        | Motion example              |
|-----------|------------------------|-----------------------------|
| Primary   | 0 ms                   | Fade in + slight translateY |
| Secondary | 100–200 ms after start | Fade in, shorter distance   |
| Tertiary  | 200–350 ms after start | Fade in only                |

**Implementation notes:**
- Use `animation-delay` or staggered JS delays. Keep total sequence under ~600 ms so the page doesn't feel slow.
- **Reduced motion:** Show all layers at once or with a single brief fade.

---

## 6. State-to-state continuity (data updates)

**When to use:** When the user changes a filter, time range, or view and the chart or data updates.

**What it does:** The transition from "old data" to "new data" is animated. Bars shrink/grow to new heights, lines morph, numbers count up or down. The layout does not "reset"—anchors stay stable so the user can follow what changed.

**Why it matters:** Hard swaps feel like a refresh and can be disorienting. Smooth transitions make the dashboard feel stable and understandable.

**Guidelines:**
- Duration: 300–500 ms for value changes; up to 600 ms for complex reflows.
- Keep axes and labels stable; animate only the data representation.
- **Reduced motion:** Crossfade or instant update.

---

## 7. Alert-first motion (real-time / urgency)

**When to use:** Alerts, notifications, or critical updates in monitoring or operational dashboards.

**What it does:** The new or changed element is briefly emphasized (e.g. subtle scale, color pulse, or entrance animation) so "what just changed" and "where" are obvious, then the UI calms down.

**Why it matters:** In busy interfaces, users need to spot changes quickly without scanning the whole screen. Motion can act as a hierarchy override for urgency.

**Guidelines:**
- Keep emphasis short (200–400 ms). Avoid continuous motion.
- **Reduced motion:** Use color and contrast only; avoid motion-based emphasis.

---

## Checklist for the agent

When suggesting or implementing motion beyond microinteractions:

- [ ] **Chart build-in:** Are there charts that should animate from baseline on load? (800–1200 ms, ease-out.)
- [ ] **Stagger:** Are there lists or grids of similar items that would benefit from a staggered reveal? (30–80 ms delay, max 10–15 items, total < 800 ms.)
- [ ] **Count-up:** Are there key numbers (stats, KPIs) that should count from 0 to value? (1.5–2 s.)
- [ ] **Progress ring:** Any circular progress that should fill on load? (500–800 ms, stroke-dashoffset.)
- [ ] **Layered reveal:** Should primary content appear before secondary? (delays 0, 100–200, 200–350 ms.)
- [ ] **State-to-state:** When data or filters change, should the transition be animated instead of a hard swap?
- [ ] **Reduced motion:** Are all of the above disabled or simplified when `prefers-reduced-motion: reduce`?

---

## References

- [Motion Design for Data Dashboards: 7 Practical Patterns](https://themotiondot.com/blog/motion-design-data-dashboards-7-patterns) (The Motion Dot)
- [Stagger Animation: Sequential Element Reveals](https://www.hashbuilds.com/patterns/what-is-stagger-animation) (HashBuilds)
- [Google Charts – Animation](https://developers.google.com/chart/interactive/docs/animation)
- [Chart.js – Animations](https://chartjs.org/docs/latest/configuration/animations.html)
- [Building a Progress Ring with CSS](https://css-tricks.com/building-progress-ring-quickly/) (CSS-Tricks)
- Count-up: CountUp.js, Quiet UI Number Ticker; typical duration 1.5–2 s
