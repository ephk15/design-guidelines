---
name: dg-orchestrator
description: 'Routes design work to the right Design Gesture skill automatically. Detects what you are building (component, pattern, platform, or a craft-agnostic gesture concern) via stack-agnostic signals pointing at code, then loads only the relevant dg rule cards. Use as the entry point when building or reviewing UI in any technology, or when asked what craft-agnostic design rules apply here.'
---

# Orchestrator

Part of the Design Gesture (dg) module — craft-agnostic design rules that apply whatever system (or none) you use.

This skill is a routing/rule-card holder: it loads only the dg rule cards relevant to what you are working on, exactly like its platform-bound siblings (hig-apple, m3-material) but without assuming any single design system.

For platform-specific enforcement (Apple HIG → hig-*, Material 3 → m3-*), delegate to those modules. For everything else, apply the dg rules here directly.
