# [CONFIDENTIAL] ZENIKA / Elastic

## File /ZE/99-ES37

Agent Loustic, l'heure est grave.

L'organisation malfaisante `4STIC` - dont le seul but est la destruction pure et simple de notre société moderne - est entrée dans la phase finale de son plan d'anéantissement.

Vous êtes chargé par les forces du bien de déjouer ses plans __par tous les moyens__.

L'agent Frantic a réussi, au péril de sa vie, à récupérer des données cruciales qui vous permettront de suivre la piste de l'organisation et - nous l'espérons - de retrouver la trace de leur cerveau. Nous savons que cet individu a prévu de passer lui-même à l'action dans un avenir très proche et nous comptons sur vous pour l'identifier. Ainsi nous pourrons l'interpeler avant son coup d'éclat et le réseau tentaculaire du `4STIC` tombera avec lui.

Le but de cette mission sera de suivre une piste qui vous permettra d'identifier le nom de cet individu, de récupérer l'adresse email de votre contact et de le prévenir dès que le mystère aura été élucidé.

Agent Loustic ! Soyez fort, malin, habile !

## Journal de l'agent Frantic

But : grâce aux différents indices, trouver l'adresse email de votre contact et lui envoyer un message pour lui prouver que vous êtes le meilleur !

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

L'index `targets` contient toutes les cibles potentielles : trouvez le document dont la localisation géographique est la plus proche du centre de Bordeaux (44.84514199825976, -0.5777454276682794), le champ `comment` de ce document contiendra la deuxième partie de l'adresse email recherchée.

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

J'ai réussi à récupérer le snapshot d'un index contenant un historique de toutes les opérations effectuées par `4STIC` dans le cadre de leur plan de grande envergure.

Une fois connecté avec le user du "Planificateur", il vous faudra créer une repository (appelez le `privileged_repository` par exemple) de type Shared FS et pointant sur le répertoire `/mnt/data/privileged`.

Vous trouverez alors dans ce repository un unique snapshot qu'il vous faudra restaurer (**sans le global state!**) pour avoir accès aux données des `operations`. De plus, ce snapshot est associé à des `metadata` qui vous donneront une autre partie de l'adresse email !

Chacune de ces opérations contient les champs suivants :

* `@timestamp` : la date d'exécution de l'opération
* `type` : le type de l'opération
* `city` : la ville concernée par l'opération
* `login`: le login Elastic du membre qui a mené l'opération
* `successful` : un booléen indiquant si l'opération a été un succès ou pas

Cet index `operations` est basé sur un `index template`, il y en a plusieurs possibles mais un seul a été appliqué. Une fois découvert, vous trouverez une autre partie de l'adresse email dans les `metadata` associées à cet `index template`.

Le chef de la sécurité de `4STIC` est un petit malin doublé d'un blagueur, il a disséminé des indices dans les données mais je ne manque pas de ressource et j'ai réussi à mettre la main sur la liste des indications permettant d'identifier le membre qui va être en charge de la prochaine opération. Rappelez-vous : il s'agit du cerveau de l'organisation, il est crucial d'obtenir cette information !

#### Chaud

Le premier indice ne peut pas être découvert à l'oeil nu, il faut observer les données sous un angle nouveau.

Votre mission sera de :

* Créer un Data View dans Kibana pour être capable d'observer les données de l'index `operations`
* Toujours dans Kibana, créer une visualisation de type `Heatmap` dont les caractéristiques sont les suivantes :
  * L'axe des ordonnées affiche les `city` dans lesquelles se sont déroulées les opérations (attention, il y en a 8 en tout, nous voulons tous les voir !)
  * L'axe des abscisses affiche les `type` d'opérations, classés par ordre alphabétique (idem, il y en 8 !)
  * La troisième dimension sera le nombre d'opérations : il faudra choisir une échelle de couleur en dégradé, par exemple `Cool` ou `Warm`

Si votre visualisation est bien conçue, vous devriez voir apparaître un chiffre !

#### The best at what he does

Le chiffre que vous avez trouvé correspond en fait à un mois de l'année 2021 ! (1 -> janvier, 12 -> décembre)

Nous savons que le membre sélectionné est celui qui a eu le plus grand pourcentage de succès au cours de ce mois de l'année 2021, nous sommes à deux doigts de le trouver !

Si vous savez utiliser les agrégations de type `bucket_script`, alors vous avez les moyens de sélectionner les opérations du mois concerné et de trouver le login du membre qui a eu le plus pourcentage de succès.

Une fois son login trouvé, il devrait être facile de retrouver son nom complet dans l'index des `membres` (rappelez-vous, nous savons comment les logins sont formés à partir du prénom, du nom et de la date de naissance des `membres` !). Enfin la dernière partie de l'adresse email que nous recomposons depuis le début de cet aventure se trouve dans le `password` de ce membre.

## Fin de l'aventure

Si vous êtes arrivés jusque là, vous êtes en possession de `5` parties d'adresse email qu'il vous suffira de rassembler dans l'ordre d'obtention pour obtenir une adresse email : `<1><2><3><4><5>@zenika.com`.

Envoyez nous un petit message ! TODO : à compléter.