# Mini projet pour tictactrip 
<center>Zhenyu ZHU <center>

***

## Analyse du problème

- Il y a quatre fichiers de données au total. ***ticket_data.csv*** il contient les principales informations. ***cities.csv***, ***station.csv***, ***provider.csv*** ils fournissent des descriptions supplémentaires des données contenues dans *** ticket_data.csv*** 
- Informations importantes : **Distance** et **durée** du voyage, **mode de transport** (divers)
- Opérations importantes: **Format uniforme** des données, **regroupement**, **conversion des unités de mesure**


## Traitement des données

#### Durée du voyage:
- Nous connaissons l'heure de départ et l'heure d'arrivée du voyage, nous soustrayons donc les deux pour obtenir la durée. La conversion des données au format **datetime** facilite le calcul.

#### Transport_type: 
- Le fichier** ticket_data** contient des informations sur **company** et sur **other_companies**. En fonction des informations contenues dans le fichier **provider.csv**, je peux donc vérifier la méthode de transport correspondante.
- La raison pour laquelle je n'utilise pas de liens intérieurs est de **réduire au minimum les colonnes inutiles**.
- Grâce au format de données de **set**, il est possible d'éviter les schémas de Transport_type.
- Lorsque j'ai fini de traiter toutes les méthodes de trafic, j'ai remarqué que la **compagnie aérienne** n'apparaissait pas dans le fichier **provider.csv**. Cela n'est pas possible pour les voyages de moyenne ou longue distance, et je pense donc que cela est dû à des problèmes liés aux données. Dans le fichier **station.csv**, j'ai observé que certains d'entre eux sont des **aérodromes** et d'autres des **gares ferroviaires**. Il serait possible de gérer ce problème si l'on pouvait énumérer le numéro d'identification de la station de tous les aéroports qu'il contient.

#### Distance: 
- Pour calculer la distance entre les villes, je relie d'abord les coordonnées des villes de **cities.csv** à **ticket_data.csv.** 
- Calculer la distance réelle entre deux coordonnées avec **geopy.distance**

## Visualisation

- Les distances sont divisées en trois groupes : 0-200 km, 201-800 km et 800-2000 km. 
- Convertir les colonnes duree de **datetime** en **float**
- Graphique basé sur **le prix du voyage**, **la durée du voyage respectivement**. Average, Min, Max

## Prévision de prix

- Le prix du voyage dépend du mode de transport, de la distance parcourue et de la durée du voyage. 
- Standardisation des données.
Regrouper les données en groupe de formation, groupe de test et groupe d'examen.
Substituer dans le modèle, ajuster et tester le modèle
- Le test du modèle peut être effectué à l'aide de ** K-fold** et **cross-validation **.
- Un calcul de type round-robin peut être utilisé pour comparer la qualité du modèle pour différents** hyperparamètres**. En raison des performances de la machine, je ne peux pas utiliser l'une ou l'autre de ces méthodes de validation du modèle, mais j'ai donné le code et je l'ai annoté.
- S'il y a plusieurs modèles, model stacking peut se faire à la fin pour optimiser les résultats

## Map Interaction

- **Geopandas** et **folium** permettent le marquage des coordonnées sur la carte.

- J'ai créé un exemple qui affiche des informations spécifiques sur ce voyage en fonction de l'identifiant du voyage.
- Pour les cartes interactives, des microservices peuvent être construits en python pour une interaction plus efficace. Par exemple Dash, Flask etc. Cela permet d'afficher sur la carte des informations sur les trajets précédents ou des prévisions de prix par ID, ville de départ et ville d'arrivée.

## Mise en œuvre ou amélioration possible

- La chaleur du voyage varie tout au long de l'année, ce qui peut avoir une incidence sur le choix des options de voyage et sur le prix du voyage. Pour des prédictions plus précises, le modèle doit être obtenu en traitant les séries temporelles.
- Les préférences en matière de prix et de temps de trajet ne sont pas les mêmes pour tous les utilisateurs. Pour les utilisateurs sensibles au prix et au temps, deux modèles différents devraient être introduits pour prédire les prix et recommander des déplacements.

