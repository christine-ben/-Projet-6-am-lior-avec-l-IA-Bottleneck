# Mon cahier des charges

## 1. Le contexte

Bottleneck est un caviste qui vend ses vins sur internet.
Mon analyse est utile à l'équipe qui gère le catalogue et les prix du site.
Elle les aide à décider quels prix corriger (erreurs) et quels prix garder (vins haut de gamme).

## 2. Le problème à résoudre

Comment repérer vite les prix qui sont sûrement des erreurs,
sans signaler par erreur les vins chers mais normaux ?

## 3. Ce que je fais et ce que je ne fais pas

Je fais :

- l'analyse des produits du catalogue (fichiers erp, web et liaison) ;
- avec les colonnes : prix de vente, prix d'achat, stock, ventes, type de produit.

Je ne fais pas :

- je ne change pas les prix moi-même ;
- je n'analyse pas les clients ;
- je n'analyse pas les boutiques physiques.

## 4. Mes contraintes

- Les données ont quelques problèmes : valeurs manquantes, ventes négatives, une marge négative.
- J'ai peu d'informations sur chaque vin (pas de région, pas d'appellation).
- Pas de données personnelles dans les fichiers. Je n'envoie jamais les fichiers à une IA, seulement le nom des colonnes.
- Mes outils : Python, VS Code, Jupyter, pandas, scikit-learn, GitHub.
- Date de rendu :18/12/2026

### 5. Comment je sais que c'est réussi (mes indicateurs)

### Données

- aucun doublon sur product_id ;
- tous les prix sont des nombres positifs.

### Modèle / résultats

- les 2 méthodes (IQR et Isolation Forest) sont comparées dans un tableau, avec 3 réglages (2 %, 5 %, 8 %) ;
- chaque produit à vérifier a une raison écrite dans la colonne "raison" (par exemple "marge négative" ou "vin premium probable"). C'est mon critère d'interprétabilité : on comprend pourquoi un produit est signalé ;
- la marge négative est bien repérée par les deux méthodes.

### Fonctionnement

- le notebook marche du début à la fin sans erreur ;
- il donne les mêmes résultats à chaque fois (random_state=42).

### Ce que je ne mesure pas, et pourquoi

- Je ne calcule pas de précision ni de rappel : je n'ai pas de liste de vraies erreurs pour comparer.
- Je ne fais pas de mesures avancées (Jaccard, score d'anomalie, kappa). Mon projet est simple et je dois pouvoir expliquer chaque chiffre à l'équipe du caviste.
- Piste pour plus tard : faire relire la liste par le caviste, ce qui permettrait de calculer une vraie précision.

## 6. Ma liste de vérification finale

- [x] Le notebook se lance avec "Run All" sans erreur
- [x] Le tableau qui compare les 2 méthodes est présent
- [x] La marge négative est bien repérée (oui produit 6324)
- [x] Chaque produit à vérifier a une raison dans la colonne "raison"
- [x] Aucun produit n'est supprimé : les produits suspects sont signalés dans la colonne "a_verifier" (61 produits), avec leur raison dans la colonne "raison"
- [x] Chaque graphique a un titre, des noms d'axes et une phrase d'explication
- [x] Aucune donnée n'a été envoyée à une IA

## 7. Mon mini-plan de formation

Pour que l'équipe sache utiliser mon travail, j'ai pensé à 2 idées :

| Idée                            | Ce que je fais                                       | Point fort                      | Point faible                                       |
| ------------------------------- | ---------------------------------------------------- | ------------------------------- | -------------------------------------------------- |
| A : une démonstration de 30 min | Je montre le notebook à l'équipe                     | On peut poser des questions     | Il faut que tout le monde soit libre en même temps |
| B : une fiche d'une page        | J'explique comment lire la liste des prix à vérifier | On peut la relire quand on veut | Pas de questions en direct                         |

Mon choix : la fiche (B), car c'est le plus simple et l'équipe peut la garder.
Ce que la fiche doit faire comprendre :

1. Un prix signalé n'est pas forcément une erreur.
2. Avant de corriger un prix, il faut regarder la marge et le type de vin.

La fiche est écrite : docs/fiche_equipe.md
