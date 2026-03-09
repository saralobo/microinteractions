# Navigation

Microinteraction patterns for tab bars, page transitions, pull-to-refresh, scroll effects, and bottom navigation.

---

## Platform Notes

| Intent | Mobile | Desktop | Responsive |
|--------|--------|---------|------------|
| Tab switch | Tap + swipe between tabs | Click | Both |
| Tab hover | **Not applicable** | `:hover` color/bg change | `@media (hover: hover)` only |
| Page transition | Slide (gesture-driven) | Crossfade or slide | Both |
| Pull-to-refresh | Yes (native pattern) | **Not applicable** | Mobile only |
| Scroll effects | Use sparingly | Parallax, sticky header | Both (with care) |
| Bottom nav | Primary mobile navigation | **Not typical** | Mobile only |
| Sidebar nav | Not typical | Yes | Desktop only (or drawer on mobile) |

**On mobile**: the bottom navigation bar uses only tap (`:active`) feedback. No hover on nav items.

**On desktop**: tab bars and sidebar links get hover feedback.

**On responsive**: wrap tab/link hover in `@media (hover: hover) and (pointer: fine) { }`.

---

## 1. Tab / Segment Switch

**Platform**: All.

**Intent**: Switch between content sections.

**Trigger**: Click/tap on a tab.

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Active indicator | Slide from previous to new tab | 200–300 ms | spring(300, 0.85) or ease-in-out |
| Previous label | Color shift to inactive | 150 ms | ease-out |
| New label | Color shift to active | 150 ms | ease-out |
| Content (crossfade) | Old 1>0, new 0>1 | 150–200 ms | ease-in-out |
| Content (slide) | Old slides out, new slides in | 200–300 ms | deceleration |

**Rules**:
- Indicator physically travels between tabs.
- Content direction matches tab position.
- **Mobile**: swipe between content areas (gesture-driven).

**Accessibility**:
- `role="tablist"`, `role="tab"`, `role="tabpanel"`.
- `aria-selected`. Arrow keys navigate.
- Reduced motion: instant indicator, crossfade only.

---

## 2. Tab / Link Hover

**Platform**: Desktop only. Skip on mobile. Wrap in `@media (hover: hover)` for responsive.

**Trigger**: `mouseenter` / `:hover`.

| Property | Hover value | Duration | Easing |
|----------|------------|----------|--------|
| `color` | Active or intermediate color | 100–150 ms | ease-in-out |
| `background-color` (opt.) | Subtle highlight (5–10% opacity) | 100–150 ms | ease-in-out |

**Responsive pattern**:
```
@media (hover: hover) and (pointer: fine) {
  .nav-item:hover {
    color: var(--color-active);
    background-color: rgba(255, 255, 255, 0.05);
  }
}
```

---

## 3. Page Transition

**Platform**: All.

**Forward (deeper)**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| New page | Slide in from right + fade | 250–350 ms | deceleration |
| Current page | Slide out left + fade (or scale down) | 250–350 ms | acceleration |
| Shared elements | Morph from source to destination | 300–400 ms | spring |

**Back (shallower)**:

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Current page | Slide out right + fade | 200–300 ms | acceleration |
| Previous page | Slide in from left + fade | 200–300 ms | deceleration |

**Mobile-specific**: back gesture (swipe from left edge) drives transition interactively.

---

## 4. Pull-to-Refresh

**Platform**: Mobile only. Not applicable on desktop.

**Intent**: Pull down to refresh content.

| Phase | Visual | Behavior |
|-------|--------|----------|
| Pulling (< threshold) | Spinner follows finger, rotates proportionally | Direct manipulation |
| Past threshold | Spinner ready, haptic feedback | — |
| Release (past) | Content springs back, spinner loads | Spring + linear rotation |
| Loading | Spinner rotates at top | 600–800 ms/cycle |
| Complete | Spinner shrinks + fades, new content | 200–300 ms |
| Release (before) | Spring back, spinner gone | 200 ms |

**Accessibility**:
- Alternative refresh button/menu.
- `aria-live="polite"` on content.
- Reduced motion: ease-out instead of spring.

---

## 5. Scroll Effects

**Platform**: Both (with caution on mobile).

### Sticky Header

| Behavior | Specification |
|----------|---------------|
| Shrink on scroll | Height 64px to 48px, font shrinks | Scroll-linked |
| Shadow on scroll | box-shadow appears | 100 ms, ease-out |
| Background blur (opt.) | backdrop-filter: blur(8px) | instant |

### Parallax (Use Sparingly — Desktop preferred)

| Element | Scroll speed |
|---------|--------------|
| Background | 0.3–0.5x |
| Foreground | 1x (normal) |
| Decorative | 0.6–0.8x |

Purely decorative. Disable for `prefers-reduced-motion`.

### Scroll-to-Top Button

| Behavior | Specification |
|----------|---------------|
| Appear | After 200–500 px scroll, fade + slide, 200 ms |
| Disappear | At top, fade out 150 ms |
| Click | Smooth scroll to top, 300–600 ms |

---

## 6. Bottom Navigation (Mobile)

**Platform**: Mobile only (or responsive as mobile-only breakpoint).

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Active icon | Scale 1.0 to 1.15, color to primary | 150–200 ms | spring(400, 0.85) |
| Active label | Fade in + slide up | 150 ms | ease-out |
| Previous icon | Scale 1.15 to 1.0, color to inactive | 150–200 ms | ease-out |
| Tap feedback (`:active`) | Scale 0.97, darken bg | 80–120 ms | ease-out |
| Ripple (opt.) | Circular from tap | 300 ms | deceleration |
| Content | Crossfade | 150–250 ms | ease-in-out |

**Rules**:
- 3–5 destinations max.
- Active state immediately clear.
- Tapping active tab scrolls to top.
- **No hover feedback** — mobile only.

**Accessibility**: Same as tabs. Min tap target: 48x48 dp. Reduced motion: instant, keep color.

---

## State Machine (Tab/Bottom Nav)

```
tab-A (active) --> (tap tab-B) --> tab-B (active)
     |                                   |
     +-- content-A visible               +-- content-B visible

tab-A (active) --> (tap tab-A) --> scroll to top
```
