# Microinteractions Agent

> **This is the entry point.** When an AI agent or LLM is given this repository as context, it should read this file first.

## Purpose

This repository is a **pattern library for applying microinteractions to existing UIs**. It does not create screens from scratch. It enriches interfaces that are already designed by adding feedback, state transitions, and motion that make the product feel alive.

The patterns are **code-neutral** — described in plain language with pseudocode-style specifications. They can be implemented in any stack (HTML/CSS, React, Vue, SwiftUI, Flutter, Jetpack Compose, Figma annotations, etc.).

---

## How to Use This Repository

### Reading Order

1. **This file (`AGENT.md`)** — understand the conversation strategy and how to interact with the user.
2. **`theory/`** — internalize the Saffer model, timing/easing, principles, and **platform rules**.
3. **`patterns/`** — look up patterns by component type when applying microinteractions.

### For Humans

Browse the `patterns/` folder to find your component type, pick the interaction intent, and follow the specification.

---

## Conversation Strategy

Before applying any microinteraction, the agent **must** gather context. The following decision tree defines the conversation flow.

### Step 1 — Detect the Mode

Ask or detect:

> **"Do you want to apply a microinteraction to a specific component, or should I analyze the entire screen?"**

| Answer | Mode |
|--------|------|
| Specific component | **Targeted mode** — go to Step 2 |
| Entire screen | **Analysis mode** — go to Step 2 |

---

### Step 2 — Detect the Platform (REQUIRED)

Before choosing which patterns or intents to apply, **always determine the target platform**. This changes which interactions are valid.

Ask or detect:

> **"Is this a mobile screen, a desktop screen, or a responsive layout that serves both?"**

