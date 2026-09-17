# iOS — platform extension

> Served by `hig-platforms`. iOS is the default/reference Apple mobile platform — iPhone & iPod touch portraiture, gestures, and phone-first UX. iPadOS gets its own extension; this file covers phone-scale behavior.

## Deltas vs the core rules

Core rules (foundations/components/patterns) already apply. This file adds the **iOS-specific layer**:

### Gesture & navigation (iOS-native)
1. **Swipe-back from the left edge** is expected for pushed screens. No visible button requirement, but the back affordance must exist (`see components/navigation-bars`).
2. **Swipe actions** on list rows (reveal destructive / mark-as / more) are standard iOS; implement or intentionally opt out.
3. **Defer to system back stack**: prefer native navigation container over hand-rolled back buttons that fight the gesture.
4. **Full-screen content + native safe areas**: respect notch/dynamic island, home indicator, and keyboard insets; content must not hide under them.

### Texture & materials
5. **Tab bar is bottom-anchored** and keeps its translucent/glass feel — it floats with depth, not a harsh separator card.
6. **Toolbars** carry screen-scoped actions; **nav bars** carry title + back + few actions. Don't merge them into a single mega-bar.
7. **Native sheets** (drag-to-dismiss, grabber) are the default for modal utility work (`see components/sheets`).

### Aesthetic discipline
8. **Large-title navigation** on level-1 screens is iOS-native (collapses into compact title on scroll). Use it to signal "top of a hierarchy", keep detail screens compact.
9. **System text styles** (Large Title → Caption) carry semantic type scaling (\= Dynamic Type). Don't fight them with bespoke sizes unless brand-demanded — any custom type must still scale.
10. **SF Symbols / system glyphs** for iconography where the brand permits; consistent family elsewhere (`see foundations icons`).
11. **Haptics**: native Taptic feedback on consequential/momentous actions (selection, success, error). Subtle, not spammy.

### System surfaces
12. **Share sheet / activity view** is the iOS-expected pattern for sharing; don't invent a custom share dialog.
13. **Permission prompts** appear in context, with a clear one-line "why" — they are a designed moment, never an afterthought (`see foundations privacy`).

## Implementation hints

- Detect target: iOS config (`ios/`, `Info.plist`, `project.pbxproj`, Flutter `ios/` folder, SwiftUI, UIKit).
- Check gestures: swipe-back supported or deliberate opt-out; swipe actions on interactive lists; safe-area handling; sheet dismissibility via drag.
- Check: large-title present on top-level, compact on detail; type follows system scale; icons from a consistent family; haptics present on key actions but restrained.

## Checklist

- [ ] swipe-back honored (or deliberate off for brand)
- [ ] swipe actions where standard
- [ ] native back stack, no hand-rolled back
- [ ] safe areas respected (notch, indicator, keyboard)
- [ ] bottom tab bar transparent/glass
- [ ] sheets drag-dismissible with grabber
- [ ] large-title on top-level screens only
- [ ] type scales with Dynamic Type
- [ ] consistent icon family
- [ ] haptics restrained and meaningful
- [ ] permissions in context with why