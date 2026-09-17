---
name: hig-orchestrator
description: 'Routes design work to the right HIG skill automatically. Detects what the developer is working on (component, pattern, platform, global design) via stack-agnostic code signals, then loads only the relevant rule cards from the hig-apple skillset. Use as the entry point when building or reviewing UI in any technology, or when asked "what HIG rules apply to this?"'
---

# HIG Orchestrator

The automatic router. It figures out *what you're building* and loads *only the rules that matter* — so the Apple HIG guidance arrives exactly when needed and never drowns you in an entire catalog.

## How it works

1. **Detect the moment.** On activation, look at the current work context: files being edited, recently touched files, the current screen/conversation goal. The moment is one of:
   - **Single component** — a specific element being built/refined.
   - **Flow / pattern** — a multi-step experience being built (form, onboarding, settings).
   - **Global / surface** — a whole screen, page, or app shell.
   - **Platform work** — platform-specific setup (iOS conventions, widgets, live activities).
   - **Review request** — user asks "is this HIG-compliant?" → hand off to `hig-audit`.

2. **Collect signals.** Grep the working files for the **triggers** declared in each rule card / pattern index (e.g., `Sheet`, `FilledButton`, `BottomNavigationBar`, `showDialog`, `loading`). These are written stack-agnostically so they work for Flutter, SwiftUI, React, Vue, Kotlin Compose, etc.

3. **Route to the minimal set.** From the matched signals, load:
   - `hig-foundations` always (its rules underpin everything).
   - The matched `hig-components/rules/<name>.md` card(s) — only matched ones.
   - Any matched `hig-patterns/patterns/<name>.md`.
   - The platform extension if the project's platform is known (`hig-platforms/platforms/<platform>.md`).
   Present them as a short summary ("Routing to: nav-bars · lists · light-dark").

4. **If no match** — tell the user plainly what was and wasn't detected and ask what they are working on, or default to foundations-only.

5. **Hand off to audit** when the user wants a review pass.

## Signal index (stack-agnostic)

The canonical source of signals lives in each skill's index/card `Triggers` section. Orchestrator merges them into one lookup. Example knowledge (non-exhaustive — always consult cards for the full set):

| What | Signals to match |
|---|---|
| Button | `Button`, `onPressed`, `onClick`, `Filled/Outlined/Text/Elevated`, `FloatingActionButton`, `<button` |
| Alert | `Alert`, `AlertDialog`, `showDialog`, `confirm`, `messagebox`, `<dialog` |
| Sheet | `BottomSheet`, `showModalBottomSheet`, `presentSheet`, `.sheet(`, `bottom-sheet` |
| Tab bar | `BottomNavigationBar`, `NavigationBar`, `TabBar` (bottom), `tab bar` |
| Tab view | `TabBar`/`TabView` (top), `TabController`, `role="tab"` |
| List | `ListView`, `ListTile`, `FlatList`, `<li>`, `TableRow` |
| Text field | `TextField`, `<input`, `textarea`, `SearchBar` |
| Toggle | `Switch`, `Toggle`, `role="switch"` |
| Progress | `ProgressIndicator`, `Spinner`, `Skeleton`, `loading`, `<progress` |
| Nav bar | `AppBar`, `navigationBar`, `<header`, `Toolbar` |
| Search | `SearchBar`, `searchable`, `type="search"` |
| Entering data | `form`, `TextFormField`, `validator`, wizard `Stepper` |
| Loading | `isLoading`, `FutureBuilder`, `await` + UI, skeleton |
| Feedback | `SnackBar`, `Toast`, `role="alert"`, `errorMessage` |
| Empty state | `isEmpty`, no-data ternary, `ListView` empty |

**Platform detection signals:** `ios/`, `Info.plist`, `xcodeproj`, `macos/`, `watchos/`, `tvOS`, `visionOS`, `android/` (→ not an Apple audit target), package manifest hints.

## Decision rules

- **One component matched →** load that component's card (+ foundations). Done.
- **Several components on the same screen →** load their union; dedupe shared rules.
- **Flow detected →** load the pattern card, plus the component cards of the fields/buttons it references.
- **Whole surface →** full foundations + the surface's component/patter union.
- **Suspected audit request →** prompt to run `hig-audit` instead of spot-loading rules.

## Working with other skills

- Tells `hig-audit` what to audit and with which cards.
- Uses card/pattern indexes as its signal source.
- Is fully **read-only** for the described flow — it routes and consults, it does not change code.