# Projet 6 amélioré avec l'IA – Bottleneck

## Le but du projet

Aider l'équipe du caviste Bottleneck à repérer les prix suspects de son catalogue en ligne,
sans confondre les erreurs de prix avec les vins haut de gamme.

## Ce que j'ai amélioré

- Avant : je trouvais les prix anormaux avec l'IQR, en regardant seulement le prix. Je vérifiais ensuite la marge à la main.
- Après : j'ai ajouté Isolation Forest, une méthode de machine learning qui regarde plusieurs colonnes en même temps (prix, prix d'achat, marge, stock, ventes, type).
- Comment j'ai choisi : voir docs/veille.md

## Mes résultats

[à compléter à la fin,:]

- L'IQR trouve [X] prix anormaux, Isolation Forest en trouve [Y].
- [Z] produits sont trouvés par les deux méthodes : ce sont les premiers à vérifier.
- La marge négative [est / n'est pas] trouvée automatiquement par Isolation Forest.

## Les limites

- Isolation Forest ne dit pas pourquoi un produit est suspect : il faut toujours vérifier.
- J'ai peu d'informations sur chaque vin (pas de région, pas d'appellation).
- Certaines données sont à corriger (ventes négatives).

## Comment lancer le projet

1. Installer Anaconda (Python).
2. Ouvrir le dossier du projet dans VS Code.
3. Ouvrir notebooks/P6_Bottleneck_amelioration.ipynb.
4. Choisir le kernel Python d'Anaconda (bouton "Select Kernel").
5. Cliquer sur "Run All".

## Comment le projet est rangé

- data/ : les fichiers Excel (erp, web, liaison)
- notebooks/ : le notebook d'origine et le notebook amélioré
- docs/ : ma veille, mon cahier des charges, mes risques
- journal_IA.md : tout ce que j'ai demandé à l'IA et ce que j'ai décidé

## Comment j'ai organisé mon travail

- Kanban et planning : [lien à ajouter à l'étape 3]
- Risques : docs/risques.md

## Ce que je ferais avec plus de temps

- Tester l'IQR par type de vin (option B de ma veille).
- Ajouter des informations sur les vins (région, appellation) pour une analyse plus précise.