Detection hints (if the user doesn't say explicitly):
- **Mobile signals**: viewport ≤ 430 px, SwiftUI/Flutter/Jetpack Compose, iOS/Android project, mobile Figma frame, bottom navigation bar, touch-first patterns.
- **Desktop signals**: viewport > 768 px, cursor-based interactions, menu bars, hover tooltips.
- **Responsive signals**: CSS media queries, breakpoints, both hover and touch are expected.

| Platform | What changes |
|----------|--------------|
| **Mobile** | No `:hover`. Use `:active` / tap feedback only. Prefer haptic cues. Long press replaces right-click. No tooltip on hover (use long press or info icon). See `theory/platform-rules.md`. |
| **Desktop** | `:hover` is valid and expected. Cursor feedback (`pointer`, `not-allowed`). Tooltip on hover. Keyboard shortcuts. See `theory/platform-rules.md`. |
| **Responsive** | Apply mobile-first. Add desktop enhancements inside `@media (hover: hover)` or `@media (pointer: fine)`. Never rely on hover for critical feedback. See `theory/platform-rules.md`. |

**After detecting the platform**, proceed to Step 3A (targeted) or Step 3B (analysis).

---

### Step 3A — Targeted Mode

1. **Identify the component.** Ask: *"Which component?"* (or infer it from the prompt).
2. **Map to component type.** Determine the pattern file.
3. **Ask for intent.** If not clear, ask:
   > *"What kind of interaction do you want?"*
   **Filter intents by platform**: on mobile, do not offer "hover" as an option. On desktop, offer hover and keyboard shortcuts.
4. **Confirm context.** Before applying, confirm:
   - **Platform** (already detected in Step 2).
   - **Stack/technology** (CSS, React, Vue, SwiftUI, Flutter, etc.) — detect from code if possible.
   - **Design system** — existing tokens or color palette?
   - **Accessibility requirements** — any specific needs?
5. **Apply the pattern.** Follow the specification, **applying only the platform-appropriate interactions**.

---

### Step 3B — Analysis Mode

1. **Scan the UI.** Analyze the screen.
2. **List interactive elements.** Present a categorized list.
3. **Ask for intent.** Ask the goal.
4. **If "general polish"**, suggest a prioritized list of microinteractions **filtered by platform**:

   **Mobile**:
   - **High impact**: Tap feedback (`:active`), loading states, success/error feedback.
   - **Medium impact**: Focus rings (for accessibility), toast notifications, pull-to-refresh.
   - **Low impact**: Skeleton screens, scroll effects.
   - **Not applicable**: Hover effects, cursor changes, tooltip on hover.

   **Desktop**:
   - **High impact**: Click feedback, hover states, loading states, form validation.
   - **Medium impact**: Focus rings, hover tooltips, toast notifications.
   - **Low impact**: Skeleton screens, scroll animations.

   **Responsive**: mobile-first list, plus desktop enhancements inside `@media (hover: hover)`.

5. **Confirm and apply** — same as Step 3A, steps 4–5.

---

### When the Component Is Not in the Catalog

If the user's component type has **no dedicated pattern file** (e.g. slider, chip, badge, breadcrumb, pagination, avatar, tag, rating stars, list item), do the following:

1. **Acknowledge** that this component type is not yet in the pattern catalog.

2. **Suggest the closest match** from the catalog and offer to apply it as a baseline:
   - **Slider / range input** → input (focus, value change) or progress (drag, thumb feedback).
   - **Chip / tag / badge (clickable)** → button (click feedback, selected state) or card (press).
   - **Breadcrumb** → navigation (link/tab-like feedback).
   - **Pagination** → button (per control) + navigation (page change).
   - **Avatar (clickable)** → button or card (press).
   - **Rating stars / thumbs up** → button (per item) or toggle (selected state).
   - **Accordion (standalone)** → card (expand/collapse).
   - **List row (clickable)** → card (press).

3. **Offer the user two paths**:
   - **Option A — Use closest pattern**: Apply the closest match, filtered by platform.
   - **Option B — Define ad hoc**: Define from scratch using theory/.

4. **If applying without a pattern (Option B)**: Use theory files (saffer-model, timing-and-easing, principles, **platform-rules**).

5. **Do not create a new pattern file** unless the user explicitly asks.

---

### Step 4 — Apply

When applying a pattern:

1. **Read the pattern file** from `patterns/<component>.md`.
2. **Pick the intent section** that matches what the user asked for.
3. **Check `theory/platform-rules.md`** — apply only the interactions valid for the detected platform.
4. **Follow the specification**: timing, easing, visual changes, states, accessibility.
5. **Adapt to the stack**: translate pseudocode into the actual technology.
6. **Respect existing styles**: do not override the design — layer the microinteraction on top.
7. **Check accessibility**: `prefers-reduced-motion`, `aria` attributes, focus management.

---

## Key Principles (Quick Reference)

- **Feedback must be immediate**: under 100 ms for direct manipulation, under 300 ms for state changes.
- **Less is more**: a subtle scale of 0.97 is better than a dramatic 0.8.
- **Consistency**: same component type should have the same feedback across the screen.
- **Respect the user**: always support `prefers-reduced-motion` media query.
- **Don't redesign**: add behavior to the existing UI, don't change the layout or visual identity.
- **Platform-aware**: never apply hover to a mobile-only screen. Never skip tap feedback on desktop.

---

## Repository Map

```
microinteractions/
├── AGENT.md              ← You are here (start here)
├── README.md             ← Project overview for humans
├── theory/
│   ├── saffer-model.md   ← Triggers, Rules, Feedback, Loops & Modes
│   ├── timing-and-easing.md  ← Duration, easing curves, device guidelines
│   ├── principles.md     ← UX laws, accessibility, signature moments
│   └── platform-rules.md ← Mobile vs Desktop vs Responsive rules
└── patterns/
    ├── README.md          ← Pattern index + intent mapping
    ├── button.md
    ├── input.md
    ├── toggle.md
    ├── card.md
    ├── toast.md
    ├── modal.md
    ├── dropdown.md
    ├── skeleton.md
    ├── progress.md
    ├── fab.md
    ├── tooltip.md
    └── navigation.md
```
