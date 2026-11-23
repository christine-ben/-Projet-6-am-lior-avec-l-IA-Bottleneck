# Mon journal des essais avec l'IA

Ici, je garde la trace de tout ce que j'ai demandé à l'IA, de ce qu'elle m'a répondu et de ce que j'ai décidé.
Ma règle : je n'envoie jamais mes fichiers de données à l'IA, seulement le nom des colonnes.

## Mes essais

| N°  | Date       | IA utilisée                     | Ce que j'ai demandé                                                                                                                                          | Type de demande     | Ce que l'IA m'a répondu                                                                                                                                                                                                                                                                                    | Ce que je garde et pourquoi                                                                                                                                                                                                                  |
| --- | ---------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 18/11/2026 | ChatGPT                         | Comment améliorer ma détection des prix anormaux ? Propose 3 méthodes avec avantages, limites et difficulté                                                  | Ouverte (découvrir) | 3 méthodes : IQR par groupe de vins, régression du prix attendu, Isolation Forest. Conseil : regarder aussi la marge, le stock et les ventes, et ne jamais supprimer un produit automatiquement                                                                                                            | Je garde l'idée de regarder plusieurs colonnes en même temps. Je retiens l'IQR par groupe et Isolation Forest. Je mets de côté la régression, car j'ai trop peu de colonnes pour bien deviner un prix                                        |
| 2   | 18/11/2026 | ChatGPT                         | Quelle méthode pour aller plus loin que mon IQR ? Isolation Forest est-il adapté ? Donne un code pour comparer                                               | Précise (choisir)   | Conseille Isolation Forest avec plusieurs colonnes, mais en plus de l'IQR, pas à sa place. Limite : il ne dit pas pourquoi un produit est bizarre. Conseille de tester 3 réglages (2 %, 5 %, 8 %)                                                                                                          | Je garde la méthode et les conseils. Mais le code était incomplet (le début manquait), je ne pouvais pas l'utiliser tel quel                                                                                                                 |
| 3   | 19/11/2026 | Claude                          | Le code de ChatGPT est incomplet : aide-moi à le compléter et à l'adapter à mon notebook                                                                     | Correction          | Code complet avec des commentaires, adapté à mes variables, avec un tableau qui compare les 3 réglages et une colonne a_verifier                                                                                                                                                                           | Je garde ce code car il marche avec mes données. Je l'ai relu, compris et testé avant de le garder                                                                                                                                           |
| 4   | 23/11/2026 | Claude (autre conversation)     | Quelles métriques utiliser quand je n'ai pas de liste de vraies erreurs ? Comment mesurer la stabilité et l'explication des résultats ? Donne du code Python | Précise (comparer)  | Plusieurs idées : taux d'alertes, recouvrement entre les 2 méthodes (Jaccard), score d'anomalie, règle métier, relecture d'un échantillon. Rappelle qu'on mesure la cohérence des résultats, pas leur exactitude. Prévient que le nombre d'alertes d'Isolation Forest vient de mon réglage (contamination) | Je n'ai pas gardé ces métriques avancées : sans liste de vraies erreurs, elles ne prouvent pas que mes résultats sont justes, et je ne pourrais pas les expliquer simplement à l'équipe. Je garde ma colonne raison                          |
| 5   | 23/11/2026 | Claude (conversation du projet) | Même question, avec du code adapté à mes variables                                                                                                           | Précise (coder)     | Le code proposé ne gérait pas les cases vides et utilisait un modèle différent du mien. J'ai aussi reçu des conseils pour choisir quoi garder                                                                                                                                                              | Je garde une seule idée : l'interprétabilité, avec ma colonne raison qui explique pourquoi chaque produit est signalé. Je ne mets pas le reste, car c'est trop compliqué à expliquer pour un résultat qui ne prouve rien sans vraies erreurs |

Au départ, j'avais prévu un autre prompt pour demander une comparaison IQR / Isolation Forest avec du code.
Je ne l'ai pas envoyé : le prompt 2 m'avait déjà donné cette comparaison et ce code.

## Ce que j'ai changé dans le code de l'IA

Le code de ChatGPT ne marchait pas tel quel :

- le début manquait (les imports, la préparation des données, la liste des colonnes) ;
- les noms des variables n'étaient pas ceux de mon notebook.

Ce que j'ai changé (avec l'aide de Claude, essai n°3) :

- j'ai ajouté les imports de scikit-learn ;
- j'ai utilisé mon tableau df_final et ma colonne outlier_iqr ;
- j'ai calculé la marge et le taux de marge ;
- j'ai testé 3 réglages (2 %, 5 %, 8 %) comme ChatGPT le conseillait ;
- j'ai ajouté une colonne a_verifier : je signale les produits, je ne les supprime pas.

Pour l'essai 4, le code proposé ne gérait pas les cases vides et utilisait un modèle sans le type de produit. Je ne l'ai pas utilisé.

Le code final est dans notebooks/P6_Bottleneck_amelioration.ipynb, partie 4.3.

## Ce que j'ai appris sur les prompts

- Une question ouverte m'aide à découvrir des méthodes que je ne connaissais pas.
- Une question précise, avec mon contexte et le nom de mes colonnes, me donne une réponse que je peux utiliser.
- L'IA peut se tromper ou donner un code incomplet : je teste et je vérifie toujours.
- L'IA propose parfois trop d'idées : je choisis celles que je sais expliquer et je garde la raison de mon choix.

## Liens vers mes conversations

- ChatGPT, essais 1 et 2 : [voir la conversation](https://chatgpt.com/share/6afd74dd-abd8-83ed-9138-e69d2f75022b)
- Claude, essai 4 (métriques) : [voir la conversation](https://claude.ai/share/e16e61ca-9a11-4d00-ac98-f27eb2cac328)
- Captures d'écran : dossier docs/captures_IA/ (essai4_metriques_prompt.png et essai4_metriques_reponse.png)
