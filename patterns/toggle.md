# Toggle / Switch

Microinteraction patterns for toggle switches, on/off controls, and binary state indicators.

---

## 1. On / Off

**Intent**: Switch between two states with clear, physical-feeling feedback.

**Trigger**: Click / tap on the toggle.

**Feedback specification**:

| Property | Off to On | On to Off | Duration | Easing |
|----------|----------|----------|----------|--------|
| Thumb position | translateX left to right | right to left | 180–250 ms | spring(stiffness: 300, damping: 0.7) |
| Track color | gray to active color | active to gray | 180–250 ms | ease-out |
| Thumb scale (press) | 1.0 to 1.1, back to 1.0 | same | 80–120 ms | ease-out |
| Thumb shadow | increase during move | same | 180–250 ms | ease-out |

**Rules**:
- Thumb should slightly overshoot (spring easing) for physical feel.
- Track color transitions smoothly, not snaps.
- If controlling a server setting, consider loading state.

**Accessibility**:
- `role="switch"` + `aria-checked="true/false"`.
- Keyboard: Space or Enter.
- Reduced motion: instant position, keep color.
- Label must be associated.

---

## 2. Loading

**Intent**: Toggle triggered an async action; result pending.

**Trigger**: After toggle click, before server confirmation.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Thumb | Move to target (optimistic) | 180–250 ms | spring |
| Track | Target color at 0.5 opacity | 180–250 ms | ease-out |
| Spinner | Small, inside/near thumb | 500–700 ms/cycle | linear |
| On success | Track opacity to 1.0 | 150 ms | ease-out |
| On failure | Thumb snaps back | 200 ms | ease-in-out |

Disable toggle during loading to prevent rapid toggling.

---

## 3. Disabled

| Property | Value |
|----------|-------|
| `opacity` | 0.4–0.5 |
| `cursor` | `not-allowed` |
| `pointer-events` | `none` |
| Colors | desaturated |

`aria-disabled="true"`. Consider explaining why.

---

## State Machine

```
off --> (click) --> on
 |                  |
 |    +-- loading --+
 |    |
 +----+

both states can be: active | loading | disabled
```
