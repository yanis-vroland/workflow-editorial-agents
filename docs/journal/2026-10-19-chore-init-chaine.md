# Journal : initialisation de la chaîne agentique

Branche `chore/init-chaine`.

## 2026-10-19 17:23

### Fait

- Dépôt créé sur GitHub par Yanis avec « Use this template » depuis `agentic-dev-workflow` (public, licence MIT).
- Fichiers propres au template retirés, selon le README du template (section « Nouveau projet ») : specs, ADR-001, `init.sh`, `lint-shell.sh`, leurs tests, `template-ci.yml`, journal du template.
- Retirés en plus, pour obtenir le même résultat qu'`init.sh` : ADR-002 à ADR-005 (le `CLAUDE.md` y renvoie par lien vers le template), `docs/demo/`, `docs/guide-adoption.md`, `renovate.json`.
- `.claude/quality.json` vidé ; dossiers `docs/adr/`, `docs/specs/`, `docs/learnings/` et `docs/journal/` créés vides.
- Cahier des charges, architecture technique et plan copiés depuis `docs/templates/`, encore à remplir par le cadrage.
- Section « Projet » du `CLAUDE.md` complétée : description et règles propres (pas de publication automatique, rien d'inventé, aucune donnée client, charte de Rachel).
- README minimal : accroche et statut « en cours de cadrage ».

### Décisions

- Public : prospects de Vroland & Almeida ; fil « l'IA agentique appliquée aux projets web et mobile, vue de l'intérieur » (Yanis).
- Page LinkedIn Vroland & Almeida, publication toujours manuelle ; l'outil fournit texte et médias (Yanis).
- Sources : actualité et dépôts de Yanis ; 1 post par semaine ; affichage sur vrolandalmeida.com (Yanis).
- Forme : application TypeScript multi-agents avec une interface de validation ; projet mené en parallèle des autres (Yanis).

### Corrections et limites

- Écart dans le README du template : la procédure « Use this template » laisse ADR-002 à 005, `docs/demo/`, `docs/guide-adoption.md` et `renovate.json`, qu'`init.sh` ne copie pas. À remonter en issue dans `agentic-dev-workflow`, avec l'accord de Yanis.
- `.claude/quality.json` vide : pas encore de code, les hooks de lint et de tests sont inactifs.
- Configuration GitHub non faite : application Claude, secret `CLAUDE_CODE_OAUTH_TOKEN`, ruleset sur `main`, label `agent-corrigé`. Tant qu'elle manque, la revue IA de cette PR échouera.

### Prochaine étape

Yanis termine la configuration GitHub et merge cette PR. Ensuite : cadrage (skill `cadrage`) à partir de la fiche `docs/projets/workflow-editorial-agents.md` de l'espace de travail, puis ADR-001 sur l'orchestration des agents.
