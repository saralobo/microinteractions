# Dropdown / Select

Microinteraction patterns for dropdown menus, select boxes, comboboxes, and action menus.

---

## 1. Open

**Intent**: Reveal the list of options.

**Trigger**: Click on trigger element.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | Scale 0.95 to 1.0 + opacity 0 to 1 | 150–250 ms | deceleration |
| Alt. | Height 0 to auto (clip) | 200–300 ms | deceleration |
| Transform origin | From trigger location | — | — |
| Chevron | Rotate 0 to 180 deg | 200 ms | ease-in-out |

**Rules**:
- Appear near trigger (below, above, or side based on space).
- Flip if not enough space.
- Options immediately interactive.

---

## 2. Close

**Trigger**: Selection, Escape, outside click, Tab.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | Scale 1.0 to 0.95 + opacity 1 to 0 | 100–200 ms | acceleration |
| Chevron | Rotate 180 to 0 deg | 200 ms | ease-in-out |

Close faster than open. Selection close is near-instant (100 ms).

---

## 3. Option Hover / Focus

| Property | Value | Duration |
|----------|-------|----------|
| `background-color` | Primary at 5–10% opacity | 50–100 ms |
| Arrow keys move highlight | — | — |

---

## 4. Selection

| Element | Behavior | Duration |
|---------|----------|----------|
| Checkmark | Fade in | 100–150 ms |
| Trigger text | Update to selected | instant |
| Close | After 100 ms delay | — |

---

## 5. Search / Filter (Combobox)

- Filter options real-time as user types.
- "No results" placeholder if empty.
- Debounce 100–200 ms.
- Non-matching options fade out (100–150 ms).

---

## 6. Multi-Select

- Click toggles option (does not close).
- Checkbox animation: scale 0 to 1 (100–150 ms, spring).
- Tag in trigger: slide in (150–200 ms).
- Tag remove: shrink + fade (100–150 ms).

---

## Accessibility

- `role="listbox"` or `role="combobox"` + `role="listbox"`.
- `aria-expanded`, `aria-activedescendant`, `aria-selected`.
- Arrow keys navigate; Enter selects; Escape closes.
- Type-ahead: letter jumps to matching option.
- Reduced motion: instant show/hide.

---

## State Machine

```
closed --> open --> option-focused --> selected --> closed
            |
            +-- filtering --> results / no results
            +-- (Escape / outside) --> closed
```
