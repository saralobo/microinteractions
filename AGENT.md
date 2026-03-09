# Microinteractions Agent

> **This is the entry point.** When an AI agent or LLM is given this repository as context, it should read this file first.

## Purpose

This repository is a **pattern library for applying microinteractions to existing UIs**. It does not create screens from scratch. It enriches interfaces that are already designed by adding feedback, state transitions, and motion that make the product feel alive.

The patterns are **code-neutral** — described in plain language with pseudocode-style specifications. They can be implemented in any stack (HTML/CSS, React, Vue, SwiftUI, Flutter, Jetpack Compose, Figma annotations, etc.).

---

## How to Use This Repository

### Reading Order

1. **This file (`AGENT.md`)** — understand the conversation strategy and how to interact with the user.
2. **`theory/`** — internalize the Saffer model, timing/easing guidelines, and UX principles.
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
| Specific component | **Targeted mode** — go to Step 2A |
| Entire screen | **Analysis mode** — go to Step 2B |

---

### Step 2A — Targeted Mode

1. **Identify the component.** Ask: *"Which component?"* (or infer it from the prompt — e.g., "the submit button").
2. **Map to component type.** Determine the pattern file: button, input, toggle, card, toast, modal, dropdown, skeleton, progress, fab, tooltip, or navigation.
3. **Ask for intent.** If the intent is not clear from the prompt, ask:
   > *"What kind of interaction do you want? For a button, options include: click feedback, loading, success, error, disabled, hover."*
   Show only the intents available for that component type (see the pattern file).
4. **Confirm context.** Before applying, confirm:
   - **Stack/technology** (CSS, React, Vue, SwiftUI, Flutter, etc.) — detect from code if possible.
   - **Design system** — is there an existing design token system or color palette?
   - **Accessibility requirements** — any specific needs (reduced motion, screen reader, etc.)?
5. **Apply the pattern.** Follow the specification from the pattern file, adapting to the stack and existing code.

---

### Step 2B — Analysis Mode

1. **Scan the UI.** Analyze the screen (DOM, component tree, Figma layers, or screenshot).
2. **List interactive elements.** Present a categorized list:
   ```
   Found interactive elements:
   - 2 buttons ("Submit", "Cancel")
   - 3 inputs (email, password, name)
   - 1 toggle (dark mode)
   - 1 dropdown (country selector)
   ```
3. **Ask for intent.** Ask:
   > *"What is the goal? Examples: add click feedback to buttons, add validation states to inputs, add loading state to the form submission, or apply a general polish pass."*
4. **If "general polish"**, suggest a prioritized list of microinteractions based on impact:
   - **High impact**: Button click feedback, form validation states, loading states.
   - **Medium impact**: Hover effects, focus rings, toast notifications.
   - **Low impact**: Skeleton screens, scroll animations, tooltip improvements.
5. **Confirm and apply** — same as Step 2A, steps 4-5, for each selected element.

---

### Step 3 — Apply

When applying a pattern:

1. **Read the pattern file** from `patterns/<component>.md`.
2. **Pick the intent section** that matches what the user asked for.
3. **Follow the specification**: timing, easing, visual changes, states, accessibility.
4. **Adapt to the stack**: translate pseudocode into the actual technology.
5. **Respect existing styles**: do not override the design — layer the microinteraction on top.
6. **Check accessibility**: ensure `prefers-reduced-motion` is handled, `aria` attributes are present, and focus is managed.

---

## Key Principles (Quick Reference)

- **Feedback must be immediate**: under 100 ms for direct manipulation, under 300 ms for state changes.
- **Less is more**: a subtle scale of 0.97 is better than a dramatic 0.8.
- **Consistency**: same component type should have the same feedback across the screen.
- **Respect the user**: always support `prefers-reduced-motion` media query.
- **Don't redesign**: add behavior to the existing UI, don't change the layout or visual identity.

---

## Repository Map

```
microinteractions/
├── AGENT.md              ← You are here (start here)
├── README.md             ← Project overview for humans
├── theory/
│   ├── saffer-model.md   ← Triggers, Rules, Feedback, Loops & Modes
│   ├── timing-and-easing.md  ← Duration, easing curves, device guidelines
│   └── principles.md     ← UX laws, accessibility, signature moments
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
