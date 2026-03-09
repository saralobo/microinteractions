# Platform Rules: Mobile vs Desktop vs Responsive

Microinteractions must be **platform-aware**. An interaction that feels natural on desktop (hover) is meaningless on mobile. An interaction that feels right on mobile (long press, swipe) may confuse desktop users.

Always detect the target platform **before** choosing which patterns to apply.

---

## Quick Decision Table

| Interaction | Mobile | Desktop | Responsive |
|-------------|--------|---------|------------|
| **Hover state** | No | Yes | Desktop only (`@media (hover: hover)`) |
| **Active / tap / press** | Yes (primary feedback) | Yes | Yes |
| **Focus ring** | Yes (accessibility) | Yes (keyboard users) | Yes |
| **Cursor changes** | No (no cursor) | Yes (`pointer`, `not-allowed`, `grab`) | Desktop only |
| **Tooltip on hover** | No | Yes | Desktop only |
| **Tooltip on long press** | Yes | No | Mobile only |
| **Long press** | Yes (context menu, preview) | Rare | Mobile only |
| **Swipe gesture** | Yes (dismiss, navigate, reorder) | Rare | Mobile only |
| **Pull-to-refresh** | Yes | No | Mobile only |
| **Right-click context menu** | No | Yes | Desktop only |
| **Keyboard shortcuts** | No | Yes | Desktop only |
| **Haptic feedback** | Yes (native apps) | No | Mobile only |
| **Drag and drop** | Long press + drag | Click + drag | Both (different triggers) |
| **Scroll effects (parallax)** | Use sparingly | Yes | Desktop only or both with care |

---

## Mobile Rules

### Triggers that exist on mobile

- **Tap** (`touchstart` / `touchend` / `:active`)
- **Long press** (~300–500 ms hold)
- **Swipe** (directional gesture)
- **Pull down** (pull-to-refresh)
- **Pinch / spread** (zoom)
- **Shake** (undo, refresh)
- **System events** (notifications, connectivity, etc.)

### Triggers that do NOT exist on mobile

- **Hover** — there is no cursor. `:hover` fires on tap (and sticks), creating broken UX.
- **Right-click** — replaced by long press.
- **Cursor change** — no cursor to change.
- **Tooltip on hover** — no hover to trigger it.

### What to apply on mobile

| Component | Mobile-appropriate feedback | NOT appropriate |
|-----------|---------------------------|------------------|
| **Button** | Tap feedback (`:active` scale 0.97, darken bg), loading, success, error, disabled | Hover state |
| **Card** | Tap feedback (`:active` scale 0.99), expand/collapse | Hover lift, hover shadow |
| **Input** | Focus ring, validation, error shake, filled state | — |
| **Toggle** | On/off with spring, loading, disabled | — |
| **FAB** | Tap feedback (`:active` scale 0.94), expand speed dial | Hover scale-up |
| **Toast** | Slide in, swipe to dismiss, auto-dismiss | — |
| **Modal** | Slide up (bottom sheet), drag to dismiss | Scale-in from center |
| **Dropdown** | Slide up or expand, selection feedback | Hover highlight on options |
| **Tooltip** | Long press to show, release to hide (or info icon tap) | Hover to show |
| **Navigation** | Tap feedback, active indicator, swipe between tabs, pull-to-refresh | Hover color change |
| **Skeleton** | Pulse or shimmer (same on all platforms) | — |
| **Progress** | Same on all platforms | — |

### Mobile-specific timings

| Interaction | Duration | Notes |
|-------------|----------|-------|
| Tap feedback | 80–120 ms | Must feel instant. Use `:active` pseudo-class. |
| Long press threshold | 300–500 ms | Before triggering context action |
| Swipe threshold | 30–50% of element width/height | Before committing dismiss |
| Haptic | Varies by OS | Use `navigator.vibrate()` or native APIs |

### CSS for mobile-only tap feedback

