# Plan

Ordre des travaux du projet, de la première à la dernière PR. Il est rempli par le cadrage (skill `cadrage`), puis tenu à jour par chaque PR. Le statut de chaque fonctionnalité est dans le [cahier des charges](cahier-des-charges-fonctionnel.md#fonctionnalités) : ce plan y renvoie sans le recopier ([spec 008](https://github.com/yanis-vroland/agentic-dev-workflow/blob/main/docs/specs/008-cadrage-et-plan-global.md)).

## Objectif

Un premier post réel, préparé par l'équipe d'agents à partir d'un profil privé, validé et publié à la main, puis affiché sur le site de la marque par l'export. Le détail est dans [« Objectif et périmètre »](cahier-des-charges-fonctionnel.md#objectif-et-périmètre) du cahier des charges.

## Règles de mise à jour

- Une PR coche, dans le même commit que son travail, les cases des tâches qu'elle termine, et seulement celles-là. Un lot de fonctionnalité est coché quand elle passe « livrée » dans le cahier des charges.
- Ajouter, retirer ou réordonner un lot est une proposition de l'agent : elle est consignée dans « Écarts au plan » et validée par l'humain dans la PR.
- Au début de chaque session, l'agent propose la première tâche non cochée et la lance après l'accord de l'humain.

## Lots

| Lot | Contenu | Dépend de | Branche prévue |
| --- | --- | --- | --- |
| A | Cadrage : cahier des charges, architecture technique, plan | — | `docs/cadrage` |
| B | ADR-001 orchestration et ADR-002 stack et stockage | A | `docs/adr-001-orchestration`, `docs/adr-002-stack` |
| C | Socle : monorepo, lint, tests, CI, `.env.example`, garde-fou des noms exclus | B | `chore/socle` |
| D | F1 Profil | C | `feat/profil` |
| E | F2 Veille RSS | D | `feat/veille-rss` |
| F | F3 Archives GitHub | D | `feat/archives-github` |
| G | F4 Angle | E, F | `feat/angle` |
| H | F5 Rédaction et critique | G | `feat/redaction-critique` |
| I | ADR-003 rendu des gabarits, puis F6 Visuel | D | `docs/adr-003-rendu`, `feat/visuel` |
| J | F7 Interface de validation (charte et maquette de l'interface, puis code) | H, I | `feat/interface-validation` |
| K | F8 Export | J | `feat/export` |
| L | Jalon MVP : premier post réel publié et affiché | K | — |
| M | Phase 2 : F9 à F13, ordre à décider après le MVP | L | — |

## Tâches

### Lot A : cadrage

- [ ] Cadrage validé : cahier des charges, architecture technique et plan.

### Lot B : décisions d'architecture

- [ ] ADR à rédiger : ADR-001 orchestration des agents (Claude Agent SDK ou LangGraph.js).
- [ ] ADR à rédiger : ADR-002 stack de l'application locale et stockage des posts.

### Lot C : socle

- [ ] Socle : monorepo pnpm, TypeScript, lint, tests, CI, `.claude/quality.json`, `.env.example`, et garde-fou des noms exclus (spec 010 du template, après le merge de sa PR).

### Lots D à K : fonctionnalités du MVP

- [ ] [F1 Profil](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] [F2 Veille RSS](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] [F3 Archives GitHub](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] [F4 Angle](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] [F5 Rédaction et critique](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] ADR à rédiger : ADR-003 rendu des gabarits médias.
- [ ] [F6 Visuel](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] Charte et maquette de l'interface de validation (skill `maquette`).
- [ ] [F7 Interface de validation](cahier-des-charges-fonctionnel.md#fonctionnalités)
- [ ] [F8 Export](cahier-des-charges-fonctionnel.md#fonctionnalités)

### Lot L : jalon MVP

- [ ] Premier post réel publié avec son visuel et affiché sur le site par l'export (avec l'humain).

## Tâches de l'humain

- [ ] **[Humain]** Valider le cadrage (PR `docs/cadrage`).
- [ ] **[Humain]** Répondre aux questions ouvertes : budget mensuel, date de fin du MVP.
- [ ] **[Humain]** Valider les ADR 001 à 003.
- [ ] **[Humain]** Créer le profil privé de la marque à partir de son design system, et la liste `.excluded-names` du dépôt (après F1).
- [ ] **[Humain]** Faire valider une fois les gabarits du profil par le propriétaire de la charte (après F6).
- [ ] **[Humain]** Créer la page LinkedIn de la marque, publier le premier post et coller son URL.
- [ ] **[Humain]** Brancher le site de la marque sur l'export (hors de ce dépôt).

## Jalons

| Date | Jalon ou décision |
| --- | --- |
| À fixer (question ouverte) | Fin du MVP : premier post réel publié et affiché |

## Écarts au plan

| Date | Écart | Raison | Décidé par |
| --- | --- | --- | --- |
| | | | |
