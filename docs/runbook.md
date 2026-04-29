# ?? Runbook - Plateforme de Données Movies

Ce document explique comment installer, lancer et vérifier le bon fonctionnement de la plateforme **ELK-Movies-Data-Platform-SAS**.

## ?? Prérequis
* **Docker** & **Docker Desktop** installés (version 20.10+)
* **Git** installé


## ??? Installation et Lancement

    1. **Cloner le projet :**
    ```bash
    git clone https://github.com/Smille999/ELK-Movies-Data-Platform-SAS.git
    cd ELK-Movies-Data-Platform-SAS
    ```

    2. **Démarrer les conteneurs (Elasticsearch, Logstash, Kibana) :**
    ```bash
        docker-compose up -d
        ```

* Laissez tourner 2 à 3 minutes lors du premier lancement.


## ?? Accès aux Services

Service	        URL	                    Usage
Kibana	        http://localhost:5601	Dashboards, Dataviz et console Dev Tools
Elasticsearch	http://localhost:9200	Moteur de recherche et base de données


## ?? Vérification

Pour vérifier que les données sont bien là, ouvrez Kibana, allez dans Dev Tools et lancez :
    ```JSON
    GET /_cat/indices?v

Vous devriez voir l'index movies_clean avec des documents à l'intérieur.


## ?? Maintenance

* Arrêter la plateforme : docker-compose down

* Tout réinitialiser : docker-compose down -v

