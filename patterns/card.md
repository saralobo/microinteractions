# Card

Microinteraction patterns for cards (content cards, product cards, list items, tiles).

---

## 1. Hover (Desktop)

**Intent**: Signal that the card is interactive.

**Trigger**: `mouseenter` / `:hover`.

| Property | Hover value | Duration | Easing |
|----------|------------|----------|--------|
| `box-shadow` | Increase elevation (e.g., 0 4px 12px rgba(0,0,0,0.1)) | 150–200 ms | ease-out |
| `transform: translateY` | -2 to -4 px | 150–200 ms | ease-out |
| `transform: scale` (alt.) | 1.01–1.02 | 150–200 ms | ease-out |
| `cursor` | `pointer` | instant | — |

**Rules**:
- Choose either lift (translateY) or scale, not both.
- If the card has a CTA button, card hover should be subtler than button hover.
- Non-interactive cards: no hover.

**Accessibility**: Reduced motion: remove translateY/scale, keep shadow.

---

## 2. Press / Active

**Intent**: Confirm the click/tap.

**Trigger**: `mousedown` / `touchstart`.

| Property | Press value | Duration | Easing |
|----------|------------|----------|--------|
| `transform: scale` | 0.98–0.99 | 80–120 ms | ease-out |
| `box-shadow` | Reduce elevation | 80–120 ms | ease-out |

---

## 3. Expand / Collapse (Accordion)

**Intent**: Reveal or hide additional content.

**Trigger**: Click on card or expand trigger.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Content area | Height: 0 to auto | 200–350 ms | deceleration |
| Content opacity | 0 to 1 (staggered 50 ms after height) | 150–200 ms | ease-out |
| Chevron icon | Rotate 0 to 180 deg | 200–300 ms | ease-in-out |
| Sibling cards | Push down smoothly | 200–350 ms | same |

**Accessibility**:
- `aria-expanded="true/false"`.
- Content: `aria-hidden` inverse of expanded.
- Reduced motion: instant expand/collapse.

---

## 4. Drag / Reorder

**Intent**: Dragging to reorder or move.

**Trigger**: Long press / drag handle.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Dragged card | Scale 1.03–1.05, shadow increase, slight rotation 1–2 deg | 150–200 ms | ease-out |
| Drop zone | Highlight (dashed border or bg change) | 150 ms | ease-out |
| Other cards | Shift to make space | 200–250 ms | ease-in-out |
| On drop | Scale to 1.0, shadow default, subtle bounce | 200–300 ms | spring |

**Accessibility**:
- Keyboard: select with Space, move with arrows.
- Announce position: "Item 3 of 5, moved to position 2."

---

## 5. Skeleton / Loading

See [skeleton.md](./skeleton.md). Cards are the most common skeleton container.

Summary: gray rectangles matching content layout, pulse or shimmer, crossfade to real content (200–400 ms).

---

## State Machine

```
default --+-- hover --> press --> action (navigate, expand, etc.)
          +-- skeleton (loading) --> default
          +-- dragging --> dropped --> default
          +-- expanded <--> collapsed
```
