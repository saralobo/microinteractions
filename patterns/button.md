# Button

Microinteraction patterns for buttons (primary, secondary, icon buttons, CTAs, submit buttons).

---

## 1. Click / Tap Feedback

**Intent**: The user feels the button physically respond to their press.

**Trigger**: `mousedown` / `touchstart` / `:active`.

**Rules**:
- On press: scale down slightly, darken background.
- On release: return to default.
- Must happen within 50 ms of the press event.

**Feedback specification**:

| Property | Press value | Release value | Duration | Easing |
|----------|------------|---------------|----------|--------|
| `transform: scale` | 0.97 | 1.0 | 80–120 ms | spring(stiffness: 400, damping: 0.85) or ease-out |
| `background-color` | darken 10–15% | original | 80–120 ms | ease-out |
| `opacity` (optional) | 0.9 | 1.0 | 80–120 ms | ease-out |

**Accessibility**:
- Reduced motion: remove scale, keep color change (instant).
- Focus: visible focus ring (2 px solid, 2 px offset) on `:focus-visible`.

**Anti-patterns**:
- Scale below 0.9 — feels broken.
- Duration > 200 ms — feels laggy.
- No feedback at all — user doesn't know if click registered.

---

## 2. Hover

**Intent**: Signal interactivity before the user commits to clicking.

**Trigger**: `mouseenter` / `:hover` (desktop only).

**Feedback specification**:

| Property | Hover value | Duration | Easing |
|----------|------------|----------|--------|
| `background-color` | lighten/darken 5–10% | 100–150 ms | ease-in-out |
| `box-shadow` | increase elevation 1–2 px | 100–150 ms | ease-in-out |
| `transform: translateY` (opt.) | -1 px | 100–150 ms | ease-in-out |
| `cursor` | `pointer` | instant | — |

**Accessibility**:
- Never put critical info only in hover.
- Reduced motion: keep color change, remove translateY.

---

## 3. Loading

**Intent**: Button triggered an async action; user must wait.

**Trigger**: Programmatic — after click, when loading state is set.

**Rules**:
- Replace text with spinner or add spinner beside text.
- Disable button (`disabled` or `aria-busy="true"`).
- Width must not change (prevents layout shift).
- If action takes < 300 ms, skip loading state.

**Feedback specification**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Button text | Fade out or shift left | 150–200 ms | ease-out |
| Spinner | Fade in at center or left of text | 150–200 ms | ease-out |
| Button width | Fixed (`min-width`) | — | — |
| Spinner rotation | 360 deg/cycle | 500–700 ms/cycle | linear |
| Opacity | 0.7 during loading (opt.) | 150 ms | ease-out |

**Accessibility**:
- `aria-busy="true"` during loading.
- `aria-live="polite"` status region announces "Loading..." / "Done".
- Reduced motion: pulsing dots or text instead of spinner.

**Anti-patterns**:
- Changing button width (layout shift).
- Allowing double-click (duplicate actions).
- Showing loading for < 200 ms (glitchy).

---

## 4. Success

**Intent**: Confirm the action completed successfully.

**Trigger**: Programmatic — after successful response.

**Feedback specification**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Spinner to checkmark | Morph or crossfade | 200–300 ms | deceleration |
| Background color | Shift to success color | 200–300 ms | ease-out |
| Text | "Done" / "Saved" / "Sent" | 200–300 ms | ease-out |
| Checkmark draw (opt.) | SVG stroke-dashoffset | 300–500 ms | ease-out |
| Return to default | Revert after 1.5–3 s | 200–300 ms | ease-in-out |

**Accessibility**:
- `aria-live="polite"` announces success.
- Reduced motion: instant color + text change.

---

## 5. Error

**Intent**: Communicate that the action failed.

**Trigger**: Programmatic — after failed response or validation.

**Feedback specification**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Shake | translateX: 0 > -4px > 4px > -4px > 4px > 0 | 300–400 ms | ease-out |
| Background | Shift to error color (subtle) | 150–200 ms | ease-out |
| Text | "Failed" / "Try again" | 150–200 ms | ease-out |
| Error icon | Fade in | 150–200 ms | ease-out |
| Return to default | After 2–5 s or on next click | 200 ms | ease-in-out |

**Accessibility**:
- `aria-live="assertive"` for error messages.
- Reduced motion: no shake, instant color change.

---

## 6. Disabled

**Intent**: Show button is not currently interactive.

**Trigger**: Conditional — when preconditions not met.

**Feedback specification**:

| Property | Value | Transition | Easing |
|----------|-------|-----------|--------|
| `opacity` | 0.5–0.6 | 150 ms | ease-in-out |
| `background-color` | desaturated/gray | 150 ms | ease-in-out |
| `cursor` | `not-allowed` | instant | — |
| `pointer-events` | `none` | instant | — |

**Accessibility**:
- Native `disabled` for form buttons.
- `aria-disabled="true"` for custom buttons.
- Consider tooltip explaining why.

---

## State Machine

```
          +---- hover ----+
          |               |
default --+---- focus ----+-- pressed --+-- loading --+-- success --> default
          |               |             |             +-- error ----> default
          +-- disabled    |             |             |
                          +-------------+             +-- (timeout) -> default
```
