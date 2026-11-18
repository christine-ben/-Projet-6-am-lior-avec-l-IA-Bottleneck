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

| Critère                       | A : IQR (actuel)                                                 | B : IQR par groupe                                   | D : Isolation Forest                                     |
| ----------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------- |
| Comment ça marche             | Un prix est anormal s'il sort des bornes calculées avec Q1 et Q3 | Pareil, mais à l'intérieur de chaque type de vin     | L'algorithme cherche les produits qui ont un profil rare |
| Colonnes utilisées            | Le prix seulement                                                | Le prix + le type de produit                         | Prix, prix d'achat, marge, stock, ventes, type           |
| Résultat sur mes données      | [à compléter] outliers                                           | Pas testée                                           | [à compléter] outliers (réglage 5 %)                     |
| Trouve la marge négative ?    | Non, je l'ai trouvée à la main                                   | Pas testée                                           | [à compléter : oui / non]                                |
| Facile à expliquer            | Très facile                                                      | Facile                                               | Plus difficile                                           |
| Temps de calcul               | Immédiat                                                         | Immédiat                                             | Quelques secondes                                        |
| Même résultat à chaque fois ? | Oui                                                              | Oui                                                  | Oui, grâce à random_state=42                             |
| Limites                       | Signale les vins chers même s'ils sont normaux                   | Les petits groupes donnent des résultats peu fiables | Il ne dit pas pourquoi un produit est bizarre            |
| Données personnelles (RGPD)   | Aucune                                                           | Aucune                                               | Aucune                                                   |

## 4. Mes sources

- Documentation officielle d'Isolation Forest (scikit-learn) : https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.IsolationForest.html
- Guide scikit-learn sur la détection d'outliers : https://scikit-learn.org/stable/modules/outlier_detection.html
- Article KDnuggets de Nate Rosidi (mars 2026), 5 méthodes testées sur des vins : https://www.kdnuggets.com/we-used-5-outlier-detection-methods-on-a-real-dataset-they-disagreed-on-96-of-flagged-samples
  https://static.marimo.app/static/outlier-detection-experiment-k3mi
- Mes échanges avec ChatGPT et Claude : voir journal_IA.md

## 5. Ce que j'ai appris pendant ma veille

- Chaque méthode a sa propre idée de ce qui est "anormal". Elles ne trouvent donc pas les mêmes produits.
- Il ne faut jamais supprimer un produit automatiquement : on le signale, puis on vérifie.
- Une méthode simple (IQR) est plus facile à expliquer. Une méthode de machine learning voit plus de choses, mais demande plus de vérifications.

## 6. Ma décision

[à compléter après le test, par exemple :]
Je garde l'IQR, car il est simple à expliquer à l'équipe.
J'ajoute Isolation Forest, car il regarde le prix d'achat et la marge en même temps et repère des produits que l'IQR ne voit pas.
Je mets de côté l'option B pour une prochaine amélioration.
