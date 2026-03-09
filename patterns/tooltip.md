# Tooltip

Microinteraction patterns for tooltips, info hints, and contextual help.

---

## Platform Notes

| Intent | Mobile | Desktop | Responsive |
|--------|--------|---------|------------|
| Show on hover | **Not applicable** | Hover trigger | `@media (hover: hover)` only |
| Show on long press | Long press (~400 ms) | Not applicable | Mobile only |
| Show on focus | `:focus-visible` | `:focus-visible` | Both |
| Info icon alternative | **Recommended** (tap to show) | Optional | Recommended for mobile |

**On mobile**: tooltips cannot trigger on hover. Use one of these alternatives:
1. **Long press**: show tooltip after ~400 ms hold. Release to dismiss.
2. **Info icon (i)**: place a small info icon next to the element. Tap to toggle tooltip.
3. **Inline help**: show the info directly in the UI (no tooltip needed).

**On desktop**: hover is the primary trigger (with delay).

**On responsive**: provide both — hover for desktop (inside `@media (hover: hover)`), info icon or long press for mobile.

---

## 1. Show

**Intent**: Provide contextual information without cluttering the UI.

**Trigger**:
- **Desktop**: `mouseenter` / `:hover` (with 200–500 ms delay).
- **Mobile**: Long press (~400 ms) or tap on info icon.
- **Both**: `:focus-visible` (keyboard).

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Delay | 200–500 ms before showing (desktop hover) | — | — |
| Opacity | 0 to 1 | 100–150 ms | ease-out |
| `transform: scale` | 0.95 to 1.0 | 100–150 ms | ease-out |
| `translateY` | 4–8 px toward target, to 0 | 100–150 ms | ease-out |
| Arrow | Points to target element | — | — |

**Rules**:
- Auto-position: above, below, left, right.
- "Warm start": moving between tooltip targets skips delay (desktop).
- Max width: 200–300 px. Longer content = use popover.

---

## 2. Hide

**Trigger**:
- **Desktop**: Mouse leaves target.
- **Mobile**: Release finger (long press), tap elsewhere, or tap info icon again.

| Property | Behavior | Duration | Easing |
|----------|----------|----------|--------|
| Delay | 100–200 ms before hiding (desktop) | — | — |
| Opacity | 1 to 0 | 80–120 ms | ease-in |
| Transform | Reverse of show | 80–120 ms | ease-in |

**Rules**:
- If cursor moves to tooltip itself, keep visible (desktop).
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
- Stay open while cursor inside (desktop) or until dismissed (mobile).
- Trigger: hover or click (click is more accessible and works on all platforms).
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
-- Desktop --
hidden --> (hover + delay) --> visible --> (leave + delay) --> hidden
                                  |
                                  +-- (Escape) --> hidden

-- Mobile --
hidden --> (long press 400ms) --> visible --> (release) --> hidden
hidden --> (tap info icon) --> visible --> (tap again / outside) --> hidden
```
