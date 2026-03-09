# Progress Indicators

Microinteraction patterns for progress bars, spinners, steppers, and upload indicators.

---

## 1. Determinate Progress Bar

**Intent**: Show how much of a task is complete (0–100%).

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Bar width | 0% to current% to 100% | 200–300 ms/update | ease-out |
| Color at 100% | Transition to success (green) | 300 ms | ease-out |
| Label (opt.) | "X%" or "X of Y" | instant | — |

**Rules**:
- Never go backwards (unless retrying).
- If stalled, keep bar position (don't fake).
- At 100%: brief success state before dismiss.

---

## 2. Indeterminate Progress Bar

**Intent**: Action in progress, completion unknown.

| Property | Behavior | Duration |
|----------|----------|----------|
| Animated stripe/gradient | Moves continuously | 1.5–2 s/cycle |
| Bar width (Material) | Grows and shrinks while sliding | 2 s/cycle |

---

## 3. Circular / Spinner

**Intent**: Loading indicator for inline or small spaces.

| Property | Behavior | Duration |
|----------|----------|----------|
| Rotation | 360 deg continuous | 600–800 ms/cycle |
| Stroke dash (Material) | Grows and shrinks | 1.5–2 s/cycle |
| Size | 16px inline, 24px button, 40px page | — |

**Rules**:
- Don't show for < 300 ms.
- > 10 s: pair with text ("Loading...", "Connecting...").

---

## 4. Steps / Stepper

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Completed step | Fill success + checkmark | 200–300 ms | ease-out |
| Current step | Pulsing or highlighted | 2 s pulse | ease-in-out |
| Upcoming step | Gray/outlined | — | — |
| Connector line | Fill left to right | 300 ms | ease-out |
| Current label | Bold/primary | 150 ms | ease-out |

Steps clickable to go back, not forward. Mobile: "Step X of Y".

---

## 5. Upload Progress

| Phase | Visual | Notes |
|-------|--------|-------|
| File selected | Thumbnail + filename animate in | 200 ms |
| Uploading | Determinate bar + percentage | — |
| Processing | Indeterminate or spinner | Unknown duration |
| Complete | Checkmark + success | 300 ms |
| Error | Error icon + retry button | Red |
| Cancel | Bar disappears | 150 ms |

---

## Accessibility

- `role="progressbar"` + `aria-valuenow/min/max`.
- `aria-valuetext` for human status.
- `aria-label` describing what's loading.
- Spinners: `role="status"` + `aria-label="Loading"`.
- Reduced motion: keep bar, replace spinner with pulsing opacity.

---

## State Machine

```
idle --> loading (0%) --> progress (X%) --> complete (100%)
                          |
                          +-- error --> retry --> loading
                          +-- cancel --> idle
```
