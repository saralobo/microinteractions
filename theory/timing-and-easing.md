# Timing and Easing

Animation timing and easing are critical to how microinteractions feel. Too fast and they're invisible; too slow and they feel sluggish. Wrong easing and they feel mechanical or unnatural.

This guide consolidates guidelines from Material Design 3, Apple HIG, and empirical UX research.

---

## Duration Guidelines

### By Interaction Type

| Interaction | Duration | Notes |
|-------------|----------|-------|
| Button press feedback | 80–120 ms | Must feel instant |
| Hover state change | 100–150 ms | Quick enough to feel responsive, slow enough to see |
| Toggle switch | 180–280 ms | Needs to feel like a physical switch |
| Dropdown open/close | 200–300 ms | Content appearing needs time to be perceived |
| Modal open | 200–300 ms | Entry should be noticeable but not slow |
| Modal close | 150–250 ms | Exit should be faster than entry |
| Toast enter | 200–300 ms | Draw attention without startling |
| Toast exit | 150–200 ms | Quick fade out |
| Page transition | 250–400 ms | Provide continuity without delay |
| Skeleton to content | 200–400 ms | Crossfade from placeholder to real content |
| Loading spinner | 400–800 ms/cycle | Moderate speed keeps it calm |
| Success checkmark | 300–500 ms | Needs time to be noticed |
| Error shake | 300–400 ms | Short, sharp |
| Pull-to-refresh | 300–500 ms | Snap-back after release |
| Tooltip show | 200–500 ms delay, 100–150 ms fade | Delay prevents accidental triggers |
| Tooltip hide | 100–150 ms | Fast exit |

### By Device (Material Design 3)

| Device | Multiplier | Standard | Notes |
|--------|-----------|----------|-------|
| Mobile | 1x | ~300 ms | Baseline |
| Tablet | 1.3x | ~390 ms | Larger surfaces need more time |
| Desktop | 0.5–0.7x | 150–200 ms | Users expect snappier responses |
| Wearable | 0.7x | ~210 ms | Small surface, quick glances |

### Hard Limits

- **Never exceed 400 ms** for simple interactions. Feels sluggish.
- **Never go below 80 ms.** The human eye can't perceive it.
- **Loading states appear after 300–500 ms.** If the action completes before this, skip the loading state entirely.

---

## Easing Curves

### Core Curves

| Curve | CSS | Use For |
|-------|-----|---------|
| **Standard (ease-in-out)** | `cubic-bezier(0.4, 0.0, 0.2, 1)` | Most transitions |
| **Deceleration (ease-out)** | `cubic-bezier(0.0, 0.0, 0.2, 1)` | Elements entering the screen |
| **Acceleration (ease-in)** | `cubic-bezier(0.4, 0.0, 1, 1)` | Elements leaving the screen |
| **Sharp** | `cubic-bezier(0.4, 0.0, 0.6, 1)` | Temporary elements |
| **Linear** | `linear` | Only for opacity fades or continuous progress bars |

### Spring Physics (Apple HIG / Modern UI)

Spring-based easing creates a more natural, physical feel:

- **Stiffness**: Higher = snappier (buttons: 300–400; modals: 200–300)
- **Damping**: Controls overshoot. Low (0.5–0.7) = bouncy; high (0.8–1.0) = smooth
- **Mass**: Affects inertia. 1.0 for most; 1.2–1.5 for large surfaces

### When to Use What

| Scenario | Curve | Why |
|----------|-------|-----|
| Button press | Spring (high stiffness, high damping) | Feels tactile |
| Button hover | Standard ease-in-out | Smooth, predictable |
| Modal appearing | Deceleration + slight spring | Enters fast, settles |
| Modal disappearing | Acceleration | Leaves quickly |
| Toast entering | Deceleration | Slides in, decelerates |
| Toast leaving | Acceleration | Slides out, accelerates |
| Toggle switch | Spring (medium stiffness, low damping) | Physical feel |
| Error shake | Custom (sharp, symmetric) | Urgency |
| Skeleton pulse | Linear | Continuous, ambient |

---

## The 100 ms Rule

Jakob Nielsen's response-time thresholds:

| Threshold | Perception | Implication |
|-----------|------------|-------------|
| < 100 ms | Instant | Direct manipulation feedback must be here |
| 100 ms – 1 s | Noticeable delay | Provide visual feedback |
| > 1 s | Flow broken | Show loading state + progress |

---

## Color as Feedback

Color changes are perceived faster than motion (~50 ms vs ~100 ms):

- **Hover**: Darken by 10–15%
- **Active/pressed**: Darken by 15–25%
- **Success**: Green spectrum
- **Error**: Red spectrum
- **Focus ring**: Primary accent at 25–40% opacity

Always pair color with another indicator (icon, text, shape) for color-blind users.

---

*References: Material Design 3 Motion, Apple HIG Animation, Nielsen Norman Group.*
