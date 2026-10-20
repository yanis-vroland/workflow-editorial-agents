# Cahier des charges fonctionnel

Ce que fait le produit, pour qui, et selon quelles règles. Ce document est la référence pour les acteurs, le glossaire et les règles métier. Chaque spec de `docs/specs/` détaille une fonctionnalité ; ce document la résume et renvoie vers elle.

Il est mis à jour dans la PR qui change ce qu'il décrit : nouvelle fonctionnalité, acteur, droit, terme ou règle métier, changement de statut d'une spec. Une section sans objet pour le projet reste, avec « Sans objet » et une phrase d'explication.

## Objectif et périmètre

Une petite structure (studio, freelance, PME) veut publier régulièrement sur LinkedIn des posts fondés sur ce qu'elle fait vraiment, sans y passer une demi-journée par semaine. L'outil est une équipe d'agents IA, lancée en local et à la demande, qui prépare un post prêt à publier : veille sur l'actualité et sur des dépôts de code publics, type de post et angle choisis pour varier d'un post à l'autre, texte, visuel aux couleurs de la marque. L'éditeur valide, corrige ou jette, puis publie lui-même. Ce qui distingue l'outil : rien n'est inventé (chaque affirmation renvoie à une source), et la marque n'est qu'un **profil** privé, chargé au lancement : le code et le dépôt restent génériques et publics.

Hors périmètre :

- Publication automatique sur LinkedIn, ou sur tout autre réseau : jamais.
- Lecture des statistiques LinkedIn.
- Image générée par IA (contraire à RM2, et la charte serait mal rendue).
- Préparation automatique ou planifiée au MVP : elle est prévue en phase 2 (F15).
- Hébergement multi-utilisateurs, comptes, authentification : l'outil tourne sur le poste de l'éditeur.
- Le site qui affiche les posts publiés : il consomme l'export (F8), hors de ce dépôt.

## Sources

Le dépôt est public et l'outil générique : les sources propres à une marque ne sont **pas** copiées dans `docs/sources/`, contrairement à la procédure du cadrage (décision de Yanis, 2026-10-20). Elles restent privées, hors dépôt, et seul ce qui est générique en est tiré ici.

| Source | Date ou version | Ce qui en est tiré |
| --- | --- | --- |
| Fiche projet privée de Yanis (hors dépôt) | 2026-10-19 | Les six agents et le rôle de l'éditeur ; médias rendus par code depuis des gabarits, sans image générée ; règles « jamais de publication automatique » et « rien d'inventé » ; export des posts publiés vers un site ; arrêt du MVP au premier post réel publié et affiché. |
| Design system d'une marque utilisatrice (artefact privé, hors dépôt) | 2026-10-20 | La forme d'un profil : tokens de couleur, typographies, rayons, logos, règles de ton et de rédaction. Sert de cas réel pour valider le format du profil (F1), sans être recopié. |
| Réponses de Yanis au cadrage | 2026-10-20 | Outil générique, profil privé non versionné, exemple de profil fictif ; un seul utilisateur, en local, sans authentification ; préparation à la demande, automatisation plus tard ; interface web locale ; veille par flux RSS et dépôts GitHub publics ; un visuel statique au MVP, autres médias en phase 2 ; export JSON ; historique des posts et variété des types de post ; panel de relecture par personas en phase 2, l'éditeur choisit les conseils retenus. |

## Acteurs et droits

La mise en œuvre technique des droits est dans [`architecture-technique.md`](architecture-technique.md#sécurité).

| Acteur | Rôle | Peut | Ne peut pas |
| --- | --- | --- | --- |
| Éditeur | Personne qui fait tourner l'outil pour sa marque, sur son poste | Écrire son profil ; lancer une préparation, en imposant ou non un type de post ; consulter l'historique des posts ; lire, corriger, rejeter ou valider un post proposé ; coller l'URL d'un post publié ; produire l'export | Faire publier l'outil à sa place (RM1) |
| Propriétaire de la charte | Personne qui détient l'identité visuelle de la marque (peut être l'éditeur) | Valider une fois les gabarits du profil (RM6) | — (n'utilise pas l'outil directement) |
| Agents | Veilleur, Archiviste, Stratège, Rédacteur, Directeur média, Critique ; en phase 2, les personas du panel et la Synthèse : composants de l'outil, pas des personnes | Lire les sources déclarées dans le profil et l'historique des posts ; produire signaux, type et angle, texte, visuel, verdict, avis | Publier ; changer de statut un post au-delà de « proposé » ; modifier le profil ou la charte |
| Site consommateur | Site de la marque, hors de ce dépôt | Lire l'export (F8) | Écrire dans l'outil |

