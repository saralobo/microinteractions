# Modal / Dialog

Microinteraction patterns for modals, dialogs, bottom sheets, and overlays.

---

## 1. Open

**Intent**: Focus user's attention on a task or decision.

**Trigger**: Button click, system event, or programmatic.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Backdrop | Opacity 0 to 0.4–0.6 | 200–300 ms | ease-out |
| Modal | Scale 0.95 to 1.0 + opacity 0 to 1 | 200–300 ms | deceleration or spring(250, 0.85) |
| Alt (mobile) | translateY 100% to 0 (slide up) | 250–350 ms | deceleration |
| Body scroll | `overflow: hidden` | instant | — |

**Rules**:
- Focus moves to first focusable element inside.
- Background inert (`aria-hidden` or `inert`).
- Escape closes. Backdrop click closes (unless required).

---

## 2. Close

**Trigger**: X button, Escape, backdrop click, or action button.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Modal | Scale 1.0 to 0.95 + opacity 1 to 0 | 150–250 ms | acceleration |
| Alt (mobile) | translateY 0 to 100% | 200–300 ms | acceleration |
| Backdrop | Opacity to 0 | 200–250 ms | ease-in |
| Body scroll | Restore | after animation | — |

Close is faster than open. Focus returns to triggering element.

---

## 3. Backdrop

| Property | Value |
|----------|-------|
| Color | rgba(0, 0, 0, 0.4–0.6) |
| Blur (opt.) | backdrop-filter: blur(4–8px) |
| Click | Closes modal (unless required) |

---

## 4. Focus Trap

- Tab cycles only through modal elements.
- Tab from last: wrap to first.
- Shift+Tab from first: wrap to last.
- Escape: close.

---

## 5. Shake on Invalid

**Intent**: User tried to submit/close but validation failed.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Modal | translateX: 0 > -6px > 6px > -6px > 6px > 0 | 350–450 ms | ease-out |
| Backdrop (opt.) | Brief opacity pulse | 200 ms | ease-in-out |

Pair with visual indicator on the invalid field.

---

## 6. Bottom Sheet (Mobile)

| Feature | Behavior |
|---------|----------|
| Drag handle | Visible bar at top |
| Drag to dismiss | Past 33% height = dismiss |
| Snap points | Partial (40–50%), full (90–95%) |
| Velocity | Fast swipe dismisses regardless of position |

---

## Accessibility

- `role="dialog"` + `aria-modal="true"`.
- `aria-labelledby` to title. `aria-describedby` to description.
- Focus trap active.
- Escape closes.
- Reduced motion: instant open/close (opacity only).

---

## State Machine

```
closed --> opening --> open --> closing --> closed
                       |
                       +-- shake (invalid) --> open
                       +-- nested modal --> (stack)
```
