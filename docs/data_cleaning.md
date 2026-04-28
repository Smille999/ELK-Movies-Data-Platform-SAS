# ?? Nettoyage des Données (Logstash Pipeline)

Ce document résume les étapes de transformation et de nettoyage (Feature 3) effectuées sur les données brutes avant leur indexation.

## ?? Logique du Pipeline Logstash

Le fichier `logstash.conf` agit comme un filtre pour garantir que seules des données de qualité arrivent dans Elasticsearch.

### 1. Filtrage et Suppression
* **Sécurité :** Les lignes du CSV ne contenant pas de titre ou de date de sortie ont été supprimées (`drop`) pour éviter d'avoir des "trous" dans nos statistiques.

### 2. Normalisation des Types (`mutate`)
Les données provenant d'un CSV sont lues par défaut comme du texte. Nous les avons converties pour permettre les calculs :
* `budget` : texte ?? **float**
* `vote_average` : texte ?? **float**
* `vote_count` : texte ?? **integer**

### 3. Gestion du Temps (`date filter`)
* Le champ `release_date` a été transformé au format standard **ISO8601**. Cela permet à Kibana de générer des graphiques d'évolution temporelle précis.

### 4. Nettoyage des Colonnes
* Les colonnes jugées inutiles pour l'analyse finale (ex: IDs internes ou URLs de posters) ont été retirées du flux de données pour optimiser la taille de l'index. 