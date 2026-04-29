# Planning Poker - Projet ELK Movies Data Platform

**Date de la session :** [10/04/2026]

**Membres de l'équipe :** [Sonia], [Arnold], [Sofiane]

**Échelle d'estimation utilisée :** Suite de Fibonacci (1, 2, 3, 5, 8, 13)

---

## Backlog et Estimations

| ID   | Feature   | Estimations initiales | Estimations finales  | Hypothèses / Remarques | Assigné à |

| *F1* | Bootstrap |  3,5,3                | 3                    |  Installation standard |Sofiane        |



| *F2* | Ingestion brute (Lecture CSV, indexation movies_raw)     | 8,3,3      | 3                 |    On suppose que le CSV n'a pas de lignes corrompues.                    |       Sonia    |



| *F3* | Nettoyage & normalisation (Conversions, anomalies, listes)                    | 8,8,8                 | 8                 |    Risque élevé : formatage des dates et éclatement des genres en listes.                    |    Arnold       |



| *F4* | Mapping & qualité data (Mapping explicite, analyzer, indexation movies_clean) | 8,8,5                 | 8                 |    Nécessite un analyzer "edge_ngram" pour la recherche partielle.                    |    Sofiane       |


| *F5* | Requêtes analytiques (12 DSL, 5 bool, cas métier)    | 8,3,5      | 5                 |    Doit couvrir tous les types de filtres (bool, range, match).                    |    Arnold (All Team)       |



| *F6* | Dataviz Kibana (6-8 visualisations, 1 dashboard structuré)                    | 5,2,3                 | 3                 |    On part sur un dashboard unique regroupant tous les KPI.                    |      Sonia     |



| *F7* | Documentation finale (Runbook, data dict, doc nettoyage/projet)               | 5,3,2                 | 3                 |    À réaliser au fil de l'eau pour ne rien oublier.                    |    All Team       |



| *F8* | Moteur de recherche (Mini moteur, full-text, 1 filtre minimum)                | 8,8,8                 | 8                 |    Utilisation probable d'une mini API Python ou Node.js.                    | All Team          |



## Règles de contribution de l'équipe

Afin de valider l'implication individuelle, chaque membre de l'équipe s'engage à respecter les règles suivantes

1.Être responsable du développement d'au moins 1 feature du tableau ci-dessus

2.Ouvrir au moins 1 Pull Request (PR) pour soumettre son travail
