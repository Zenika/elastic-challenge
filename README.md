# [CONFIDENTIAL] ZENIKA / Elastic

## File /ZE/99-ES37

Agent Loustic, l'heure est grave.

L'organisation malfaisante `4STIC` - dont le seul but est la destruction pure et simple de notre société moderne - est entrée dans la phase finale de son plan d'anéantissement.

Vous êtes chargé par les forces du bien de déjouer ses plans __par tous les moyens__.

Un agent a réussi, au péril de sa vie, à récupérer des données cruciales qui vous permettront de suivre la piste de l'organisation et - nous l'espérons - de retrouver la trace de leur cerveau. Nous savons que cet individu a prévu de passer lui-même à l'action dans un avenir très proche et nous comptons sur vous pour l'identifier. Ainsi nous pourrons l'interpeler avant son coup d'éclat et le réseau tentaculaire du `4STIC` tombera avec lui.

Le but de cette mission sera de suivre une piste qui vous permettra d'identifier le nom de cet individu, de récupérer l'adresse email de votre contact et de le prévenir dès que le mystère aura été élucidé.

Agent Loustic ! Soyez fort, malin, habile !

## Indications détaillées

But : grâce aux différents indices, trouver l'adresse email de votre contact et lui envoyer un message pour lui prouver comme vous êtes fort !

### Pré-requis / démarrage

Vous avez accès à Docker et pouvez lancer un docker-compose.

* Cloner ce repository
* Démarrer le docker-compose via `docker compose up`
* Une fois les containers démarrés, se connecter à Kibana via `https://localhost:5601`

### Indice 1

Pour démarrer l'enquête, vous allez d'abord devoir vous connecter à l'application Kibana et trouver le dashboard `Premiere Piste`.

### Indice 2

Les données contenues dans l'index `targets` ont leakées. Cet index contient la liste des cibles potentielles, il faut trouver ici la cible qui est la plus proche de la Mairie de Bordeaux.
Le document correspondant aura un champ comment qui permettra de constituer le 2ème indice.
