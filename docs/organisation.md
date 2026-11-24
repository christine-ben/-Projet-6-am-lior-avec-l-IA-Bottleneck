# Organisation de mon projet

## 1. Les grandes parties du projet (les lots)

| Lot | Nom                        | Ce que je fais dans ce lot                                                |
| --- | -------------------------- | ------------------------------------------------------------------------- |
| L1  | Cadrage                    | Je prépare le projet, je fais ma veille et j'écris mon cahier des charges |
| L2  | Audit des données          | Je relance mon notebook et je liste les problèmes de qualité des données  |
| L3  | Analyse exploratoire (EDA) | Je revois mon analyse des prix existante (IQR, z-score)                   |
| L4  | Amélioration               | Je teste Isolation Forest avec l'aide de l'IA et je le compare à l'IQR    |
| L5  | Validation                 | Je vérifie les résultats et je les fais valider par mon mentor            |
| L6  | Restitution                | Je nettoie le notebook, j'écris le README et je prépare la présentation   |

## 2. Ma liste de tâches (le backlog)

Un backlog, c'est la liste de tout ce que je dois faire.
Mise à jour : 23/11/2026

| N°  | Ce que je dois faire                                | Temps  | À finir avant | C'est fini quand...                                                          | Où j'en suis |
| --- | --------------------------------------------------- | ------ | ------------- | ---------------------------------------------------------------------------- | ------------ |
| T1  | Préparer mon projet (dossiers, VS Code, GitHub)     | 2 h    | –             | Mon projet est sur GitHub                                                    | Terminé      |
| T2  | Faire ma veille : chercher et comparer des méthodes | 4 h    | T1            | veille.md compare 2 méthodes ou plus, avec des liens et mon choix            | Terminé      |
| T3  | Écrire le cahier des charges                        | 2 h    | T2            | cahier_des_charges.md est rempli                                             | Terminé      |
| T4  | Faire marcher mon notebook du projet 6              | 1 h    | T1            | "Run All" marche sans erreur                                                 | Terminé      |
| T5  | Noter les problèmes dans les données                | 2 h    | T4            | Les problèmes sont écrits dans le notebook                                   | Terminé      |
| T6  | Revoir mes résultats avec l'IQR                     | 1 h    | T5            | Le nombre d'outliers (36) est noté dans veille.md                            | Terminé      |
| T7  | Tester des questions à l'IA et les noter            | 2 h    | T2            | journal_IA.md rempli (5 essais) avec liens et captures dans docs/captures_IA | Terminé      |
| T8  | Tester Isolation Forest                             | 3 h    | T6, T7        | Le code marche et le tableau s'affiche                                       | Terminé      |
| T9  | Comparer 3 réglages (2 %, 5 %, 8 %) avec l'IQR      | 2 h    | T8            | Je commente le tableau dans "Ce que je retiens"                              | Terminé      |
| T10 | Écrire pourquoi chaque produit est signalé          | 2 h    | T9            | Chaque produit a une raison dans la colonne "raison"                         | Terminé      |
| T11 | Vérifier ma liste de cases à cocher                 | 1 h    | T10           | Toutes les cases du cahier des charges sont cochées                          | Terminé      |
| T12 | Montrer mon travail à mon mentor                    | 1 h    | T11           | J'ai noté ses remarques et je les ai corrigées                               | en cours     |
| T13 | Nettoyer mon notebook                               | 2 h    | T9            | Il est clair, sans cellule vide, et "Run All" marche                         | Terminé      |
| T14 | Créer le fichier requirements.txt                   | 30 min | T13           | Le fichier liste mes librairies                                              | Terminé      |
| T15 | Finir le README                                     | 2 h    | T13           | Il contient résultats, limites et comment lancer le projet                   | Terminé      |
| T16 | Écrire la fiche pour l'équipe                       | 1 h    | T3, T10       | La fiche d'une page est dans docs/                                           | Terminé      |

Où j'en suis : 15 terminées, 1 en cours, 0 à faire.

## 3. Mon planning

Début du projet : 16/11/2026. Date de rendu : 18/12/2026

| Semaine | Dates         | Lots   | Tâches        | Jalon (ce qui doit être fini)                             |
| ------- | ------------- | ------ | ------------- | --------------------------------------------------------- |
| 1       | 16/11 → 23/11 | L1, L2 | T1 à T5, T7   | J1 – 23/11 : veille et cahier des charges terminés        |
| 2       | 24/11 → 30/11 | L3, L4 | T6, T8, T9    | J2 – 30/11 : Isolation Forest testé et comparé à l'IQR    |
| 3       | 01/12 → 07/12 | L5     | T10, T11, T12 | J3 – 07/12 : résultats vérifiés et validés par mon mentor |
| 4       | 08/12 → 14/12 | L6     | T13 à T16     | J4 – 14/12 : notebook propre, README fini, projet rendu   |

## 4. Mes points de contrôle

| Quand      | Ce que je vérifie                                                                  | Qui vérifie          | Preuve                                                            |
| ---------- | ---------------------------------------------------------------------------------- | -------------------- | ----------------------------------------------------------------- |
| J1 – 23/11 | La veille compare au moins 2 options, avec des sources et une décision             | Moi, puis mon mentor | Commit "Jalon 1 : veille et cahier des charges"                   |
| J2 – 30/11 | Le notebook tourne avec "Run All", le tableau IQR / Isolation Forest s'affiche     | Moi                  | Commit "Jalon 2 : Isolation Forest testé"                         |
| J3 – 07/12 | Chaque produit signalé a une raison, les critères d'acceptation sont cochés        | Mon mentor           | Commit "Jalon 3 : résultats validés" + remarques du mentor notées |
| J4 – 14/12 | Tout est propre, le README est complet, un autre utilisateur peut lancer le projet | Moi, puis mon mentor | Commit "Jalon 4 : version finale"                                 |

À chaque jalon, je fais aussi :

- une capture de mon Kanban (dossier docs/captures_kanban) ;
- un enregistrement sur GitHub (git add, git commit, git push).

## 5. Mon tableau Kanban

- Outil : Trello
- Lien : [voir mon tableau Trello](https://trello.com/invite/b/6afeb5078d4fc03b20eafa90/ATTIf8997ad9f5a1cc42a487858d06991f7dAA71F437/mission-1-bottleneck)
- Captures : dossier docs/captures_kanban/

## 6. Mes risques

Voir docs/risques.md

## 7. Remarques de mon mentor

Date : [date de sa réponse]En attente de la réponse de mon mentor

- Remarque : [ce qu'il a dit]
- Ce que j'ai corrigé : []
