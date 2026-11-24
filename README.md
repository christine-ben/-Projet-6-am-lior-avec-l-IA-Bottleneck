# Projet 6 amélioré avec l'IA – Bottleneck

## Le but du projet

Aider l'équipe du caviste Bottleneck à repérer les prix suspects de son catalogue en ligne,
sans confondre les erreurs de prix avec les vins haut de gamme.

## Ce que j'ai amélioré

- Avant : je trouvais les prix anormaux avec l'IQR, en regardant seulement le prix. Je vérifiais ensuite la marge à la main.
- Après : j'ai ajouté Isolation Forest, une méthode de machine learning qui regarde plusieurs colonnes en même temps (prix, prix d'achat, marge, stock, ventes, type).
- J'ai aussi ajouté une colonne "raison" qui explique pourquoi chaque produit est signalé.
- Comment j'ai choisi : voir docs/veille.md

## Mes résultats

- L'IQR trouve 36 prix anormaux.
- Isolation Forest signale 17, 42 ou 66 produits selon le réglage (2 %, 5 % ou 8 %). Ce nombre est fixé par le réglage, ce n'est pas un résultat en soi : ce qui compte, c'est quels produits sont signalés.
- Avec le réglage 5 % : 17 produits sont trouvés par les deux méthodes, 19 seulement par l'IQR et 25 seulement par Isolation Forest.
- La marge négative (produit 6324 : vendu 92 €, acheté 99 €) est trouvée par Isolation Forest avec les 3 réglages testés.
- Les 19 produits signalés seulement par l'IQR sont des grands vins chers à marge normale : ce sont des faux suspects.
- Isolation Forest repère aussi des problèmes de stock (stock très élevé, aucune vente).
- Le même vin apparaît sous 2 numéros (4594 et 6324) avec des ventes négatives : doublon possible à vérifier.
- Au total, 61 produits sont à vérifier. Chacun a une raison écrite dans la colonne "raison".
- Aucun produit n'est supprimé : je les signale seulement.

## Les limites

- Sans liste de vraies erreurs, je ne peux pas calculer de précision ni de rappel : je vérifie seulement que chaque alerte est expliquée (colonne "raison"), pas qu'elle est exacte.
- Le nombre de produits signalés par Isolation Forest est fixé par mon réglage (contamination), ce n'est pas un résultat en soi.
- Un produit signalé est un candidat à vérifier, pas une erreur confirmée : un grand cru rare peut être anormal et légitime.
- Isolation Forest ne dit pas pourquoi un produit est suspect : j'ai ajouté des règles simples pour écrire une raison, mais leurs seuils sont des choix personnels.
- J'ai peu d'informations sur chaque vin (pas de région, pas d'appellation).
- Certaines données sont à corriger (ventes négatives).
- Je n'ai pas mesuré la stabilité des résultats : ce serait une amélioration possible.

## Comment lancer le projet

1. Installer Anaconda (Python).
2. Ouvrir le dossier du projet dans VS Code.
3. Dans le terminal, taper : pip install -r requirements.txt
4. Ouvrir notebooks/P6_Bottleneck_amelioration.ipynb.
5. Choisir le kernel Python d'Anaconda (bouton "Select Kernel").
6. Cliquer sur "Run All".

## Comment le projet est rangé

- data/ : les fichiers Excel (erp, web, liaison)
- notebooks/ : le notebook d'origine et le notebook amélioré
- docs/ : ma veille, mon cahier des charges, mes risques, mon organisation
- journal_IA.md : tout ce que j'ai demandé à l'IA et ce que j'ai décidé

## Comment j'ai organisé mon travail

- Tableau Kanban (Trello) : [voir mon tableau Trello](https://trello.com/invite/b/6afeb5078d4fc03b20eafa90/ATTIf8997ad9f5a1cc42a487858d06991f7dAA71F437/mission-1-bottleneck)
- Captures du Kanban : dossier docs/captures_kanban/
- Liste des tâches, planning et points de contrôle : docs/organisation.md
- Risques : docs/risques.md

## Ce que je ferais avec plus de temps

- Tester l'IQR par type de vin (option B de ma veille).
- Ajouter des informations sur les vins (région, appellation) pour une analyse plus précise.
- Faire relire la liste des produits à vérifier par le caviste, pour calculer une vraie précision.
