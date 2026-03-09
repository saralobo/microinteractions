# Navigation

Microinteraction patterns for tab bars, page transitions, pull-to-refresh, scroll effects, and bottom navigation.

---

## 1. Tab / Segment Switch

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
- Mobile: swipe between content areas.

**Accessibility**:
- `role="tablist"`, `role="tab"`, `role="tabpanel"`.
- `aria-selected`. Arrow keys navigate.
- Reduced motion: instant indicator, crossfade only.

---

## 2. Page Transition

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

---

## 3. Pull-to-Refresh

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

## 4. Scroll Effects

### Sticky Header

| Behavior | Specification |
|----------|---------------|
| Shrink on scroll | Height 64px to 48px, font shrinks | Scroll-linked |
| Shadow on scroll | box-shadow appears | 100 ms, ease-out |
| Background blur (opt.) | backdrop-filter: blur(8px) | instant |

### Parallax (Use Sparingly)

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

## 5. Bottom Navigation (Mobile)

| Element | Behavior | Duration | Easing |
|---------|----------|----------|--------|
| Active icon | Scale 1.0 to 1.15, color to primary | 150–200 ms | spring(400, 0.85) |
| Active label | Fade in + slide up | 150 ms | ease-out |
| Previous icon | Scale 1.15 to 1.0, color to inactive | 150–200 ms | ease-out |
| Ripple (opt.) | Circular from tap | 300 ms | deceleration |
| Content | Crossfade | 150–250 ms | ease-in-out |

**Rules**:
- 3–5 destinations max.
- Active state immediately clear.
- Tapping active tab scrolls to top.

**Accessibility**: Same as tabs. Min tap target: 48x48 dp. Reduced motion: instant, keep color.

---

## State Machine (Tab/Bottom Nav)

```
tab-A (active) --> (tap tab-B) --> tab-B (active)
     |                                   |
     +-- content-A visible               +-- content-B visible

tab-A (active) --> (tap tab-A) --> scroll to top
```
