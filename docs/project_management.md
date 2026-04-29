# ?? Gestion de Projet & Méthodologie

Ce document détaille l'organisation de l'équipe et la méthodologie de travail adoptée pour le projet ELK Movies.

## ?? Répartition des Rôles

L'équipe a travaillé de manière collaborative avec une répartition claire des responsabilités :
* **Sofiane :** Lead Architecture Docker, Configuration du Mapping (Analyzers) et Documentation.
* **Sonia :** Ingestion des données via Logstash et création du Dashboard Kibana.
* **Arnold :** Nettoyage des données (Logstash filters) et requêtes analytiques DSL.

## ?? Méthodologie : Planning Poker

Pour estimer la complexité de nos tâches, nous avons utilisé la méthode du **Planning Poker** (basée sur la suite de Fibonacci). Cela nous a permis d'aligner notre compréhension technique de chaque feature avant de commencer le développement.

> *Note : Le détail de nos sessions de vote est disponible dans le fichier [planning_poker.md](planning_poker.md).*

## ??? Architecture du Projet

Le flux de données respecte l'architecture suivante :
1. **Source :** Fichier CSV (`movies.csv`).
2. **Transport & Nettoyage :** Logstash (Pipeline).
3. **Stockage & Indexation :** Elasticsearch (avec Mapping optimisé).
4. **Visualisation :** Kibana (Dashboards).