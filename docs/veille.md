# Ma veille : mieux détecter les prix anormaux

## 1. Mon besoin

Dans mon projet 6, j'ai analysé le catalogue du caviste Bottleneck.
Pour trouver les prix anormaux (les "outliers"), j'ai utilisé le z-score et l'IQR.
Ces méthodes regardent seulement le prix de vente.

Le problème : un vin très cher n'est pas forcément une erreur. C'est peut-être un vin haut de gamme.
J'ai dû vérifier à la main, avec la marge, si chaque prix était une erreur ou non.

Mon besoin : trouver une méthode qui regarde plusieurs informations en même temps
(prix de vente, prix d'achat, marge, stock, ventes, type de produit),
pour repérer plus vite les vrais prix suspects.

## 2. Les options que j'ai étudiées

- Option A : l'IQR sur tout le catalogue (ce que j'ai déjà fait dans mon projet 6).
- Option B : l'IQR par groupe de vins (méthode 1 proposée par ChatGPT).
- Option C : la régression du prix attendu (méthode 2 proposée par ChatGPT). Je l'écarte : j'ai trop peu de colonnes pour bien deviner le prix d'un vin.
- Option D : Isolation Forest (méthode 3 proposée par ChatGPT), un algorithme de machine learning qui regarde plusieurs colonnes à la fois.

## 3. Mon tableau de comparaison

| Critère                                 | A : IQR (actuel)                                                                       | B : IQR par groupe                                        | D : Isolation Forest                                                                   |
| --------------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------- | --- | ------ |
| Comment ça marche                       | Un prix est anormal s'il sort des bornes calculées avec Q1 et Q3                       | Pareil, mais à l'intérieur de chaque type de vin          | L'algorithme cherche les produits qui ont un profil rare                               |
| Colonnes utilisées                      | Le prix seulement                                                                      | Le prix + le type de produit                              | Prix, prix d'achat, marge, stock, ventes, type                                         |
| Qualité (résultat sur mes données)      | 36 outliers                                                                            | Pas testée                                                | 17 (réglage 2 %), 42 (5 %), 66 (8 %)                                                   |
| Trouve la marge négative ?              | Le produit est dans la liste, mais l'IQR ne dit pas que sa marge est négative          | Pas testée                                                | Oui, avec les 3 réglages                                                               |
| Faux suspects                           | Beaucoup : 19 grands vins signalés seulement parce qu'ils sont chers                   | Pas testée                                                | Moins sur les prix, mais il signale aussi des problèmes de stock                       |
| Facile à expliquer                      | Très facile                                                                            | Facile                                                    | Plus difficile                                                                         |
| Temps de calcul                         | Immédiat                                                                               | Immédiat                                                  | Quelques secondes                                                                      |
| Même résultat à chaque fois ?           | Oui                                                                                    | Oui                                                       | Oui, grâce à random_state=42                                                           |
| Limites                                 | Signale les vins chers même s'ils sont normaux                                         | Les petits groupes donnent des résultats peu fiables      | Il ne dit pas pourquoi un produit est bizarre                                          |
| Données personnelles (RGPD)             | Aucune                                                                                 | Aucune                                                    |
| Biais (ce qui peut fausser le résultat) | Regarde un seul prix : un vin cher est signalé même s'il est normal (19 faux suspects) | Dépend du type de vin ; peu fiable si le groupe est petit | Dépend des colonnes choisies et du réglage (17, 42 ou 66 produits selon 2 %, 5 %, 8 %) |
| Facile à maintenir                      | Très facile : quelques lignes de code                                                  | Facile                                                    | Moyen : il faut la librairie scikit-learn et bien choisir le réglage                   |     | Aucune |

## 4. Mes sources

- Documentation officielle d'Isolation Forest (scikit-learn) : https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.IsolationForest.html
- Guide scikit-learn sur la détection d'outliers : https://scikit-learn.org/stable/modules/outlier_detection.html
- Article KDnuggets de Nate Rosidi (mars 2026), 5 méthodes testées sur des vins : https://www.kdnuggets.com/we-used-5-outlier-detection-methods-on-a-real-dataset-they-disagreed-on-96-of-flagged-samples
- Expérience de détection d'outliers (marimo) : https://static.marimo.app/static/outlier-detection-experiment-k3mi
- Mes échanges avec ChatGPT et Claude : voir journal_IA.md

## 5. Ce que j'ai appris

- Chaque méthode a sa propre idée de ce qui est "anormal". Elles ne trouvent pas les mêmes produits : c'est aussi ce que dit l'article KDnuggets, et c'est ce que j'ai observé (17 produits en commun sur 36 et 42).
- L'IQR repère les vins chers. Isolation Forest repère les profils incohérents (marge négative, ventes négatives, stock qui dort).
- Il ne faut jamais supprimer un produit automatiquement : on le signale, puis on vérifie.

## 6. Ma décision

Je garde l'IQR, car il est simple à expliquer à l'équipe.
J'ajoute Isolation Forest (réglage 5 %), car il trouve la marge négative avec tous les réglages et il évite de signaler des grands vins juste parce qu'ils sont chers.
J'ajoute une colonne "raison" pour expliquer chaque alerte, car Isolation Forest ne le fait pas.
Je garde l'option B (IQR par groupe) pour une prochaine amélioration.

## 7. Rappel : ce que l'IQR avait trouvé

- Q1 = 14,50 € (25 % des produits coûtent moins cher que ça)
- Q3 = 42,00 € (75 % des produits coûtent moins cher que ça)
- IQR = Q3 − Q1 = 27,50 €
- Limites calculées : de −26,75 € à 83,25 €
- Résultat : 36 prix anormaux. Ils sont tous au-dessus de 83,25 €, car la limite basse est négative et aucun prix ne peut être aussi bas.
- Le produit le plus cher du catalogue coûte 225 €.
- Pour comparaison, le z-score donnait une moyenne de 32,23 € et un écart-type de 26,65 €. Sa limite haute (moyenne + 3 écarts-types) était d'environ 112 €.
- Limite de la méthode : l'IQR regarde seulement le prix. Il signale donc aussi des vins chers qui sont normaux (grands crus avec une marge normale), et il ne dit pas si un produit a une marge négative.
