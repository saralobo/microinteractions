# Microinteractions

A **code-neutral pattern library** for applying microinteractions to existing UIs.

Based on [Dan Saffer's *Microinteractions: Designing with Details*](https://www.oreilly.com/library/view/microinteractions-designing/9781449342685/) framework, Material Design 3 motion guidelines, Apple Human Interface Guidelines, and modern UX best practices observed in products like Stripe, Linear, Figma, Notion, and Airbnb.

## What This Is

- A **reference** for designers and developers who want to add feedback, state transitions, and motion to interfaces that are already designed.
- An **agent-ready repository** — structured so that an AI agent (Cursor, Claude, GPT, etc.) can read `AGENT.md` first and know exactly how to guide the user through applying microinteractions.
- **Code-neutral** — patterns are described in plain language with pseudocode. They work with any stack: HTML/CSS, React, Vue, SwiftUI, Flutter, Jetpack Compose, Figma, or anything else.

## What This Is Not

- Not a UI component library.
- Not a design system.
- Not a collection of ready-to-paste code snippets.

It's the *behavior layer* that sits on top of your existing components.

## Quick Start

1. **For AI agents**: Read [`AGENT.md`](./AGENT.md) first. It contains the conversation strategy and decision tree.
2. **For humans**: Browse [`patterns/`](./patterns/) and find your component type.
3. **For theory**: Read [`theory/`](./theory/) to understand the foundational model.

## Repository Structure

```
microinteractions/
├── AGENT.md                  # AI agent entry point + conversation strategy
├── README.md                 # This file
├── theory/
│   ├── saffer-model.md       # The 4-part model: Triggers → Rules → Feedback → Loops & Modes
│   ├── timing-and-easing.md  # Duration, easing curves, per-device guidelines
│   └── principles.md         # UX laws, accessibility, signature moments
└── patterns/
    ├── README.md             # Index + intent-to-pattern mapping
    ├── button.md             # Click, loading, success, error, disabled, hover
    ├── input.md              # Focus, validation, error, disabled, filled, password strength
    ├── toggle.md             # On/off, loading, disabled
    ├── card.md               # Hover, press, expand, drag, skeleton
    ├── toast.md              # Enter, auto-dismiss, action, stacking
    ├── modal.md              # Open, close, backdrop, focus trap, shake
    ├── dropdown.md           # Open, close, selection, search, multi-select
    ├── skeleton.md           # Pulse, wave, content transition
    ├── progress.md           # Determinate, indeterminate, steps, upload
    ├── fab.md                # Idle, press, expand, morph
    ├── tooltip.md            # Show, hide, delay, position
    └── navigation.md         # Tab switch, page transition, pull-to-refresh, scroll
```

## The Saffer Model (TL;DR)

Every microinteraction has four parts:

| Part | What it does | Example |
|------|--------------|---------|
| **Trigger** | Initiates the interaction | User clicks a button |
| **Rules** | Defines what happens | Button becomes disabled, shows spinner |
| **Feedback** | Communicates the rules to the user | Spinner animation, "Saving..." text |
| **Loops & Modes** | Meta-rules over time | After 3 uses, skip the confirmation |

## Design Philosophy

> *"The details are not the details. They make the design."* — Charles Eames

- **Immediate**: Feedback under 100 ms for direct manipulation.
- **Subtle**: A 2% scale change is felt; a 20% scale change is distracting.
- **Consistent**: Same component, same behavior, everywhere.
- **Accessible**: Always respect `prefers-reduced-motion`. Always provide non-motion alternatives.
- **Layered**: Add behavior on top of the existing design. Never redesign.

## References

- Saffer, D. (2013). *Microinteractions: Designing with Details*. O'Reilly Media.
- [Material Design 3 — Motion](https://m3.material.io/styles/motion)
- [Apple HIG — Animation](https://developer.apple.com/design/human-interface-guidelines/animation)
- [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/)
- Norman, D. (2013). *The Design of Everyday Things*. Basic Books.

## License

MIT
