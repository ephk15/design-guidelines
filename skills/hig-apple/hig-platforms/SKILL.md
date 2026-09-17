---
name: hig-platforms
description: 'Apple HIG per-platform extensions, made stack-agnostic. The core rules in hig-foundations, hig-components and hig-patterns are platform-independent; THIS skill adds the deltas for each Apple platform (iOS, iPadOS, macOS, watchOS, tvOS, visionOS). Use to review or implement when the target platform is known and its native conventions matter.'
---

# HIG Platforms

The Apple HIG is platform-aware: iPhone, iPad, Mac, Apple Watch, Apple TV, and Vision Pro each have their own conventions for the *same* underlying patterns. This skill is an **extension layer** — it never restates core rules; it adds only what differs per platform.

## How to use

1. Confirm the target platform (or platforms) of the surface you're working on.
2. Load the platform extension file: `platforms/<platform>.md`.
3. Apply core rules from `hig-foundations`, `hig-components`, `hig-patterns`, then layer the platform deltas on top.
4. If the design must run on **multiple platforms**, treat the highest-fidelity platform first, then ensure the deltas of the others don't conflict (flag conflicts explicitly).

## Platform index

| Platform | Source | Extension file |
|---|---|---|
| iOS | `hig-apple/platforms/ios.md` | iPhone / iPod conventions, gestures, aesthetics |
| iPadOS | `platforms/ipados.md` (todo) | multitasking, sidebars, drag-and-drop, larger screens |
| macOS | `platforms/macos.md` (todo) | menu bar, windows, keyboard-first, precise selection |
| watchOS | `platforms/watchos.md` (todo) | glanceability, complications, Digital Crown |
| tvOS | `platforms/tvos.md` (todo) | focus/D-pad navigation, 10-foot UI, Apple TV remote |
| visionOS | `platforms/visionos.md` (todo) | spatial layout, depth, windows/volumes/spaces |
| Cross-device systems | `system-experiences.md` (todo) | widgets, Live Activities, complications, notifications |

## Cross-cutting platform rules

1. **Platform conventions are defaults, not chains.** A custom brand identity can deliberately deviate, but the deviation must be a *design decision*, not an accident (this holds for every platform).
2. **Never copy a platform's control literally across platforms** — gestures/affordances differ (a Mac context menu ≠ a watch context menu). Translate the *intent*, not the widget.
3. **Responsive is table stakes.** The same logical app must adapt layout/input from the smallest to the largest Apple screen, not merely reflow a phone screenshot.
4. **A platform's system affordances are part of its UX** — back gesture (iOS), scroll wheel + menubar (macOS), Digital Crown (watchOS), remote focus (tvOS). Respect them or flag the deviation.

## Working with other skills

- Core rules always come first: foundations → components → patterns → platform deltas.
- `hig-audit` asks which platform(s) a project targets so it can include the platform deltas in its deviation report.
- `hig-orchestrator` detects the target platform (config files, package manifest) and loads the relevant `platforms/<platform>.md`.