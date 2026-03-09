# The Saffer Model

Dan Saffer's *Microinteractions: Designing with Details* (O'Reilly, 2013) defines a four-part structure that every microinteraction follows. This is the foundational framework for every pattern in this repository.

---

## The Four Parts

```
Trigger → Rules → Feedback → Loops & Modes
```

### 1. Trigger

The moment the microinteraction begins. There are two types:

**Manual triggers** — initiated by the user:
- Click / tap
- Hover
- Swipe / gesture
- Voice command
- Keyboard shortcut
- Drag

**System triggers** — initiated by the system when conditions are met:
- Timer elapsed (e.g., alarm goes off)
- Data received (e.g., new message notification)
- Location change (e.g., geofence alert)
- Error detected (e.g., network failure)
- State change (e.g., battery low)

#### Trigger Design Principles

1. **Make the trigger recognizable.** Users should understand that something is interactive. Use affordances: buttons look pushable, toggles look switchable.
2. **Same trigger, same action.** The trigger should initiate the same behavior every time. Inconsistency breaks mental models.
3. **Bring the data forward.** The trigger itself can display information about the microinteraction's state (e.g., a download icon showing progress).
4. **Don't break the affordance.** If it looks like a button, it must act like a button.
5. **Frequency determines visibility.** Common actions need prominent triggers. Rare actions can be hidden (menu, shortcut, gesture).
6. **Invisible triggers must be learnable.** Gestures and shortcuts have no visual cue — they must be discoverable through onboarding, help, or natural exploration.

---

### 2. Rules

Rules define what happens once the microinteraction is triggered. They are the hidden logic — the user never sees them directly, only through feedback.

#### Rule Design Principles

1. **Don't start from zero.** Use previous data, smart defaults, and contextual information to reduce user effort. Pre-fill, auto-detect, remember.
2. **Absorb complexity.** Handle edge cases gracefully so the user doesn't have to. If the system can figure it out, don't ask.
3. **Limit options.** Offer the minimum necessary choices. For microinteractions, one action is ideal; two is acceptable; three or more signals a feature, not a microinteraction.
4. **Prevent errors.** Constrain inputs (character limits, valid ranges, type restrictions) so the user can't enter invalid data.
5. **Use microcopy.** Short, clear text labels and messages are part of the rules. They guide without overwhelming.
6. **Think in states.** Every microinteraction has states: default, active, loading, success, error, disabled. Define all of them.

#### Common States

| State | Description |
|-------|-------------|
| Default / Idle | No interaction happening |
| Hover | Cursor over the element (desktop) |
| Focus | Element has keyboard focus |
| Active / Pressed | Element is being clicked or tapped |
| Loading | Action in progress, awaiting result |
| Success | Action completed successfully |
| Error | Action failed or input is invalid |
| Disabled | Element is not interactive |

---

### 3. Feedback

Feedback is how the rules are communicated to the user. It's what the user sees, hears, or feels.

#### Feedback Channels

| Channel | Speed | Examples |
|---------|-------|----------|
| **Visual** | 20–40 ms to brain | Color change, animation, icon swap, text update |
| **Auditory** | 8–10 ms to brain | Click sound, chime, alert tone |
| **Haptic** | ~50 ms to brain | Vibration, force feedback, taptic engine |

#### Feedback Design Principles

1. **Feedback illuminates the rules.** The user should understand what happened and what's happening now.
2. **Less is more.** Not every action needs visible feedback. Reserve prominent feedback for meaningful state changes.
3. **Match the channel to the message.** Errors benefit from color + haptic. Success benefits from color + sound. Loading benefits from animation.
4. **Use animation as feedback.** Motion communicates: a button scales down to confirm a press, a spinner indicates loading, a checkmark confirms success.
5. **Feedback is personality.** It's where the product's character comes through — playful bounces, smooth eases, sharp snaps.
6. **Think human.** Use real-world analogies. A switch should feel like it clicks. A card should feel like it lifts. A delete should feel weighty.
7. **Don't cry wolf.** If everything flashes and bounces, nothing feels important. Reserve strong feedback for important moments.

---

### 4. Loops & Modes

Loops and modes are the meta-rules — how the microinteraction changes over time or under special conditions.

#### Loops

**Short loops**: What happens during the microinteraction.
- Animation repeat cycle
- Polling interval (check for updates every N seconds)
- Auto-dismiss timer (toast disappears after 5 seconds)

**Long loops**: What happens over the lifetime of the microinteraction.
- First-time use vs. repeated use (progressive disclosure)
- Adaptive behavior (learn from user patterns)
- Degradation (what happens after months of use — is it still relevant?)

#### Modes

Modes change the rules of a microinteraction. They should be used sparingly because they increase complexity.

**Spring-loaded modes**: Temporary — active only while a condition holds.
- Example: Hold Shift to multi-select. Release Shift, mode ends.
- Example: Long press to preview. Release, preview closes.

**One-off modes**: Permanent state changes.
- Example: First-run tutorial. Once completed, never shows again.
- Example: "Don't show this again" checkbox.

#### Principles

1. **Avoid modes when possible.** They add cognitive load.
2. **If you must use a mode, make it obvious.** Visual indicators, different background color, clear labeling.
3. **Spring-loaded modes are safer than persistent modes.** They end automatically.
4. **Long loops are opportunities.** A microinteraction that adapts over time (e.g., skipping confirmations for power users) creates delight.

---

## Putting It Together

When designing (or applying) a microinteraction:

1. **Define the trigger.** What starts it? User action or system condition?
2. **Write the rules.** What happens? What are all the possible states?
3. **Design the feedback.** How does the user know what's happening? Through which channels?
4. **Consider loops and modes.** Does it change over time? Are there special conditions?

Then translate this into your stack.

---

*Reference: Saffer, D. (2013). Microinteractions: Designing with Details. O'Reilly Media.*
