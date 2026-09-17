---
name: "dg-setup"
description: "Enables the Design Gesture (dg) BMAD module in this project. Focus: craft-agnostic enforcement of the gesture fundamentals — rhythm, intent, motion, micro-interaction — with field-normalized deltas, plus a craft-decision orchestration that routes you to the right design system (Apple HIG, Material 3) when the product context demands one. Use when the user asks to install dg, configure Design Gesture, set up gesture rules, or register the dg module."
---

# Design Gesture Setup

## Overview

Installs and configures the **dg** module into a BMAD project. This module owns the **craft-agnostic layer** — what stays true whether your craft is Apple HIG, Material 3, or neither:

- **Gesture orchestration** (`dg-orchestrator`): detects what you're actually building and routes to the correct authority — `hig` if Apple context, `m3` if Material context, or the gesture layer itself when no platform system applies.
- **Gesture audit** (`dg-audit`): runs a compliance pass on gesture/motion/rhythm fundamentals and produces a prioritized deviation list with **delta tracking between runs** (only new/changed deltas reported, never a full re-dump).
- **Gesture foundations/components/patterns/platforms**: the craft-agnostic rules themselves — rhythm, spacing, intent, motion, echo, adaptive deltas.

The module is addressable BMAD-native: it is added to the project `_bmad/config.yaml`, registered in the marketplace catalogue (`bmad-help.csv`), and its setup skill can be invoked repeatedly without duplicating catalogue rows.

## Configuration

Module variables are read from `./assets/module.yaml`. Values are written to:

- `{project-root}/_bmad/config.yaml` → `[modules.dg]` section (module metadata + shared settings)
- `{project-root}/_bmad/config.user.yaml` → user-scoped settings (`user_setting: true` keys), never in shared config
- `{project-root}/_bmad/bmad-help.csv` → catalogue rows (appended idempotently, `code` = `dg`)

`{project-root}` is a **literal token** — never substitute it in config values. In filesystem paths (e.g. `--marketplace-dir`), resolve it to the real project root before running scripts.

## On Activation

1. Read `./assets/module.yaml` for module metadata and variable definitions (`code` = `dg`).
2. Detect a legacy `assets/module.yaml` or existing `[modules.dg]` / `[modules.dg:*]` config section — if present, inform the user this is an **update** and reuse legacy values as defaults.
3. Collect configuration: user-scoped keys (`user_name`, `communication_language`, `document_output_language`) and any module.yaml variable with a `prompt` field.

Respond to the user's arguments with the scaffolder flow, then run the merge scripts:
- `scripts/merge-config.py` — writes `[modules.dg]` into both `config.yaml` and `config.user.yaml` (anti-zombie: drops existing `[modules.dg]` rows first).
- `scripts/merge-help-csv.py` — appends the 8 `dg` rows to `bmad-help.csv` (dropping stale `dg` rows first).
- `scripts/setup-standalone-help.py` — scaffolds the help catalogue entry if absent.

## Output

- `{project-root}/_bmad/config.yaml` — `[modules.dg]` section
- `{project-root}/_bmad/bmad-help.csv` — 8 catalogue rows (code prefix `dg-`)
- Confirmation summary listing registered module + active skills.
