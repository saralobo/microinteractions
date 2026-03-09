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
2. **Perception first**: Read [`theory/perception-and-motion.md`](./theory/perception-and-motion.md) to ground motion in *how we perceive it* — attention (we look at what moves), easing (smooth vs linear vs abrupt), timing and spacing. Start here before applying any motion.
3. **For humans**: Browse [`patterns/`](./patterns/) and find your component type.
4. **For theory**: Read [`theory/`](./theory/) to understand the foundational model.
5. **For visible motion** (chart build-in, stagger, count-up, progress ring): Read [`theory/motion-patterns.md`](./theory/motion-patterns.md).

## Repository Structure

```
microinteractions/
├── AGENT.md                    # AI agent entry point + conversation strategy
├── README.md                   # This file
├── theory/
│   ├── perception-and-motion.md # Why motion works: attention, easing, timing+spacing (read first)
│   ├── saffer-model.md         # The 4-part model: Triggers, Rules, Feedback, Loops & Modes
│   ├── timing-and-easing.md    # Duration, easing curves, per-device guidelines
│   ├── principles.md           # UX laws, accessibility, signature moments
│   ├── platform-rules.md       # Mobile vs Desktop vs Responsive (hover, touch, cursor)
│   └── motion-patterns.md      # Chart build-in, stagger reveal, count-up, progress ring, layered reveal
└── patterns/
    ...
```

## The Saffer Model (TL;DR)

Every microinteraction has four parts: **Trigger** (what starts it), **Rules** (what happens), **Feedback** (what the user sees/feels), **Loops & Modes** (over time).

## Design Philosophy

- **Perception-first**: Motion draws the eye — use it with intent. Ask: What should the user notice? Does this movement have service meaning? See [`theory/perception-and-motion.md`](./theory/perception-and-motion.md).
- **Immediate**: Feedback under 100 ms for direct manipulation.
- **Subtle**: A 2% scale change is felt; a 20% scale change is distracting.
- **Consistent**: Same component, same behavior, everywhere.
- **Accessible**: Always respect `prefers-reduced-motion`. Always provide non-motion alternatives.
- **Layered**: Add behavior on top of the existing design. Never redesign.

## Motion & animation (beyond microinteractions)

When the goal is **visible motion**, use [`theory/motion-patterns.md`](./theory/motion-patterns.md): chart build-in, staggered reveal, count-up, progress ring fill, layered reveal. Motion should be a **clarity layer**, not decoration. All patterns respect `prefers-reduced-motion`.

## References

- Saffer, D. (2013). *Microinteractions: Designing with Details*. O'Reilly Media.
- [Material Design 3 — Motion](https://m3.material.io/styles/motion)
- [Apple HIG — Animation](https://developer.apple.com/design/human-interface-guidelines/animation)
- [Motion Design for Data Dashboards: 7 Practical Patterns](https://themotiondot.com/blog/motion-design-data-dashboards-7-patterns) (The Motion Dot)
- [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/)
- Norman, D. (2013). *The Design of Everyday Things*. Basic Books.

## License

MIT
