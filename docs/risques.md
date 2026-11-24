# Les risques de mon projet

| Risque                              | Ce qui peut se passer                                                                    | Chance que ça arrive     | Gravité | Ce que je fais pour l'éviter                                                                                                              |
| ----------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Fuite de données                    | J'envoie les fichiers de l'entreprise à une IA                                           | Faible                   | Grave   | J'envoie seulement le nom des colonnes, jamais les fichiers                                                                               |
| Erreur de l'IA                      | Le code donné par l'IA est faux ou incomplet                                             | Moyenne                  | Moyenne | Je teste chaque code et je vérifie les résultats. Ça m'est arrivé : le code de ChatGPT était incomplet                                    |
| Faux suspects                       | Des vins chers mais normaux sont signalés comme des erreurs                              | Forte                    | Moyenne | Je regarde la marge et le type de vin avant de conclure. Je ne supprime rien                                                              |
| Résultats qui changent              | Isolation Forest donne un résultat différent à chaque lancement                          | Forte si je ne fais rien | Faible  | Je fixe random_state=42 pour avoir toujours le même résultat                                                                              |
| Données de mauvaise qualité         | Ventes négatives, valeurs manquantes                                                     | Moyenne                  | Moyenne | Je les repère et je les note dans les limites                                                                                             |
| Retard                              | Je ne finis pas à temps                                                                  | Moyenne                  | Grave   | Je fais d'abord ce qui est obligatoire, puis les bonus. Résultat : toutes les tâches ont été finies avant la date de rendu du 18/12/2026. |
| Perte de mon travail                | Mon ordinateur plante ou j'efface un fichier                                             | Faible                   | Grave   | J'enregistre sur GitHub après chaque étape                                                                                                |
| Pas de vraies erreurs pour vérifier | Je ne peux pas prouver que mes alertes sont justes                                       | Forte                    | Moyenne | Je n'écris pas "précision" ni "exactitude". Je signale des produits à vérifier et j'explique chaque alerte avec la colonne raison         |
| Trop d'idées de l'IA                | L'IA propose des méthodes ou des métriques trop compliquées que je ne sais pas expliquer | Moyenne                  | Faible  | Je garde seulement ce que je sais expliquer, et je note ce que j'écarte dans journal_IA.md                                                |

## Bilan des risques (24/11/2026)

- Aucune donnée n'a été envoyée à l'IA.
- Le code de ChatGPT était incomplet (risque arrivé) : je l'ai complété et testé.
- Les faux suspects étaient bien présents : 19 grands vins signalés seulement par l'IQR. Je ne supprime rien, je signale seulement.
- Le résultat est reproductible (random_state=42).
