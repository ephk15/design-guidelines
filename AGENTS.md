# AGENTS.md — design-guidelines

Repo public de **modules de design-systèmes installables au format BMAD**, chacun livré comme une structure de skills communautaire qu'installent les agents (Claude Code, Codex, Cursor, etc.).

Trois modules publiés : `hig-apple` (Apple HIG), `m3-material` (Material 3), `design-gesture` (gestes de design cross-platform). Chaque module vit dans `skills/<module>/` et contient :
- `<module>-setup/` — la config native : `assets/module.yaml`, `assets/module-help.csv` (catalogue local), `scripts/merge-config.py` + `scripts/merge-help-csv.py`, `SKILL.md`.
- 7 skills frères `<module>-*` (audit, components, foundations, gesture/patterns/platforms selon le module, orchestrator) — chacun son `SKILL.md`.

## Politique de versionning

- [Semantic Versioning](https://semver.org/) strict : `MAJOR.MINOR.PATCH` (MAJOR = rupture, MINOR = fonctionnalité rétro-compatible, PATCH = correctif).
- Chaque **commit** = un ajout isolé qui passe le validateur natif avec **0 finding** : message `feat(<module>): …` / `fix(<module>): …` — un commit **par module** (pas de fourre-tout).
- Chaque **release** = un **tag `vX.Y.Z`** poussé (`git push origin vX.Y.Z`) + une **GitHub Release** (notes rédigées, artefacts si présents). `0.x` = API instable (prerelease) ; `v1.0.0` = premier contrat public.
- **CHANGELOG.md** à la racine au format [Keep a Changelog](https://keepachangelog.com/) : section `## [Unreleased]` alimentée au fil des commits ; à la release, la section devient datée.
- Toute évolution du **catalogue racine** (`skills/<module>/<module>-setup/assets/module-help.csv` puis fusion dans le catalogue BMAD global) ou du TOML de config passe par les scripts natifs de merge (`merge-help-csv.py`, `merge-config.py`) — **jamais** d'édition à la main du registre.

## Contribuer

1. Lire `CONTRIBUTING.md` (workflow complet, branches, PR, relecture).
2. Ouvrir un sujet avec un titre clair avant toute PR ; utiliser les templates d'issue.
3. Tout code doit passer : validateur du module (`validate-module.py <module-dir>` → 0 finding) + tests le cas échéant.
4. PR ciblée vers `main`, relecture obligatoire (au moins 1 approbation), squash au merge.
5. Comportement attendu : code de conduite (`CODE_OF_CONDUCT.md`) — contributions respectueuses ; signaler les vulnérabilités via `SECURITY.md`, jamais en issue publique.

## Non-négociables

- Ne jamais scraper/copier le contenu propriétaire d'un fabricant (Apple, Google…) à l'identique : on **résume/distille** la logique de design, on ne reproduit pas les artworks, logos ou textes.
- Pas de secrets commités ; `.env*` toujours ignorés.
- La structure BMAD des modules est exacte — on ne réinvente pas le gabarit.
- Le repo reste public & libre (licence MIT) : tout le contenu y est publiable en l'état.

## Commandes

- Valider un module : `python3 .agents/scripts/bmad-module-builder/scripts/validate-module.py skills/<module>` (doit rendre `status: pass`, `findings: 0`).
- Fusionner un nouveau module dans le registre racine : exécuter les merge scripts natifs du module (ils mettent à jour catalogue + TOML).
- Livrer : `git add <chemin isolé> && git commit && git push origin main`.

Quand un point de ce fichier entre en conflit avec un autre doc, **le code et ce fichier priment** ; signaler l'incohérence en issue.
