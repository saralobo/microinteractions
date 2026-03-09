# FAB (Floating Action Button)

Microinteraction patterns for floating action buttons and speed dials.

---

## 1. Idle

| Property | Value |
|----------|-------|
| `box-shadow` | Elevated (8–12 px) |
| `border-radius` | 50% (circle) or 28px (rounded rect, Material 3) |
| Position | Fixed, bottom-right, 16–24 px from edges |
| Z-index | Above content, below modals |

---

## 2. Press

**Trigger**: `mousedown` / `touchstart`.

| Property | Press value | Duration | Easing |
|----------|------------|----------|--------|
| `transform: scale` | 0.92–0.95 | 80–120 ms | ease-out |
| `box-shadow` | Reduce elevation | 80–120 ms | ease-out |
| Ripple (opt.) | Circular from touch point | 300–400 ms | deceleration |

---

## 3. Expand / Speed Dial

**Trigger**: Click/tap.

**Open**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| FAB icon | Rotate 45 deg (+ becomes x) | 200–300 ms | spring(300, 0.8) |
| Action buttons | Scale 0 to 1, staggered 30–50 ms | 200–300 ms | deceleration + spring |
| Action labels (opt.) | Fade in after buttons | 100 ms delay + 150 ms | ease-out |
| Backdrop (opt.) | Fade in 0.3 opacity | 200 ms | ease-out |

**Close**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Action buttons | Scale 1 to 0, reverse stagger | 150–200 ms | acceleration |
| FAB icon | Rotate back to 0 deg | 200–300 ms | spring |
| Backdrop | Fade out | 150 ms | ease-in |

---

## 4. Morph

**Intent**: FAB transforms into another element (toolbar, form, card).

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Shape | border-radius 50% to target; resize | 300–400 ms | deceleration |
| Position | Translate to target | 300–400 ms | deceleration |
| Icon | Fade out | 100–150 ms | ease-out |
| Target content | Fade in after morph | 150–200 ms | ease-out |

---

## 5. Scroll Behavior

- **Scroll down**: Hide (translateY 80px + fade, 200 ms, acceleration).
- **Scroll up**: Show (translateY 0 + fade in, 250 ms, deceleration).
- **At bottom**: Always show.

---

## Accessibility

- `aria-label` describing the action.
- Speed dial: `aria-expanded`, `aria-haspopup="true"`, `role="menu"` + `role="menuitem"`.
- Keyboard: Enter/Space to toggle, Escape to close.
- Reduced motion: instant show/hide, no rotation/morph.

---

## State Machine

```
idle --> pressed --> action
  |
  +--> expanded (speed dial) --> action --> idle
  |         |
  |         +-- (Escape / backdrop) --> idle
  |
  +--> morphed --> (done) --> idle
  |
  +--> hidden (scroll down) --> visible (scroll up) --> idle
```
