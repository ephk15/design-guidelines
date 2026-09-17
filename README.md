# design-guidelines

Modules [BMAD](https://github.com/ephk15/bmad) d'application des design guidelines mobiles, formatés **community-modules installables**.

Ce dépôt expose 2 modules de design systèmes, packagés au format natif BMAD (v7, community-modules) :

| Module | Code | Description |
| --- | --- | --- |
| `skills/hig-apple/` | `hig` | **Apple HIG** — Human Interface Guidelines iOS/macOS (architect, foundations, components, patterns, platforms, audit) |
| `skills/m3-material/` | `m3` | **Material 3** — Material Design de Google (architect, foundations, components, patterns, platforms, audit) |

Chaque module suit la structure officielle d'un module BMAD : configuration native (`*-setup`) + skills de travail en frères, sous la forme installable attendue par l'installer BMAD (équivalente à `wds`, `bmb`).

## Installation

### Via l'installer BMAD (recommandé)

L'installer natif BMAD sait consommer les **community-modules** (`community-modules/` dans son cache). Pointez-le vers ce dépôt ou le dossier de module :

```sh
bmad install ephk15/design-guidelines   # installe les 2 modules sur le projet courant
```

### Manuellement (copie dans un projet BMAD)

1. Copiez le dossier module (`skills/hig-apple/` ou `skills/m3-material/`) dans `skills/` du projet cible.
2. Lancez le skill `hig-setup` / `m3-setup` : il fusionne sa config (module.yaml + registre) et son catalogue (module-help.csv → bmad-help.csv), et nettoie le legacy.
3. Le module est alors catalogué (skills disponibles via la BMAD-help) et la configuration registrée.

Le format est agnostique de la version (v6 TOML / v7 config.yaml) : les scripts de merge gèrent les deux.

## Structure

```
design-guidelines/
├── LICENSE
├── README.md
└── skills/
    ├── hig-apple/         # Module Apple HIG
    │   ├── hig-setup/     #   configuration + merge scripts + module.yaml + module-help.csv
    │   └── hig-*/         #   architect, foundations, components, patterns, platforms, audit
    └── m3-material/       # Module Material 3
        ├── m3-setup/     #   configuration + merge scripts + module.yaml + module-help.csv
        └── m3-*/         #   architect, foundations, components, patterns, platforms, audit
```

Chaque `*-setup` contient : `module.yaml` (registre), `module-help.csv` (catalogue), les scripts de merge (`merge-config.py`, `merge-help-csv.py`, `cleanup-legacy.py`) et le `SKILL.md` d'installation.

## Licence

MIT — voir [LICENSE](LICENSE).
