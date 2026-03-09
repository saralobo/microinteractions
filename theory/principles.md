# Principles

Core principles that govern microinteraction design. Drawn from UX research, cognitive psychology, design system guidelines, and real-world product patterns.

---

## 1. Feedback Is Non-Negotiable

Every user action that changes state must produce perceptible feedback. If the user clicks and nothing visible happens, the UI is broken.

> *"The most basic heuristic: make the system status visible."* — Jakob Nielsen, Heuristic #1

---

## 2. Subtlety Over Spectacle

The best microinteractions go unnoticed consciously but are felt. A button that scales to 0.97 on press feels right; one that scales to 0.7 feels like a bug.

Quantitative guideline:
- **Scale**: 2–5% (0.95–0.98)
- **Opacity**: 5–15% (0.85–0.95)
- **Translation**: 2–8 px
- **Rotation**: 1–5 degrees
- **Shadow elevation**: 1–4 px

---

## 3. Consistency Creates Trust

Same component type = same microinteraction = everywhere in the product. If the primary button has a scale-down press effect on one page, it must have it on every page.

---

## 4. Accessibility Is Required, Not Optional

### prefers-reduced-motion

Always wrap animations in a reduced-motion check:

```
IF user prefers reduced motion:
  - Replace animations with instant state changes (opacity fade <= 150 ms is acceptable)
  - Remove parallax, bounces, shakes, continuous loops
  - Keep color and text feedback
```

### Focus Management

- Every interactive element must have a visible focus indicator.
- Modal dialogs must trap focus.
- After an action (e.g., delete), focus must move to a logical next element.

### ARIA

- Loading: `aria-busy="true"`
- Error: `aria-invalid="true"` + `aria-describedby`
- Live updates: `aria-live="polite"` for success/error messages
- Disabled: native `disabled` or `aria-disabled="true"`

### Color

- Never use color alone to communicate state. Pair with icon, text, or shape.
- Contrast: 4.5:1 for text, 3:1 for UI components (WCAG AA).

---

## 5. The Signature Moment

Dan Saffer's concept: a microinteraction so well crafted it becomes a brand identifier.

Examples: Facebook's Like animation, Slack's message sent sound, iPhone's haptic home button, Stripe's payment form flow, Linear's keyboard-first interactions.

Signature moments emerge from caring about the details. They can't be forced.

---

## 6. UX Laws Applied to Microinteractions

### Fitts's Law
*Time to reach a target depends on distance and size.*
- Minimum interactive target: 44x44 px (Apple) / 48x48 dp (Material).
- Feedback areas should extend beyond the visual element.

### Hick's Law
*Decision time increases with choices.*
- Microinteractions should offer minimal choices (ideally zero — smart defaults).

### Miller's Law
*Working memory holds ~7 items.*
- Limit visible options in dropdowns and step indicators.

### Doherty Threshold
*Productivity increases when response time < 400 ms.*
- All feedback should begin within 100 ms and complete within 400 ms.

### Jakob's Law
*Users expect your product to work like others they know.*
- Use standard patterns. Don't reinvent the checkbox or toggle.

### Peak-End Rule
*Users judge by the peak and the end.*
- Success moments (order confirmed, task completed) are high-impact. Make them memorable.
- Smooth error recovery leaves a positive impression.

---

## 7. Don't Start from Zero

Dan Saffer's principle: never present a blank slate.
- Smart defaults, previous data, contextual information.
- Skeleton screens (not blank screens) while loading.
- Error states with recovery actions (not just "something went wrong").

---

## 8. Layer, Don't Replace

Microinteractions are an enhancement layer:
- Don't change the layout.
- Don't change the design language.
- Prefer animating existing properties (opacity, transform, color).
- The UI without microinteractions must still be fully functional.

---

## 9. Orchestration

When multiple microinteractions happen simultaneously:
- **Stagger entrances**: 30–50 ms between elements.
- **Don't compete**: One attention-grabbing animation at a time.
- **Hierarchy of motion**: Primary action prominent; secondary subtle.
- **Shared timing**: Related elements use the same duration and easing.

---

## 10. Test and Observe

- A/B test with and without. Measure task completion time, error rate, satisfaction.
- Observe users. Do they notice the feedback? Understand the state?
- Test edge cases: slow connections, old devices, 100th use.
- Watch for fatigue: delightful on first use, annoying on 1000th.

---

*References: Saffer (2013), Nielsen Norman Group, Laws of UX, WCAG 2.2, Material Design 3, Apple HIG.*
