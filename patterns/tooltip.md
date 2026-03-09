# Tooltip

Microinteraction patterns for tooltips, info hints, and contextual help.

---

## 1. Show

**Intent**: Provide contextual information without cluttering the UI.

**Trigger**: Hover (desktop) or long press (mobile).

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Delay | 200–500 ms before showing | — | — |
| Opacity | 0 to 1 | 100–150 ms | ease-out |
| `transform: scale` | 0.95 to 1.0 | 100–150 ms | ease-out |
| `translateY` | 4–8 px toward target, to 0 | 100–150 ms | ease-out |
| Arrow | Points to target element | — | — |

**Rules**:
- Auto-position: above, below, left, right.
- "Warm start": moving between tooltip targets skips delay.
- Max width: 200–300 px. Longer content = use popover.

---

## 2. Hide

**Trigger**: Mouse leaves target / release.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Delay | 100–200 ms before hiding | — | — |
| Opacity | 1 to 0 | 80–120 ms | ease-in |
| Transform | Reverse of show | 80–120 ms | ease-in |

**Rules**:
- If cursor moves to tooltip itself, keep visible.
- Moving to different target: close + open new (warm start).

---

## 3. Positioning

- Preferred: above target.
- Fallback order: below > right > left.
- Never clipped by viewport.
- Arrow centered on target.
- Gap: 4–8 px.

---

## 4. Rich Tooltip

Interactive content (links, buttons, formatted text).
- Stay open while cursor inside.
- Trigger: hover or click (click is more accessible).
- Dismissible with Escape.
- Consider popover instead.

---

## Accessibility

- Trigger: `aria-describedby` pointing to tooltip `id`.
- Tooltip: `role="tooltip"`.
- Show on `focus` too (not just hover).
- Escape dismisses.
- No required actions in tooltip content.
- Reduced motion: instant show/hide.

---

## State Machine

```
hidden --> (hover + delay) --> visible --> (leave + delay) --> hidden
                                  |
                                  +-- (Escape) --> hidden
```
