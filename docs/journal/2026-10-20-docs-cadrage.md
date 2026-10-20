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

## 2026-10-20 12:02

### Fait

- Cadrage complété après relecture de Yanis : types de post et variété (RM9, F4 renommée « Type et angle »), projets cités seulement s'ils sont publics ou déclarés publiables (RM10), historique des posts passé en MVP (F12), panel de relecture par personas en phase 2 (F14, RM11), préparation planifiée en phase 2 (F15).
- Glossaire : Type de post, Historique, Persona, Avis ; une source peut être une entrée du profil (présentation, prestation, projet).
- Plan : lot K2 (F12) avant le jalon MVP ; F14 en premier lot de la phase 2.

### Décisions

- Préparation à la demande au MVP, automatisation plus tard (Yanis).
- Historique des posts et variété des types (Yanis).
- Panel de relecture en phase 2 ; l'éditeur coche les conseils retenus, le Rédacteur réécrit (Yanis).
- Types de post portés par des fiches du profil plutôt que par un agent par type : proposition de l'agent, à valider par Yanis dans la PR.

### Corrections et limites

- Le MVP grossit d'une fonctionnalité (F12) : à surveiller face à la priorité P2.

### Prochaine étape

Yanis valide le cadrage dans la PR #2. Ensuite : ADR-001 sur l'orchestration des agents.