```
.btn {
  -webkit-tap-highlight-color: transparent; /* remove default blue flash */
  transition: transform 100ms ease-out, background-color 100ms ease-out;
}
.btn:active {
  transform: scale(0.97);
  background-color: /* darken 10-15% */;
}
```

---

## Desktop Rules

### Triggers that exist on desktop

- **Click** (`mousedown` / `mouseup` / `:active`)
- **Hover** (`mouseenter` / `mouseleave` / `:hover`)
- **Focus** (Tab key / `:focus-visible`)
- **Right-click** (context menu)
- **Keyboard shortcuts** (Ctrl+S, etc.)
- **Drag and drop** (`mousedown` + `mousemove`)
- **Scroll** (wheel, trackpad)
- **System events** (notifications, etc.)

### Triggers that rarely exist on desktop

- **Long press** — uncommon, awkward with a mouse.
- **Swipe** — only on trackpads (not reliable).
- **Pull-to-refresh** — not a desktop pattern.
- **Haptic** — no haptic engine.

### What to apply on desktop

| Component | Desktop-appropriate feedback | Extra vs mobile |
|-----------|-----------------------------|-----------------|
| **Button** | Hover (bg change, shadow), click feedback (scale 0.97), loading, success, error, disabled, cursor `pointer` | Hover state, cursor |
| **Card** | Hover (lift, shadow), click feedback, expand/collapse, drag & drop | Hover lift |
| **Input** | Focus ring, hover border change, validation | Hover border |
| **Toggle** | Same + hover brightness change | Hover |
| **FAB** | Hover scale-up (1.05), click feedback (scale 0.94) | Hover |
| **Toast** | Slide in, hover pauses auto-dismiss, X button to close | Hover pause |
| **Modal** | Scale-in from center, backdrop blur, shake on invalid | — |
| **Dropdown** | Hover highlight on options, click to select, keyboard navigation | Hover highlight |
| **Tooltip** | Hover to show (200–500 ms delay), focus to show | Hover trigger |
| **Navigation** | Hover color change, click feedback, keyboard shortcuts | Hover, shortcuts |

---

## Responsive Rules

For UIs that serve **both mobile and desktop**:

### Strategy: Mobile-first, desktop-enhance

1. **Base styles** = mobile (`:active` feedback, no hover, no cursor changes).
2. **Desktop enhancements** inside media queries:

```
/* Hover is only valid on devices with a fine pointer (mouse/trackpad) */
@media (hover: hover) and (pointer: fine) {
  .btn:hover {
    background-color: /* lighten/darken 5-10% */;
  }
  .card:hover {
    transform: translateY(-2px);
    box-shadow: /* elevated */;
  }
  .tooltip-trigger:hover .tooltip {
    opacity: 1;
  }
}
```

### Why `@media (hover: hover)` and not just screen width

- A tablet in landscape can be > 768 px but still has **no hover** (touch only).
- A Surface or iPad with a mouse/trackpad **does** have hover.
- `(hover: hover) and (pointer: fine)` is the most reliable way to detect a device that supports hover.

### Never do this

- Never rely on hover for critical information (it's invisible on touch).
- Never show a tooltip only on hover without an alternative (info icon, long press).
- Never skip `:active` feedback on desktop — clicks also need feedback.
- Never apply `:hover` styles unconditionally on a mobile screen — they stick on tap and feel broken.

---

## Platform Detection Checklist (for the agent)

Before applying any microinteraction, check:

- [ ] Is this a **mobile** screen? (viewport ≤ 430 px, native app, bottom nav, touch patterns)
- [ ] Is this a **desktop** screen? (viewport > 768 px, cursor-based, menu bar, hover patterns)
- [ ] Is this **responsive**? (media queries, breakpoints, both touch and cursor expected)
- [ ] Did I **ask the user** if unclear?
- [ ] Am I applying **only platform-appropriate interactions**?
- [ ] Am I wrapping desktop-only interactions in `@media (hover: hover) and (pointer: fine)`?

---

*Reference: Apple HIG (touch targets), Material Design 3 (device categories), W3C pointer media queries.*
