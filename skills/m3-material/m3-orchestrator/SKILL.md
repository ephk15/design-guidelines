---
name: m3-orchestrator
description: 'Routes design work to the right Material Design 3 (M3) skill automatically. Detects what the developer is working on (component, pattern, platform/breakpoint, global design) via stack-agnostic code signals, then loads only the relevant rule cards from the m3-material skillset. Use as the entry point when building or reviewing UI in any technology, or when asked "what M3 rules apply to this?"'
---

# M3 Orchestrator

The automatic router for the Material 3 skillset. It figures out *what you're building* and loads *only the rules that matter* — so the M3 guidance arrives exactly when needed and never drowns you in an entire catalog.

## How it works

1. **Detect the moment.** On activation, look at the current work context: files being edited, recently touched files, the current screen/conversation goal. The moment is one of:
   - **Single component** — a specific element being built/refined.
   - **Flow / pattern** — a multi-step experience being built (form, onboarding, settings).
   - **Global / surface** — a whole screen, page, or app shell.
   - **Responsive work** — breakpoints, densities, adaptive layout.
   - **Review request** — user asks "is this M3-compliant?" → hand off to `m3-audit`.

2. **Collect signals.** Grep the working files for the **triggers** declared in each rule card / pattern index (e.g., `FilledButton`, `CardTheme`, `BottomNavigationBar`, `showModalBottomSheet`, `ProgressIndicator`). These are written stack-agnostically so they work for Flutter, Jetpack Compose, React, Vue, Kotlin, etc.

3. **Route to the minimal set.** From the matched signals, load:
   - `m3-foundations` always (its rules underpin everything).
   - The matched `m3-components/rules/<name>.md` card(s) — only matched ones.
   - Any matched `m3-patterns/patterns/<name>.md`.
   - The responsive extension if breakpoint/adaptive work is detected (`m3-platforms/platforms/adaptive.md`).
   Present them as a short summary ("Routing to: buttons · text-fields · state-layers · dark").

4. **If no match** — tell the user plainly what was and wasn't detected and ask what they are working on, or default to foundations-only.

5. **Hand off to audit** when the user wants a review pass.

## Signal index (stack-agnostic)

The canonical source of signals lives in each skill's index/card `Triggers` section. Orchestrator merges them into one lookup. Example knowledge (non-exhaustive — always consult cards for the full set):

| What | Signals to match |
|---|---|
| Button | `Button`, `FilledButton`, `OutlinedButton`, `TextButton`, `ElevatedButton`, `onPressed`, `onClick`, `<button` |
| FAB | `FloatingActionButton`, `FAB`, `extended` |
| Card | `Card`, `CardTheme`, `card-`, `<mat-card`, `ExpansionTile` |
| Chip | `Chip`, `FilterChip`, `AssistChip`, `InputChip`, `SuggestionChip` |
| Bottom sheet | `showModalBottomSheet`, `BottomSheet`, `modal-bottom-sheet`, `DraggableScrollableSheet` |
| Snackbar | `SnackBar`, `showSnackBar`, `<mat-snack`, `toast` |
| Dialog | `showDialog`, `AlertDialog`, `Dialog`, `<dialog`, `fullscreenDialog` |
| Text field | `TextFormField`, `TextField`, `<input`, `OutlinedTextField`, `FilledTextField` |
| Toggle | `Switch`, `Checkbox`, `Radio`, `role="switch"` |
| Slider | `Slider`, `<input type="range"` |
| Tabs | `TabBar`, `TabController`, `tabs`, `role="tablist"` |
| Progress | `ProgressIndicator`, `CircularProgressIndicator`, `LinearProgressIndicator`, `<progress` |
| Navigation bar | `NavigationBar`, `BottomNavigationBar`, `NavigationRail`, `NavigationDrawer` |
| App bar | `AppBar`, `app-bar`, `<header`, `AppBarTheme` |
| Menu | `DropdownMenu`, `PopupMenuButton`, `showMenu`, `<select`, `dropdown` |
| List | `ListView`, `ListTile`, `Card` list, `<li>`, data tables |
| Entering data | `form`, `TextFormField`, `validator`, wizard, `Stepper` |
| Loading | `isLoading`, `FutureBuilder`, skeleton, shimmer |
| Feedback | `Snackbar`, role="alert", `errorMessage`, validation error |
| Empty state | `isEmpty`, no-data ternary, `ListView` empty |
| Adaptive / responsive | `MediaQuery`, `Breakpoint`, `breakpoint`, `LayoutBuilder`, `maxWidth`, `WindowSizeClass` |
| Dark mode | `darkTheme`, `darkColorScheme`, `ThemeData.dark`, `prefers-color-scheme` |

**Platform detection signals:** `compose`, `android`, `flutter`, `react`, `vue`, `web`, `material.dart`, `material/`, `--md-` tokens, `ThemeData`, package manifest hints.

## Decision rules

- **One component matched →** load that component's card (+ foundations). Done.
- **Several components on the same screen →** load their union; dedupe shared rules.
- **Flow detected →** load the pattern card, plus the component cards of the fields/buttons it references.
- **Whole surface →** full foundations + the surface's component/pattern union.
- **Adaptive/responsive work →** also load `m3-platforms/platforms/adaptive.md`.
- **Suspected audit request →** prompt to run `m3-audit` instead of spot-loading rules.

## Working with other skills

- Tells `m3-audit` what to audit and with which cards.
- Uses card/pattern indexes as its signal source.
- Is fully **read-only** for the described flow — it routes and consults, it does not change code.