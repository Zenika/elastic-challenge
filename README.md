# [CONFIDENTIAL] ZENIKA / Elastic
## File /ZE/99-ES37

Agent Emile Lastic, l'heure est grave.

blabla, l'histoire.
But : grâce aux différents indices, trouver l'adresse email de votre contact et lui envoyer un email pour (...)

Pré-requis : Docker

* Cloner ce repository
* Démarrer le docker-compose via `docker compose up`
* Une fois les containers démarrés, se connecter à Kibana via `https://localhost:5601`

Pour démarrer l'enquête, vous allez d'abord devoir vous connecter à l'application Kibana et trouver le dashboard `<nom_du_dashboard>` (qque chose du genre "premier contact"), le premier indice s'y trouvera.

Les données contenues dans l'index `targets` ont fuité. Cet index contient la liste des cibles potentielles, il faut trouver ici la cible qui est la plus proche de la Mairie de Bordeaux.
Le document correspondant aura un champ comment qui permettra de constituer le 2ème indice.

