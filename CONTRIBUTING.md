# Contribuer à design-guidelines

Merci de vouloir contribuer ! Ce dépôt regroupe des **modules de design-systèmes** (Apple HIG, Material 3, Design Gesture) au format communautaire **BMAD installable**.

## Ce dont on a besoin

- De nouveaux modules de design-systèmes ou des suggestions de modules existants
- Des corrections de contenu, de structure ou de fichiers de config des modules existants
- De la documentation, des exemples et des traductions
- Des retours sur l'installabilité réelle des modules (testez-les dans vos projets)

## Avant de commencer

1. Lisez `AGENTS.md` — c'est le contrat source de vérité (politique de versionning, structure BMAD, non-négociables).
2. Ouvrez un sujet (issue) pour toute contribution substantielle avant de coder, ou référencez l'issue dans votre PR.

## Développement local

- Un module BMAD vit dans `skills/<module>/` et a la structure exacte : `*-setup` (configuration native + catalogue + scripts de merge) + 7 skills frères `*-*`.
- Validation (obligatoire, doit rendre 0) :
  ```sh
  python3 .agents/skills/bmad-module-builder/scripts/validate-module.py skills/<module>
  ```
- Catalogue + config globaux : fusion via les scripts natifs de merge du module (`merge-config.py`, `merge-help-csv.py`) — **jamais** d'édition à la main. Toute nouvelle skill doit être déclarée dans `assets/module-help.csv` du `-setup`, au format du catalogue.

## Processus de PR

- **Un commit par module** (message `feat(<module>): …`), idéalement un seul.
- Passez la validation (0 finding) AVANT d'ouvrir la PR, et mentionnez le résultat dans la description.
- Ciblez `main`. Attendez une relecture (au moins 1 approbation).
- Restez dans le périmètre de votre sujet ; ne mélangez pas deux modules dans une PR.

## Après la PR

Les mainteneurs taguent les releases (`vX.Y.Z`) et maintiennent `CHANGELOG.md`. Voir la politique complète dans `AGENTS.md`.
