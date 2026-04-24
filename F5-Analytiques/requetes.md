
# Livrable F5 : Requêtes Analytiques DSL - Arnold

Ce document regroupe les 12 requêtes effectuées sur l'index `movies_clean`.

---

## PARTIE 1 : 5 Requêtes Booléennes (Filtres complexes)

### Q1 : Les Blockbusters rentables
**Scénario :** Identifier les films à gros budget (> 100M) très bien notés (> 7).
```json
GET /movies_clean/_search
{
  "query": {
    "bool": {
      "filter": [
        { "range": { "budget": { "gte": 100000000 } } },
        { "range": { "vote_average": { "gte": 7 } } }
      ]
    }
  }
}


Q2 : La niche Francophone (Sans drame)
Scénario : Films en français qui ne sont pas du genre "Drama".

JSON
GET /movies_clean/_search
{
  "query": {
    "bool": {
      "must": [{ "term": { "original_language": "fr" } }],
      "must_not": [{ "match": { "genres": "Drama" } }]
    }
  }
}

Q3 : Classiques d'animation des années 90
Scénario : Genre Animation, sortis entre 1990 et 1999, avec une forte popularité (plus de 1000 votes).

GET /movies_clean/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "genres": "Animation" } }
      ],
      "filter": [
        { "range": { "release_date": { "gte": "1990-01-01", "lte": "1999-12-31" } } },
        { "range": { "vote_count": { "gt": 1000 } } }
      ]
    }
  }
}

Q4 : Recherche thématique "Espace" (Pertinence)
Scénario : Films dont le résumé contient "Space" ou "Galaxy". Le score de pertinence augmente si les deux sont présents.

GET /movies_clean/_search
{
  "query": {
    "bool": {
      "should": [
        { "match": { "overview": "Space" } },
        { "match": { "overview": "Galaxy" } }
      ]
    }
  }
}

Q5 : Action à petit budget
Scénario : Films du genre "Action" ayant coûté moins de 5 millions à produire.

GET /movies_clean/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "genres": "Action" } }
      ],
      "filter": [
        { "range": { "budget": { "lt": 5000000 } } }
      ]
    }
  }
}

PARTIE 2 : 7 Agrégations (Analyses statistiques)

Q6 : Statistiques budgétaires globales
Scénario : Analyse statistique (Moyenne, Min, Max, Somme) des budgets.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "stats_budget": {
      "stats": {
        "field": "budget"
      }
    }
  }
}

Q7 : Top 10 des Genres les plus fréquents
Scénario : Identifier les 10 genres les plus représentés.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "top_genres": {
      "terms": {
        "field": "genres.keyword",
        "size": 10
      }
    }
  }
}

Q8 : Répartition par langue (Top 5)
Scénario : Visualiser la diversité linguistique via les 5 langues principales.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "langues_principales": {
      "terms": {
        "field": "original_language.keyword",
        "size": 5
      }
    }
  }
}

Q9 : Histogramme annuel des sorties
Scénario : Évolution du nombre de films produits par année.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "films_par_an": {
      "date_histogram": {
        "field": "release_date",
        "calendar_interval": "year"
      }
    }
  }
}

Q10 : Durée moyenne (Runtime) par Genre
Scénario : Comparaison de la durée moyenne des films par genre.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "genres_et_duree": {
      "terms": {
        "field": "genres.keyword"
      },
      "aggs": {
        "duree_moyenne": {
          "avg": {
            "field": "runtime"
          }
        }
      }
    }
  }
}

Q11 : Revenu total cumulé
Scénario : Somme totale des revenus générés.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "chiffre_affaire_total": {
      "sum": {
        "field": "revenue"
      }
    }
  }
}

Q12 : Diversité du Casting (Cardinalité)
Scénario : Nombre d'artistes uniques dans l'index.

GET /movies_clean/_search
{
  "size": 0,
  "aggs": {
    "nombre_artistes_uniques": {
      "cardinality": {
        "field": "credits.keyword"
      }
    }
  }
}