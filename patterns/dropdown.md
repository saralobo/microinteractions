# Dropdown / Select

Microinteraction patterns for dropdown menus, select boxes, comboboxes, and action menus.

---

## Platform Notes

| Intent | Mobile | Desktop | Responsive |
|--------|--------|---------|------------|
| Open trigger | Tap | Click | Both |
| Option hover/highlight | **Not applicable** (scroll + tap) | `:hover` highlight | `@media (hover: hover)` only |
| Selection | Tap | Click | Both |
| Keyboard navigation | Not applicable (native) | Arrow keys, Enter, Escape | Desktop only |
| Appearance | Often slides up as bottom sheet | Appears below/above trigger | Platform-specific |

**On mobile**: dropdowns often become bottom sheets or full-screen selectors. Option hover does not apply — the user scrolls and taps.

**On desktop**: options highlight on hover and support keyboard navigation.

**On responsive**: consider a bottom-sheet on small screens, standard dropdown on desktop.

---

## 1. Open

**Platform**: All.

**Intent**: Reveal the list of options.

**Trigger**: Click on trigger element.

**Desktop**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | Scale 0.95 to 1.0 + opacity 0 to 1 | 150–250 ms | deceleration |
| Transform origin | From trigger location | — | — |
| Chevron | Rotate 0 to 180 deg | 200 ms | ease-in-out |

**Mobile (bottom sheet variant)**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | translateY 100% to 0 (slide up) | 250–350 ms | deceleration |
| Backdrop | Opacity 0 to 0.4 | 200 ms | ease-out |
| Chevron | Rotate 0 to 180 deg | 200 ms | ease-in-out |

**Rules**:
- Appear near trigger (below, above, or side based on space).
- Flip if not enough space.
- Options immediately interactive.

---

## 2. Close

**Trigger**: Selection, Escape, outside click, Tab.

**Desktop**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | Scale 1.0 to 0.95 + opacity 1 to 0 | 100–200 ms | acceleration |
| Chevron | Rotate 180 to 0 deg | 200 ms | ease-in-out |

**Mobile (bottom sheet)**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Option list | translateY 0 to 100% | 200–300 ms | acceleration |
| Backdrop | Opacity to 0 | 150 ms | ease-in |

Close faster than open.

---

## 3. Option Hover / Focus

**Platform**: Desktop only (hover). Focus works on both via keyboard.

| Property | Value | Duration |
|----------|-------|----------|
| `background-color` | Primary at 5–10% opacity | 50–100 ms |
| Arrow keys move highlight | — | — |

**Responsive pattern**:
```
@media (hover: hover) and (pointer: fine) {
  .dropdown-option:hover {
    background-color: rgba(var(--primary), 0.08);
  }
}
```

---

## 4. Selection

**Platform**: All.

| Element | Behavior | Duration |
|---------|----------|----------|
| Checkmark | Fade in | 100–150 ms |
| Trigger text | Update to selected | instant |
| Close | After 100 ms delay | — |

---

## 5. Search / Filter (Combobox)

**Platform**: All.

- Filter options real-time as user types.
- "No results" placeholder if empty.
- Debounce 100–200 ms.
- Non-matching options fade out (100–150 ms).

---

## 6. Multi-Select

**Platform**: All.

- Click/tap toggles option (does not close).
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
