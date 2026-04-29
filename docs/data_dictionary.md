# ?? Dictionnaire de Données (Mapping)

Notre base de données Elasticsearch utilise un index nommé **`movies_clean`**. Un "Mapping" explicite a été créé (Feature 4) pour forcer le typage des données et optimiser la recherche ainsi que les visualisations.

## ??? Structure des champs

| Champ         | Type Elasticsearch | Description & Usage                                      |
| :---          | :---               |  :---                                                    |
| `title`       | `text`             | Titre du film. Utilise l'analyzer custom **edge_ngram**. |
| `genres`      | `keyword`          | Genres du film (Action, Drama...).                       |
| `release_date`| `date`             | Date de sortie officielle.                               |
| `budget`      | `float`            | Budget de production.                                    |
| `vote_average`| `float`            | Note moyenne des spectateurs.                            |
| `vote_count`  | `integer`          | Nombre total de votes.                                   |

## ?? Focus Technique : L'Analyzer edge_ngram

Le champ `title` a été configuré spécifiquement avec un filtre `edge_ngram` (min_gram: 1, max_gram: 20). 

**Pourquoi ?** 

Cela permet la fonctionnalité d'**autocomplétion** (recherche partielle). 
Si un utilisateur tape "Bat", Elasticsearch trouve instantanément "Batman" car le mot a été découpé et indexé lettre par lettre lors de l'ingestion, rendant la recherche extrêmement rapide.