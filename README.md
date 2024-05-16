## Visualiser les prochains passages de transports en commun

![alt text](https://github.com/anteid/ha-tbm/blob/main/Capture.png?raw=true)

## Demande de clé pour accéder aux WebServices Bordeaux Métropole

Faire une demande sur : https://opendata.bordeaux-metropole.fr/pages/demande-cle/

## Requêtes JSON

Deux requêtes JSON sont effectués sur le jeu de données  sv_horai_a :
- une requête pour récupérer les 5 prochains passages de bus à l'arrêt Henri Barbusse.
- une requêete pour connaitre l'heure d'arrivée de ces bus à l'arrêt Gambetta.

### Jeu de données sv_horai_a
Permet de récupérer les prochains passages de bus : numéro de course, heure estimée, à un arrêt donné 
Explication du jeu de données : https://opendata.bordeaux-metropole.fr/explore/dataset/sv_horai_a/information/

Pour récupérer l'identifiant de l'arrêt : se servir de la carte disponible sur https://opendata.bordeaux-metropole.fr/explore/dataset/sv_arret_p/map/?location=18,44.85644,-0.6419&basemap=jawg.streets. Exemple : Henri Barbusse : GID n°992.

Entrée du jeu de données :
- rs_sv_arret_p : arrêt pour lequel on veut récupérer les horaires de passage (992 pour Henri Barbusse)
- etat : NON_REALISE (pour renvoyer uniquement les prochains passages et pas les horaires des courses déjà effectuées)
- attributes : sorties souhaitées du jeu de données
  - rs_sv_cours_a : numéro de course
  - hor_estime : heure de passage estimée du bus à l'arret
- order_by : selon quel critère on veut ordonner les données en réponse (ici on veut les prochains passage en premier)
- maxfeatures : nombre de réponses max souhaitées (ici 5 bus pour les 5 prochains passages max)
- key : la clé fournie par Bordeaux Métropole


Sorties du jeu de données :
  - rs_sv_cours_a : numéro de course
  - hor_estime : heure de passage estimée du bus à l'arret

Pour la deuxième requête, la particularité est qu'on filtre les résultats selon les courses qui nous intéressent :

Entrée du jeu de données :
- filter : on s'intéresse aux courses relevées dans la première requete à l'arrêt 2348 (Gambetta, cf carte pour adapter le numéro à l'arrêt voulu)
- attributes : sorties souhaitées du jeu de données
  - rs_sv_cours_a : numéro de course
  - hor_estime : heure de passage estimée du bus à l'arret
- order_by : selon quel critère on veut ordonner les données en réponse (ici on veut les prochains passage en premier)
- key : la clé fournie par Bordeaux Métropole
