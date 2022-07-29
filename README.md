# [CONFIDENTIAL] ZENIKA / Elastic

## File /ZE/99-ES37

Agent Loustic, l'heure est grave.

L'organisation malfaisante `4STIC` - dont le seul but est la destruction pure et simple de notre société moderne - est entrée dans la phase finale de son plan d'anéantissement.

Vous êtes chargé par les forces du bien de déjouer ses plans __par tous les moyens__.

L'agent Frantic a réussi, au péril de sa vie, à récupérer des données cruciales qui vous permettront de suivre la piste de l'organisation et - nous l'espérons - de retrouver la trace de leur cerveau. Nous savons que cet individu a prévu de passer lui-même à l'action dans un avenir très proche et nous comptons sur vous pour l'identifier. Ainsi nous pourrons l'interpeler avant son coup d'éclat et le réseau tentaculaire du `4STIC` tombera avec lui.

Le but de cette mission sera de suivre une piste qui vous permettra d'identifier le nom de cet individu, de récupérer l'adresse email de votre contact et de le prévenir dès que le mystère aura été élucidé.

Agent Loustic ! Soyez fort, malin, habile !

## Journal de l'agent Frantic

But : grâce aux différents indices, trouver l'adresse email de votre contact et lui envoyer un message pour lui prouver comme vous êtes fort !

### Pré-requis / démarrage

Vous avez accès à Docker et pouvez lancer un docker-compose.

* Cloner ce repository
* Démarrer le docker-compose via `docker compose up`
* Une fois les containers démarrés, se connecter à Kibana via `https://localhost:5601`

### La piste à suivre

Pour démarrer l'enquête, vous allez d'abord devoir vous connecter à l'application Kibana grâce au seul compte que j'ai pu me procurer (login : `tt64`, mot de passe : `password`) et trouver le dashboard `Premiere Piste`. Vous aurez en votre possession la première partie de l'adresse email recherchée ! \o/

### La cible

J'ai réussi à obtenir un _leak_ des données confidentielles de 4STIC. Celles-ci contiennent la liste des cibles potentielles de l'organisation.

D'après mes informations, la prochaine cible serait très proche du centre de Bordeaux, en France.

L'index `targets` contient toutes les cibles potentielles : trouvez le document dont la localisation géographique est la plus proche du centre de Bordeaux (44.84514199825976, -0.5777454276682794), le champ `comment` de ce document contiendra la deuxième partie de mon adresse email.

### Le planificateur

Ok, il semblerait que l'organisation ait chargé un de ses membres de préparer cette opération sur cette cible près de Bordeaux ...

Je n'ai pas réussi à en apprendre énormément sur lui mais il est crucial d'arriver à le retrouver car lui seul a accès à toutes les données qui nous intéressent.

Tout ce que je connais de lui :

* son prénom : il commence par la lettre J
* son nom de famille : il commence par la lettre E et finit par la lettre R
* sa décennie de naissance : 1980
* sa ville de résidence : Barcelone

Les données des membres de l'organisation sont contenues dans l'index `members`.

Si vous arrivez à trouver ce membre, il vous suffira de vous connecter à Kibana avec un login formé de la première lettre de son prénom, de la première lettre de son nom de famille et des deux derniers chiffres de son année de naissance. Son mot de passe sera celui qui est en clair dans le document trouvé dans l'index `members`.

### Les opérations

A partir d'ici, il faudra que vous vous connectiez avec les login et mot de passe du membre "Planificateur".

Continuer (création d'un snapshot, etc.)