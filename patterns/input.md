# Input

Microinteraction patterns for text inputs, textareas, search fields, and form fields.

---

## 1. Focus

**Intent**: Clearly indicate which field the user is interacting with.

**Trigger**: `focus` / `:focus-visible` / click or tab.

**Feedback specification**:

| Property | Focus value | Duration | Easing |
|----------|------------|----------|--------|
| `border-color` | primary accent | 150 ms | ease-out |
| `box-shadow` | 0 0 0 2–3px rgba(primary, 0.25) | 150 ms | ease-out |
| `outline` | none (replaced by border/shadow) | instant | — |
| Floating label | translate up, scale 0.85 | 150–200 ms | ease-out |

**Accessibility**:
- Never remove outline without equivalent visible indicator.
- Focus ring contrast: 3:1 minimum (WCAG 2.2).

---

## 2. Blur

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

## 3. Inline Validation (Real-time)

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

## 4. Error (on Submit)

Same as invalid above, but triggered on form submit. Additional:
- Scroll to first error field.
- Focus first error field.
- Show all error messages simultaneously.

---

## 5. Disabled

| Property | Value | Transition |
|----------|-------|----------|
| `opacity` | 0.5–0.6 | 150 ms |
| `background-color` | light gray | 150 ms |
| `cursor` | `not-allowed` | instant |

---

## 6. Filled / Has Value

| Property | Value | Duration |
|----------|-------|----------|
| Floating label | stay elevated and scaled | — |
| `border-color` (opt.) | slightly more prominent | 150 ms |

---

## 7. Password Strength Meter

**Trigger**: Each keystroke in password field.

| Strength | Bar width | Color | Duration |
|----------|----------|-------|----------|
| Weak (< 3 criteria) | 33% | Red | 200 ms |
| Medium (3–4) | 66% | Yellow/Orange | 200 ms |
| Strong (5+) | 100% | Green | 200 ms |

Criteria: length >= 8, uppercase, lowercase, number, special char.

**Accessibility**: `role="progressbar"` + `aria-valuenow` + `aria-live="polite"` on label.

---

## 8. Character Count

| Remaining | Color | Animation |
|-----------|-------|-----------|
| > 20% of limit | Default | None |
| 10–20% | Warning (yellow) | None |
| < 10% | Error (red) | Subtle pulse |
| 0 (at limit) | Error + bold | None |

---

## State Machine

```
default --+-- focus --+-- typing --+-- valid --> (blur) --> filled
          |           |            +-- invalid --> error
          |           |            +-- validating (async) --> valid / invalid
          |           +-- (blur, empty) --> default
          +-- disabled
```
