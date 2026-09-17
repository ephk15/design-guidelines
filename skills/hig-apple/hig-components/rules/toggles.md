# Toggles — rule card

A **toggle** (switch) is a control for an on/off binary state that takes effect *immediately* where flipped. Distinct from checkboxes (form-commit semantics) and from radio/segments (multiple exclusives).

**Triggers**: `Switch`, `Toggle`, `toggle`, `CupertinoSwitch`, `MaterialSwitch`, `switch`, `ToggleButton`, `toggleSwitch`, `switchRole`, `role="switch"`, `on/off` control, `checkbox` (review whether semantics match).

## Rules

1. **Immediate effect.** A switch's state change applies instantly — the setting is live. If the change requires a "Save"/"Apply" step later, a switch is the wrong control (prefer checkbox/radio in a form).
2. **The label states the controlled thing.** The text beside a switch is the feature it toggles ("Wi-Fi", "Dark Mode", "Notifications"), not an instruction.
3. **Binary only.** If state can be "sometimes" or has three+ stable values, use segmented control/radio — a switch can't express a third state.
4. **Agreement not adhesion.** Labels should describe the service ("Send analytics") not pretend the user wants it ("Love getting promotional emails").
5. **Consistent visual language:** on = filled/emphasis; off = dimmed/neutral. The same switch family everywhere.
6. **Reversible and safe.** Toggling must never be destructive without an additional confirm (e.g., a switch that deletes data on flip needs protection).
7. **Readable while off** — off state must remain legible (never cryptic grayout with unseen description).

## The why

A switch promises "flip → done." The moment it lies (needs save, or the "done" is a setup for something else) the user loses trust in the entire settings surface.

## Implementation hints

- Detect triggers above. Check:
  - Setting applied on flip or staged for later save? Staged → flag wrong control.
  - Label > 2-3 words or phrased as user's desire → flag (rephrase to describe the feature).
  - Multiple exclusive options (A/B/C) implemented as switches → flag, suggest segments/radio.
  - Any switch with destructive consequence without confirm → flag.
  - Off-state legibility → check contrast/opacity.

## Checklist

- [ ] live effect on flip
- [ ] label = the controlled feature
- [ ] strictly binary
- [ ] honest description
- [ ] consistent on/off visual language
- [ ] no unguarded destructive flip