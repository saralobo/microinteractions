# Toast / Snackbar

Microinteraction patterns for toast notifications, snackbars, and inline alerts.

---

## 1. Enter

**Intent**: A non-blocking message appears to inform the user.

**Trigger**: Programmatic — after action completes or system event.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Position | Slide in from bottom (mobile) or top-right (desktop) | 250–350 ms | deceleration |
| Opacity | 0 to 1 | 200–300 ms | ease-out |
| `translateY` | 100% to 0 (bottom) or -100% to 0 (top) | 250–350 ms | deceleration |

**Rules**:
- Consistent location every time.
- Must not cover critical UI (e.g., submit button).
- Max width: 400–560 px desktop; full width minus margins mobile.

---

## 2. Auto-Dismiss

**Rules**:
- Default: 3–5 s informational, 5–8 s actionable.
- Timeout pauses on hover.
- Dismiss animation faster than enter.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Opacity | 1 to 0 | 150–200 ms | ease-in |
| `translateY` | 0 to 20 px or slide out | 150–200 ms | acceleration |

---

## 3. Manual Dismiss

| Action | Behavior | Duration | Easing |
|--------|----------|----------|--------|
| Swipe follow | translateX follows finger | real-time | direct |
| Release (past threshold) | continue + fade | 150 ms | acceleration |
| Release (before threshold) | snap back | 200 ms | spring |
| X button | same as auto-dismiss | 150 ms | ease-in |

---

## 4. Stacking

- Stack vertically, 8–12 px gap.
- Newer pushes older up/down.
- Max visible: 3–5.
- Staggered entry: 50–100 ms between.

---

## 5. Types

| Type | Color | Icon | Timeout |
|------|-------|------|---------|
| **Info** | Blue/neutral | info circle | 3–5 s |
| **Success** | Green | checkmark | 3 s |
| **Warning** | Yellow/amber | triangle | 5–8 s |
| **Error** | Red | X circle | No auto-dismiss or 8+ s |

---

## 6. Action Toast

Includes action button ("Undo", "View", "Retry").
- Action button clearly distinguishable.
- Timeout pauses on hover.
- After action, dismiss immediately.

---

## Accessibility

- `role="status"` for info/success; `role="alert"` for error/warning.
- `aria-live="polite"` or `aria-live="assertive"`.
- Keyboard-dismissible (Escape).
- Must not steal focus.
- Reduced motion: instant appear/disappear.

---

## State Machine

```
hidden --> entering --> visible --> exiting --> hidden
                          |
                          +-- (timeout) --> exiting
                          +-- (swipe) --> exiting
                          +-- (X click) --> exiting
                          +-- (action) --> exiting
```
