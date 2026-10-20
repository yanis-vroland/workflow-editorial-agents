# Journal : cadrage du projet

Branche `docs/cadrage`.

## 2026-10-20 11:36

### Fait

- Cadrage (skill `cadrage`) : cahier des charges, architecture technique et plan remplis, sans spec ni code.
- Sources lues : fiche projet privée et design system d'une marque utilisatrice, cités sans être copiés dans `docs/sources/`.
- `CLAUDE.md` (section « Projet ») et `README` rendus génériques : plus aucun nom de marque, de personne ni de site.
- `.gitignore` : profils réels (`profiles/*.local.yaml`) et `.excluded-names` ignorés.
- Avant cette branche : historique Git du dépôt réécrit pour retirer la liste des noms exclus du `CLAUDE.md` (commit d'initialisation), force-push de `main` et des branches par Yanis, avec un script préparé par l'agent (ses commandes étaient refusées par les permissions). Vérification : 0 occurrence des noms de `.excluded-names`, en local et sur le dépôt distant.

### Décisions

- Outil générique et dépôt public ; données de marque dans un profil local non versionné, exemple fictif versionné (Yanis).
- Sources du cadrage non copiées dans `docs/sources/`, par écart à la procédure du cadrage (Yanis).
- Export JSON des posts publiés, consommé par le site hors de ce dépôt (Yanis).
- Un seul utilisateur, en local, sans authentification ; lancement manuel ; interface web locale ; veille par flux RSS et dépôts GitHub publics ; un visuel statique au MVP (Yanis, en acceptant les propositions de l'agent).
- Réécriture de l'historique pour retirer les noms exclus (Yanis).

### Corrections et limites

- `refs/pull/1/head` et les vues de la PR #1 gardent l'ancien commit : seul le support GitHub peut les purger.
- Les réponses aux questions 5, 6 et 8 du cadrage sont la première option proposée, acceptée par un « tout d'accord » : à confirmer à la validation.
- Budget et date de fin du MVP non donnés : en questions ouvertes.
- Écart au template à remonter : la procédure du cadrage suppose un projet privé (sources copiées dans `docs/sources/`) et ne prévoit pas un outil générique public.

### Prochaine étape

Yanis valide le cadrage dans la PR. Ensuite : ADR-001 sur l'orchestration des agents.
