# Sliders — rule card

A **slider** lets the user select a value from a continuous or discrete range by dragging a thumb. Material: continuative and discrete (stop points), single and dual-range.

**Triggers** (stack-agnostic detection signals): `Slider`, `SliderTheme`, `<input type="range">`, `slider`, `RangeSlider`, `discrete`.

## Rules

1. **Know when a slider is the right control**: sliders are for *relative* value selection where position communicates proportion (volume, brightness). Exact precise values usually belong in a stepper/number field; binary settings never use a slider.
2. **Discrete vs continuous**: discrete sliders snap to stop points and *show the current value* (value label) — use them when the domain is step-like. Continuous shows no tick in flux and needs a live value readout.
3. **Value always visible**: the current value is shown near the slider (label above/below or value bubble) — a slider without a readout is a guessing game.
4. **Feedback**: dragging shows the thumb's state layer; release commits; `onChangeEnd` for the committed value (don't fire expensive actions on every drag tick).
5. **Labels**: a label states what the slider controls; min/max at the ends when not obvious from context.
6. **Touch target ≥ 48dp**: the thumb is hit-area sized, and the track is tappable/draggable; handle thickness matches platform minimums.
7. **Accessibility**: the thumb is a focusable control announcing value + range (aria-valuenow/valuemax); keyboard adjusts step-wise.
8. **Dual-range**: for "between X and Y" use dual-range, with both handles showing values.

## The why

Sliders communicate *position along a continuum*, which no spinner can. Losing the live value or announcing nothing defeats the entire point of the gesture.

## Implementation hints

- Detect via triggers. Then check:
- No value readout → flag.
- Continuous slider where domain is discrete → flag (make it discrete with stops).
- Actions fired continuously during drag instead of on commit → flag.
- No min/max label or unit → flag.
- Thumb < 48dp interactive → flag.

## Checklist

- [ ] slider justified vs stepper/number field
- [ ] discrete vs continuous correct for domain
- [ ] value always visible
- [ ] commit on release, not per-drag-tick
- [ ] labels + min/max when needed
- [ ] ≥ 48dp target, SR announces value/range