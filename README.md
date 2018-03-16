# Projet Data US

## Description

Le projet consiste à afficher sur une carte les données des différentes populations par états des états-unis.

## Insights
- quels sont les facteurs de risque les + importants par état ?
- quelle ethnie est la plus représentée par état ?
- quel état à une population susceptible d’aller le + aux urgences ?
- quelles sont les ethnies les plus distribuées et avec le plus de risques ?
- quelles sont les typologies de personnes en surpoids ? 
- quel est leur style de vie?

## Valeur ajoutée
Déterminer le profil type des populations par état des Etats-Unis afin de :
- mieux cibler les publicités
- mieux gérer les facteurs de risque par état

## Target
- gouvernement
- publicitaires
- commerces
- services publics

# Pipeline big data
## Architecture
### Collecte
https://www.healthdata.gov/dataset/community-health-status-indicators-chsi-combat-obesity-heart-disease-and-cancer/resource 

- open data donc pas de data compliance ni RGPD 
- pas de web scrapping nécessaire
- Transformation des fichiers CSV en 1 fichier JSON grâce à un script 
> but : écrire 1 seul fichier json qui rassemble toutes les données des fichiers csv avec en première clé, le nom de l’état US

### Intégration
- Pas de nettoyage des données ni d’anonymisation à effectuer car open data
- Utilisation de Kafka plutôt que de Flume car https://blog.octo.com/introduction-a-flume-ng/ 
- pas d’utilisation de Swagger UI car on n’utilise pas une API web dans notre projet
- écrire un programme python ou scala (ou java comme en cours) pour envoyer les données JSON vers MongoDB grâce à Kafka

> ex: modifier la boucle dans CarController pour que le script aille lire chaque ligne de notre fichier csv ou json pour pouvoir l’envoyer à MongoDB via le consumer Kafka
 
### Stockage
- quelle est la structure de ces documents? JSON, 1 enregistrement = 1 ligne csv
- quelles sont les contraintes qui portent sur le contenu des documents?

#### Si les données sont semi-structurées, utiliser : 
##### Cassandra (fichiers json ou xml)
- très proche du modèle SGBD, Cassandra permet de vérifier le type de donnée inséré dans une table et de garantir la véracité des données
- utilise la clé paire-valeur (colonne) et les documents (lignes) = structure atomique de représentation des informations semi-structurées
- utilise les index grâce aux identifiants uniques associés à une paire clé-valeur
- permet de tracer l’historique des données
- inconvénient : le modèle est figé donc les données ne sont pas réutilisables ou scalables 

##### MongoDB (fichiers json)
- base centralisée pour le stockage de documents JSON
- capacité à passer en mode distribué pour répartir le stockage et les traitements
- pas de schéma relationnel donc possibilité d’insérer des docs json
- inconvénient : contrôle des données du côté application et non lors de leur insertion

##### Hive (fichiers csv)
- modèle de données relationnelles basé sur les données contenues dans HDFS 
- le métastore stocke le modèle de BDD (définition des tables + métadonnées) 
- inférence possible des types de données
- utilisation de HiveQL, proche de SQL pour faire des requêtes

##### Pig
- langage scripting pour exécution des jobs MapReduce

#### Si les données sont non structurées, utiliser :
##### HBase 
- si données avec beaucoup de colonnes dont une majorité de cellules sont vides
- utilisation des données directement dans HDFS sans passer par des tâches
- capacité à gérer beaucoup de données (de l’ordre du Po)
- forte tolérance aux pannes

### Analyse
- Hive
- MongoDB 
 
### Visualisation, Restitution
- carte dynamique des US
 
## Cahier des charges
### Installation des composants
- Installer Kafka sur AWS
- Installer MongoDB sur AWS

### Gestion de projet
- Créer un repository Git pour le projet

### Requêtes et visualisation
- Envoyer les fichiers csv sur AWS au cas où
- Loader les fichiers csv dans Hive au cas où

# Sources de données
https://www.healthdata.gov/dataset/community-health-status-indicators-chsi-combat-obesity-heart-disease-and-cancer/resource  

**DATA_ELEMENT_DESCRIPTION.csv** defines each data element and indicates where its description is found in Data Sources, Definitions, and Notes.
=> 5 colonnes, 579 lignes

**DEFINED_DATA_VALUE.csv** defines the meaning of specific values (such as missing or suppressed data).  
=> 2 colonnes, 13 lignes

**HEALTHY_PEOPLE_2010.csv** identifies the Healthy People 2010 Targets and the U.S. Percentages or Rates.
=> 4 colonnes, 23 lignes

**DEMOGRAPHICS.csv** identifies the data elements and values in the Demographics indicator domain.
=> 44 colonnes, 3142 lignes

**LEADING_CAUSES_OF_DEATH.csv** identifies the data elements and values in the Leading Causes of Death indicator domain.
=> environ 220 colonnes, 3142 lignes

**SUMMARY_MEASURES_OF_HEALTH.csv** identifies the data elements and values in the Summary Measures of Health indicator domain.

**MEASURES_OF_BIRTH_AND_DEATH.csv** identifies the data elements and values in the Measures of Birth and Death indicator domain.
=> 3142 lignes

**RELATIVE_HEALTH_IMPORTANCE.csv** identifies the data elements and values in the Relative Health Importance indicator domain.

**VULNERABLE_POPS_AND_ENV_HEALTH.csv** identifies the data elements and values in the Vulnerable Populations and Environmental Health indicator domain.

**PREVENTIVE_SERVICES_USE.csv** identifies the data elements and values in the Preventive Services indicator domain.

**RISK_FACTORS_AND_ACCESS_TO_CARE.csv** identifies the data elements and values in the Risk Factors and Access to Care indicator domain.
