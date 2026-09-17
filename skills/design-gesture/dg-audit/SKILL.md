---
name: dg-audit
description: 'Audit a screen or project against the Design Gesture ruleset (craft-agnostic), stack-agnostic. Produces a prioritized list of deviations with severity, the rule violated, and a proposed fix — never a bare score. Supports delta tracking between runs. Use when asked to review, audit, or check craft-agnostic design-gesture compliance of an interface or codebase.'
---

# Audit

Part of the Design Gesture (dg) module — craft-agnostic design rules that apply whatever system (or none) you use.

This skill is a routing/rule-card holder: it loads only the dg rule cards relevant to what you are working on, exactly like its platform-bound siblings (hig-apple, m3-material) but without assuming any single design system.

For platform-specific enforcement (Apple HIG → hig-*, Material 3 → m3-*), delegate to those modules. For everything else, apply the dg rules here directly.
