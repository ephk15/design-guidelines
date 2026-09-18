# Sécurité

## Politique

- **Pas de secrets commités.** `.env*` est toujours ignoré ; tout secret découvert dans l'historique doit être révoqué puis purgé.
- Les modules contiennent des **instructions de design** (logique, structure, principes) — pas de clés, tokens, credentials ou données privées.

## Signalement d'une vulnérabilité

**Ne créez pas d'issue publique pour une vulnérabilité.** Contactez les mainteneurs en privé via GitHub Security Advisories (repo → Security → Report a vulnerability), ou par email à `ephk15@gmail.com` avec le sujet `[security] <description courte>`.

Vous recevrez une réponse sous **48h** avec les prochaines étapes. Les vulnérabilités validées seront traitées en priorité et, si pertinent, documentées après correctif dans `CHANGELOG.md`.
