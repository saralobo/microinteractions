# FAB (Floating Action Button)

Microinteraction patterns for floating action buttons and speed dials.

---

## Platform Notes

| Intent | Mobile | Desktop | Responsive |
|--------|--------|---------|------------|
| Press (tap/click) | `:active` scale 0.92–0.95 | `:active` + hover prestate | Both |
| Hover (scale up) | **Not applicable** | `:hover` scale 1.05 | `@media (hover: hover)` only |
| Expand / Speed Dial | Tap | Click | Both |
| Morph | Same | Same | Same |
| Scroll behavior | Show/hide on scroll | Optional | Same |

**On mobile**: skip hover (Section 3 on desktop). The FAB responds only to tap (`:active`). Do not apply scale-up on hover.

**On responsive**: wrap hover in `@media (hover: hover) and (pointer: fine) { }`.

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

**Platform**: All.

**Trigger**: `mousedown` / `touchstart`.

| Property | Press value | Duration | Easing |
|----------|------------|----------|--------|
| `transform: scale` | 0.92–0.95 | 80–120 ms | ease-out |
| `box-shadow` | Reduce elevation | 80–120 ms | ease-out |
| Ripple (opt.) | Circular from touch point | 300–400 ms | deceleration |

**Mobile-specific**: add `-webkit-tap-highlight-color: transparent`.

---

## 3. Hover

**Platform**: Desktop only. Skip on mobile. Wrap in `@media (hover: hover)` for responsive.

**Trigger**: `mouseenter` / `:hover`.

| Property | Hover value | Duration | Easing |
|----------|------------|----------|--------|
| `transform: scale` | 1.05 | 120–150 ms | ease-out |
| `box-shadow` | Increase elevation | 120–150 ms | ease-out |
| `cursor` | `pointer` | instant | — |

**Responsive pattern**:
```
@media (hover: hover) and (pointer: fine) {
  .fab:hover {
    transform: scale(1.05);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.45);
  }
}
```

---

## 4. Expand / Speed Dial

**Platform**: All.

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

## 5. Morph

**Platform**: All.

**Intent**: FAB transforms into another element (toolbar, form, card).

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Shape | border-radius 50% to target; resize | 300–400 ms | deceleration |
| Position | Translate to target | 300–400 ms | deceleration |
| Icon | Fade out | 100–150 ms | ease-out |
| Target content | Fade in after morph | 150–200 ms | ease-out |

---

## 6. Scroll Behavior

**Platform**: All (especially common on mobile).

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
  +--> hover (desktop only) --> pressed --> action
  |
  +--> expanded (speed dial) --> action --> idle
  |         |
  |         +-- (Escape / backdrop) --> idle
  |
  +--> morphed --> (done) --> idle
  |
  +--> hidden (scroll down) --> visible (scroll up) --> idle
```
