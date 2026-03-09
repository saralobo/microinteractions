# Patterns Index

Each file defines microinteraction patterns for a specific component type.

## Component Types

| Component | File | Intents |
|-----------|------|---------|
| Button | [button.md](./button.md) | Click feedback, hover, loading, success, error, disabled |
| Input | [input.md](./input.md) | Focus, blur, validation, error, disabled, filled, password strength, character count |
| Toggle | [toggle.md](./toggle.md) | On/off, loading, disabled |
| Card | [card.md](./card.md) | Hover, press, expand/collapse, drag, skeleton |
| Toast | [toast.md](./toast.md) | Enter, auto-dismiss, action, stacking, types |
| Modal | [modal.md](./modal.md) | Open, close, backdrop, focus trap, shake, bottom sheet |
| Dropdown | [dropdown.md](./dropdown.md) | Open, close, selection, search, multi-select |
| Skeleton | [skeleton.md](./skeleton.md) | Pulse, wave, shimmer, content transition |
| Progress | [progress.md](./progress.md) | Determinate, indeterminate, steps, upload, circular |
| FAB | [fab.md](./fab.md) | Idle, press, expand, morph, scroll behavior |
| Tooltip | [tooltip.md](./tooltip.md) | Show, hide, delay, position, rich content |
| Navigation | [navigation.md](./navigation.md) | Tab switch, page transition, pull-to-refresh, scroll, bottom nav |

## Intent Mapping (Quick Lookup)

When a user says... go to:

| User says | Component | Intent | File |
|-----------|-----------|--------|------|
| "click feedback" / "tap feedback" | Button | Click | button.md |
| "loading" / "spinner" / "submitting" | Button / Progress | Loading | button.md, progress.md |
| "success" / "done" / "confirmed" | Button / Toast | Success | button.md, toast.md |
| "error" / "failed" / "shake" | Button / Input / Modal | Error | button.md, input.md, modal.md |
| "hover" / "hover effect" | Button / Card | Hover | button.md, card.md |
| "focus" / "focus ring" | Input | Focus | input.md |
| "validation" / "inline validation" | Input | Validation | input.md |
| "toggle" / "switch" | Toggle | On/off | toggle.md |
| "expand" / "collapse" / "accordion" | Card | Expand | card.md |
| "notification" / "toast" / "snackbar" | Toast | Enter | toast.md |
| "modal" / "dialog" / "popup" | Modal | Open | modal.md |
| "dropdown" / "select" / "combobox" | Dropdown | Open | dropdown.md |
| "skeleton" / "placeholder" / "shimmer" | Skeleton | Pulse | skeleton.md |
| "progress bar" / "stepper" / "upload" | Progress | Determinate | progress.md |
| "FAB" / "floating button" | FAB | Press | fab.md |
| "tooltip" / "hint" | Tooltip | Show | tooltip.md |
| "tab" / "page transition" / "pull to refresh" | Navigation | Various | navigation.md |
| "disabled" / "inactive" | Button / Input / Toggle | Disabled | button.md, input.md, toggle.md |
| "general polish" / "add life" | All | Analysis mode | See AGENT.md Step 2B |
