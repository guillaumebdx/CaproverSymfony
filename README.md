# CaproverSymfony

## 1/ Se rendre sur le vps et installer via docker
`docker run -p 80:80 -p 443:443 -p 3000:3000 -v /var/run/docker.sock:/var/run/docker.sock -v /captain:/captain caprover/caprover`

Ceci installera caprover et sera directement accessible à 

http://[IP_OF_YOUR_SERVER]:3000

Le mot de passe par défaut est *captain42*

## 2/ Créer un wildcard 

Sur un nom de domaine afin de permettre à caprover de générer des sous domaines à la volée pour créer les applications par exemple : votreapplication.votreNDD.fr, phpmyadmin.votreNDD.fr, etc)

## 3/ Créer les apps.

Aller dans le menu Apps et créez ces Apps (et autres si besoin) :

(one click app) mysql
(one click app) phpmyadmin
Votre application symfony


## 4/ Configurez votre app symfony depuis l’interface caprover

### onglet App configs

Indiquez les variables globales

APP_ENV : prod

DATABASE_URL : mysql://db_user:db_password@127.0.0.1:3306/db_name

### onglet Deployment

Indiquez le repo github ainsi que la branche pour le déploiement automatique

Puis allez dans les webhooks de votre repo github pour copier coller l’url fourni dans le premier champ par caprover

## Pour se connecter en ssh

Il faudra automatiser lors du déploiement les migrations. Pour l'instant, se connecter en ssh pour accéder à bin/console
Exemple :

`ssh root@vps734968.ovh.net`

Puis entrer dans le container docker avec cette commande : (remplacez par le nom de votre application)

`docker exec -it $(docker ps --filter name=srv-captain--poc-symfony -q) /bin/sh`

Ou si comme moi vous préférez le bash que le shell :

`docker exec -it $(docker ps --filter name=srv-captain--poc-symfony -q) /bin/bash`

Si vous testez ce POC, sachez que cette application n'a qu'une seule route de controller : /home
