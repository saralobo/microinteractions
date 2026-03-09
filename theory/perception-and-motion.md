# Perception and motion: why it matters

This document grounds the microinteractions and motion repository in **how we perceive movement**. Before choosing *what* to animate or *which* easing to use, the analysis should start from what actually happens with our eyes and brain when something moves.

---

## 1. We are wired to look at what moves

Humans are programmed to direct attention to things that move. Motion is a powerful **attention cue**: it invites the gaze and signals "something changed" or "this is relevant." That is why:

- **Motion has a cost.** If something moves, it will draw attention. If the movement has no service meaning (e.g. decorative only, or random), it competes with what the user should be doing and can feel noisy or distracting.
- **Motion has a purpose.** In interfaces, motion and microinteractions should **direct attention with intent**: to confirm an action, to show what changed, to guide to the next step, or to give hierarchy (primary vs secondary). The movement should be in service of the task.

So the first question when designing or applying motion is not "what can we animate?" but **"what deserves attention here, and does this motion support that?"**

---

## 2. How we perceive motion: easing and "feel"

The *way* something moves strongly influences how we perceive it. The same distance and duration can feel very different depending on the **easing** (acceleration curve):

| Type | What it does | How it tends to feel | When it's often used |
|------|----------------|----------------------|------------------------|
| **Linear** | Constant speed from start to end | Mechanical, predictable; can feel stiff or "digital" | Rare in UI; sometimes for progress or very neutral transitions |
| **Ease-in** | Starts slow, ends fast | Object "accelerates in"; can feel like it's leaving or gaining momentum | Exits, things moving out of view |
| **Ease-out** | Starts fast, ends slow | Object "decelerates"; feels like it's arriving or settling | Entrances, things coming to rest (e.g. modals, cards) |
| **Ease-in-out** | Slow at start and end, faster in the middle | Smoother, more "natural" arc | General-purpose transitions when you want a balanced feel |
| **Custom / spring** | Physics-like or branded curve | Can feel bouncy, organic, or very controlled | When the product has a defined motion language |

- **Smooth, natural curves** (ease-out, ease-in-out, well-tuned springs) usually feel more comfortable and intentional; they match our expectation of how physical things slow down and stop.
- **Abrupt or linear motion** can feel harsh or "machine-like"; it can work for alerts or very short feedback but often undermines calm and clarity.
- **Consistency** matters: the same type of action (e.g. "something appearing") should use a consistent easing across the product so the user builds a subconscious model of "how this interface moves."

So the second question is: **"Does this easing match the intent (entrance vs exit vs feedback) and the product's motion language?"**

---

## 3. Timing, spacing, and speed

Beyond easing:

- **Duration** (timing): Too short and the user may not notice or may feel rushed; too long and the interface feels slow or theatrical. Guidelines in the repo (e.g. under 100 ms for press, 200–300 ms for state changes) exist so motion is noticeable but not blocking.
- **Distance / spacing**: The same duration over a larger distance feels faster; over a smaller distance, it can feel subtler. So "how far" and "how long" together define perceived speed.
- **Velocity** (speed at each moment) is what easing actually changes: we perceive not just "it moved" but "how it accelerated or decelerated."

Together, **timing + spacing + easing** define the perceived quality of the motion. Analysis should consider all three, not only duration.

---

## 4. Implications for the repository and the agent

- **Start from perception and intent.** Before suggesting or implementing a microinteraction or motion:
  1. What should the user notice or understand? (attention)
  2. Does this movement support that? (service meaning)
  3. What easing and timing match this intent and the rest of the product? (perception and consistency)

- **Document easing in theory.** The repo should state clearly when to prefer ease-out vs ease-in vs ease-in-out (and point to timing-and-easing.md and motion-patterns.md). Easing is not a cosmetic choice; it shapes how the motion is perceived.

- **When the user shares course material** (e.g. slides on "Animando marcas e produtos", perception of animation, when to use which curve), that content should be analyzed and merged into this document and into timing-and-easing and motion-patterns so that the repository's recommendations are grounded in learning and practice, not only in generic guidelines.

---

## 5. Short checklist (for the agent)

Before applying or suggesting motion:

- [ ] **Attention:** What element or change should the user notice? Is this motion drawing attention to the right thing?
- [ ] **Meaning:** Does the movement have a clear service meaning (feedback, hierarchy, continuity), or is it decorative?
- [ ] **Easing:** Does the curve match the intent (entrance to often ease-out; exit to often ease-in; general to ease-in-out) and the product's motion language?
- [ ] **Timing and spacing:** Is the duration appropriate for the distance and context? Is it consistent with other similar actions in the product?
- [ ] **Perception-first:** Would a user perceive this as intentional and helpful, or as noise?

---

*This document will be enriched with content from the user's course materials (e.g. "Animando marcas e produtos", perception of animation, when to use which curve) once those materials are shared and analyzed.*