## Glossaire

| Terme | Nom dans le code | Définition |
| --- | --- | --- |
| Profil | `Profile` | Tout ce qui est propre à une marque : nom, public, ligne éditoriale, ton, langue, présentation, prestations, projets publiables, catalogue de types de post, charte (tokens, polices, logos), sources à surveiller, personas, noms exclus. Fichier local non versionné ; un exemple fictif est versionné. |
| Préparation | `Run` | Une exécution de l'équipe d'agents, lancée par l'éditeur, qui aboutit à un post proposé ou à un échec motivé. |
| Signal | `Signal` | Élément candidat repéré par le Veilleur (article d'un flux RSS) ou l'Archiviste (commit, ADR, PR, journal d'un dépôt public), avec son URL. |
| Type de post | `PostType` | Famille de post déclarée dans le catalogue du profil (exemples : présentation de la marque, actualité, projet en cours ou livré, prestation), avec ses consignes : sources attendues, structure, gabarit. |
| Source | `Source` | Signal retenu, ou entrée du profil (présentation, prestation, projet publiable), cité par un post : chaque affirmation du post y renvoie. |
| Angle | `Angle` | Ce que dit le post et pourquoi il intéresse le public du profil, choisi par le Stratège à partir des signaux et du type de post. |
| Historique | `PostHistory` | Liste de tous les posts, quel que soit leur statut, avec type, angle, date, sources et URL ; consultée par l'éditeur et lue par le Stratège pour varier. |
| Post | `Post` | Texte, média et sources d'une préparation, avec son statut (voir « Statuts et transitions »). |
| Média | `Media` | Fichier joint au post (au MVP : un visuel PNG), produit en remplissant un gabarit. |
| Gabarit | `Template` | Mise en page rendue par code (HTML ou SVG) qui applique la charte du profil ; les agents le remplissent, ils ne dessinent pas. |
| Verdict | `Review` | Résultat du Critique sur un post : accepté, ou renvoyé au Rédacteur avec les motifs. |
| Persona | `Persona` | Phase 2. Lecteur type déclaré dans le profil (rôle, attentes, objections), simulé par un agent du panel de relecture. Jamais présenté comme un vrai retour client. |
| Avis | `Feedback` | Phase 2. Points forts, points faibles et conseils de modification d'un persona sur un post proposé ; la Synthèse les fusionne et les classe. |
| Export | `Export` | Fichier JSON versionné des posts publiés, lu par le site consommateur. |
| Noms exclus | `excludedNames` | Noms (clients, employeurs) qui ne doivent apparaître ni dans un prompt ni dans un post. Liste privée, jamais versionnée. |

## Règles métier

### Statuts et transitions

| Objet | De | Vers | Condition | Qui |
| --- | --- | --- | --- | --- |
| Post | — | en préparation | Préparation lancée à la demande | Éditeur |
| Post | en préparation | proposé | Verdict « accepté » du Critique | Agents |
| Post | en préparation | échoué | Limite d'itérations atteinte ou erreur, motif conservé | Agents |
| Post | proposé | en préparation | Phase 2 : conseils du panel cochés, réécriture par le Rédacteur puis nouveau verdict du Critique | Éditeur |
| Post | proposé | validé | Relecture, corrections éventuelles | Éditeur |
| Post | proposé | rejeté | Motif facultatif | Éditeur |
| Post | validé | publié | URL du post LinkedIn collée | Éditeur |

### Autres règles

- RM1 : l'outil ne publie jamais. Aucune intégration n'écrit sur LinkedIn ; la publication est un geste de l'éditeur.
- RM2 : rien d'inventé. Chaque affirmation factuelle d'un post renvoie à au moins une source (signal ou entrée du profil), et aucun chiffre, témoignage ou cas client n'apparaît sans source. Le Critique refuse un post qui enfreint cette règle.
- RM3 : un post proposé à l'éditeur a reçu un verdict « accepté » du Critique.
- RM4 : aucun nom exclu du profil n'apparaît dans un prompt envoyé à un modèle ni dans un post ; un post qui en contient est refusé.
- RM5 : l'outil ne lit que les sources déclarées dans le profil (flux RSS, dépôts GitHub publics).
- RM6 : un gabarit applique la charte du profil sans la modifier, et n'est utilisé qu'après une validation unique par le propriétaire de la charte.
- RM7 : l'export ne contient que les posts au statut « publié », avec leur texte, leurs médias, leurs sources et leur URL LinkedIn.
- RM8 : le code, les gabarits génériques, les prompts et les exemples du dépôt ne contiennent aucune donnée d'une marque réelle : elle vit dans le profil local.
- RM9 : chaque post a un type, pris dans le catalogue du profil. Sauf type imposé par l'éditeur, le Stratège choisit un type et un angle différents de ceux des derniers posts de l'historique (nombre à trancher, voir « Questions ouvertes »).
- RM10 : un projet n'est cité que s'il est public (dépôt public) ou déclaré publiable dans le profil.
- RM11 : phase 2, le panel de relecture conseille sans jamais bloquer : seul le Critique peut refuser un post. Ses avis n'entrent jamais dans le post ; l'éditeur choisit les conseils retenus.

## Parcours utilisateur

### Éditeur

1. Copie le profil d'exemple, le remplit pour sa marque (ton, public, présentation, prestations, types de post, sources, charte, noms exclus) et fait valider ses gabarits une fois par le propriétaire de la charte (F1, F6).
2. Ouvre l'interface locale et lance une préparation à la demande, en imposant un type de post ou non (F7).
3. Les agents collectent les signaux (F2, F3), choisissent un type et un angle en tenant compte de l'historique (F4), rédigent et font critiquer le texte (F5), produisent le visuel (F6).
4. Relit le post proposé dans l'interface : texte, visuel, sources cliquables ; corrige, rejette ou valide (F7). En phase 2, lit les avis du panel, coche les conseils à retenir et fait réécrire le post (F14).
5. Publie le post à la main sur LinkedIn, puis colle son URL dans l'interface (F7).
6. Produit l'export, que le site de sa marque affiche (F8).
7. Consulte l'historique des posts pour voir ce qui a été fait, par type et par statut (F12).

## Fonctionnalités

| Phase | Fonctionnalité | Spec | Statut |
| --- | --- | --- | --- |
| 1 (MVP) | F1 Profil : format, chargement, validation, exemple fictif | — | à spécifier |
| 1 (MVP) | F2 Veille : signaux depuis les flux RSS du profil (Veilleur) | — | à spécifier |
| 1 (MVP) | F3 Archives : signaux depuis les dépôts GitHub publics du profil (Archiviste) | — | à spécifier |
| 1 (MVP) | F4 Type et angle : choix du type de post dans le catalogue du profil et de l'angle, variés par rapport à l'historique (Stratège) | — | à spécifier |
| 1 (MVP) | F5 Rédaction et critique : texte sourcé, boucle Rédacteur–Critique bornée | — | à spécifier |
| 1 (MVP) | F6 Visuel : un gabarit statique rempli et rendu en PNG (Directeur média) | — | à spécifier |
| 1 (MVP) | F7 Interface de validation : lancer à la demande (type imposé ou non), relire, corriger, rejeter, valider, coller l'URL | — | à spécifier |
| 1 (MVP) | F8 Export JSON des posts publiés | — | à spécifier |
| 1 (MVP) | F12 Historique des posts : liste consultable (date, type, angle, statut, sources, URL) | — | à spécifier |
| 2 | F9 Carrousel (gabarit multi-pages rendu en PDF) | — | à spécifier |
| 2 | F10 Vidéo courte (Remotion) | — | à spécifier |
| 2 | F11 Captures réelles de projets (Playwright) | — | à spécifier |
| 2 | F13 Jeu d'évals du Critique et du Rédacteur | — | à spécifier |
| 2 | F14 Panel de relecture : personas du profil, avis, synthèse, conseils cochés et réécriture (premier lot de la phase 2) | — | à spécifier |
| 2 | F15 Préparation planifiée (automatisation du lancement) | — | à spécifier |

## Questions ouvertes

- Budget mensuel maximum en appels LLM et API (2026-10-20, Yanis). Influence l'ADR-001 et le modèle par agent.
- Date de fin du MVP (2026-10-20, Yanis). Recommandation de l'agent : 4 semaines, pour ne pas retarder P2.
- Nombre maximal d'itérations Rédacteur–Critique avant l'échec d'une préparation (2026-10-20, Yanis ; à trancher dans la spec F5).
- Préparation sans signal pertinent : échec motivé, ou post « de fond » tiré des archives seules ? (2026-10-20, Yanis ; spec F4).
- Nombre de posts récents dont le Stratège doit éviter le type et l'angle (RM9) (2026-10-20, Yanis ; spec F4).
- Catalogue de types de l'exemple fictif : lesquels livrer par défaut ? (2026-10-20, Yanis ; spec F1).
- Le jeu d'évals (F13) doit-il passer en phase 1 ? Il pèse dans la preuve « multi-agents » auprès d'un recruteur (2026-10-20, Yanis).
