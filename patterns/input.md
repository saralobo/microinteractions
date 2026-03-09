# Input

Microinteraction patterns for text inputs, textareas, search fields, and form fields.

---

## Platform Notes

| Intent | Mobile | Desktop | Responsive |
|--------|--------|---------|------------|
| Focus | Tap to focus (keyboard slides up) | Click or Tab | Both |
| Hover (border change) | **Not applicable** | `:hover` border color change | `@media (hover: hover)` only |
| Validation | Same | Same | Same |
| Disabled cursor | No cursor | `cursor: not-allowed` | `@media (pointer: fine)` for cursor |

**On mobile**: the virtual keyboard appearing is itself significant feedback. Focus ring and border change work the same.

**On desktop**: inputs also get a subtle `:hover` state (border color change) before focus.

**On responsive**: wrap hover border in `@media (hover: hover) and (pointer: fine) { }`.

---

## 1. Focus

**Platform**: All.

**Intent**: Clearly indicate which field the user is interacting with.

**Trigger**: `focus` / `:focus-visible` / click or tab.

**Feedback specification**:

| Property | Focus value | Duration | Easing |
|----------|------------|----------|--------|
| `border-color` | primary accent | 150 ms | ease-out |
| `box-shadow` | 0 0 0 2–3px rgba(primary, 0.25) | 150 ms | ease-out |
| `outline` | none (replaced by border/shadow) | instant | — |
| Floating label | translate up, scale 0.85 | 150–200 ms | ease-out |

**Mobile-specific**: virtual keyboard slides up — ensure the focused input is scrolled into view.

**Accessibility**:
- Never remove outline without equivalent visible indicator.
- Focus ring contrast: 3:1 minimum (WCAG 2.2).

---

## 2. Hover

**Platform**: Desktop only. Skip on mobile. Wrap in `@media (hover: hover)` for responsive.

**Trigger**: `mouseenter` / `:hover` (before focus).

| Property | Hover value | Duration | Easing |
|----------|------------|----------|--------|
| `border-color` | Slightly more prominent (e.g., 20–30% lighter/darker) | 100–150 ms | ease-in-out |

**Responsive pattern**:
```
@media (hover: hover) and (pointer: fine) {
  .input:hover:not(:focus) {
    border-color: rgba(255, 255, 255, 0.2);
  }
}
```

---

## 3. Blur

**Platform**: All.

**Intent**: Return to resting state; optionally trigger validation.

**Trigger**: `blur` / click outside.

**Feedback specification**:

| Property | Value | Duration | Easing |
|----------|-------|----------|--------|
| `border-color` | default | 150 ms | ease-in-out |
| `box-shadow` | none | 150 ms | ease-in-out |
| Floating label (has value) | stay elevated | — | — |
| Floating label (empty) | return to placeholder | 150–200 ms | ease-in-out |

---

## 4. Inline Validation (Real-time)

**Platform**: All.

**Intent**: Immediate feedback about input validity.

**Trigger**: On blur, or debounced on input (150–300 ms after typing stops).

**Valid state**:

| Property | Value | Duration | Easing |
|----------|-------|----------|--------|
| `border-color` | success (green) | 150 ms | ease-out |
| Checkmark icon | fade in at right | 150–200 ms | ease-out |

**Invalid state**:

| Property | Value | Duration | Easing |
|----------|-------|----------|--------|
| `border-color` | error (red) | 150 ms | ease-out |
| `background-color` | very light red (opt.) | 150 ms | ease-out |
| Error message | slide down + fade in | 150–200 ms | deceleration |
| Shake (first time) | translateX +/-3px | 300 ms | ease-out |

**Accessibility**:
- `aria-invalid="true"` when invalid.
- Error message: `id` referenced by `aria-describedby`.
- `aria-live="polite"` on error container.
- Reduced motion: no shake, instant color.

---

## 5. Error (on Submit)

**Platform**: All.

Same as invalid above, but triggered on form submit. Additional:
- Scroll to first error field.
- Focus first error field.
- Show all error messages simultaneously.

---

## 6. Disabled

**Platform**: All (with cursor differences).

| Property | Value | Transition |
|----------|-------|----------|
| `opacity` | 0.5–0.6 | 150 ms |
| `background-color` | light gray | 150 ms |
| `cursor` | `not-allowed` (desktop only) | instant |

---

## 7. Filled / Has Value

**Platform**: All.

| Property | Value | Duration |
|----------|-------|----------|
| Floating label | stay elevated and scaled | — |
| `border-color` (opt.) | slightly more prominent | 150 ms |

---

## 8. Password Strength Meter

**Platform**: All.

**Trigger**: Each keystroke in password field.

| Strength | Bar width | Color | Duration |
|----------|----------|-------|----------|
| Weak (< 3 criteria) | 33% | Red | 200 ms |
| Medium (3–4) | 66% | Yellow/Orange | 200 ms |
| Strong (5+) | 100% | Green | 200 ms |

Criteria: length >= 8, uppercase, lowercase, number, special char.

**Accessibility**: `role="progressbar"` + `aria-valuenow` + `aria-live="polite"` on label.

---

## 9. Character Count

**Platform**: All.

| Remaining | Color | Animation |
|-----------|-------|-----------|
| > 20% of limit | Default | None |
| 10–20% | Warning (yellow) | None |
| < 10% | Error (red) | Subtle pulse |
| 0 (at limit) | Error + bold | None |

---

## State Machine

```
          +-- hover (desktop only) --+
          |                          |
default --+--------------------------+-- focus --+-- typing --+-- valid --> (blur) --> filled
          |                                      |            +-- invalid --> error
          |                                      |            +-- validating (async) --> valid / invalid
          |                                      +-- (blur, empty) --> default
          +-- disabled
```
