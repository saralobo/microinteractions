# Skeleton Screen

Microinteraction patterns for skeleton loading states, shimmer effects, and content transitions.

---

## 1. Pulse

**Intent**: Gentle pulsing animation on placeholder blocks indicates content is loading.

**Trigger**: Component mounts with no data.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| `opacity` | 0.4 to 0.7 to 0.4 (loop) | 1.5–2 s/cycle | ease-in-out |
| `background-color` | Light gray (#e5e7eb) | — | — |
| `border-radius` | Match real content | — | — |

Use for short loading times (< 3 s).

---

## 2. Wave / Shimmer

**Intent**: Directional gradient sweep across placeholders.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Gradient | Linear moving left to right | 1.5–2 s/cycle | linear |
| Colors | transparent > rgba(255,255,255,0.4) > transparent | — | — |
| Direction | LTR layouts: left to right; RTL: right to left | — | — |

Pseudocode:
```
background: linear-gradient(90deg, transparent 0%, rgba(255,255,255,0.4) 50%, transparent 100%)
background-size: 200% 100%
animation: shimmer 1.5s linear infinite
```

Use for longer loading times (3+ s). All skeletons should shimmer in sync.

---

## 3. Content Transition

**Intent**: Smooth transition from skeleton to real content.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Skeleton opacity | 1 to 0 | 200–300 ms | ease-out |
| Content opacity | 0 to 1 | 200–300 ms | ease-out |
| Stagger (opt.) | 30–50 ms between blocks | — | — |

**Rules**:
- Crossfade: skeleton out, content in.
- Never show skeleton for < 300 ms (flash prevention).

---

## Layout Guidelines

| Real content | Skeleton shape |
|--------------|----------------|
| Text line | Rectangle, line-height, 60–90% width |
| Heading | Rectangle, taller, 40–60% width |
| Avatar | Circle |
| Image | Rectangle, same aspect ratio |
| Button | Rounded rectangle, button size |
| Icon | Small circle or square |

Match exact spacing of real layout. Don't use skeletons for action components (buttons, toggles) or if data loads < 300 ms.

---

## Accessibility

- `aria-busy="true"` on container.
- `aria-hidden="true"` on shapes (decorative).
- `aria-live="polite"` loading announcement.
- Reduced motion: pulse only (no shimmer).

---

## State Machine

```
loading (skeleton) --> transitioning --> loaded (real content)
                                          |
                                          +-- error (not skeleton)
```
