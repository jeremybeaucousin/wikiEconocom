# Dev local

## Mysql

* Get image
> docker pull mysql:5.7

* Create container
> docker run --name mysqlCreoleV2 -e MYSQL_ROOT_PASSWORD=creoleV2 -d -v mysqlCreoleV2:/var/lib/mysql -v C:\DockerVolume\creoleV1.5\mysql:/volumeWindows -p 3306:3306 mysql:5.7

* Enter container
> docker exec -it mysqlCreoleV2 /bin/bash

## PYTHON

* Build image :
> docker build --rm -f Dockerfile -t python:creoleV2 ./

NB : Se placer àu niveau de l'emplacement du Dockerfile (situé dans le dépot git)

* Create container
> docker run -it --rm --name pythonCreoleV2 -p 5000:5000 -v "{{$PATH_TO_DATA}}:/r3a/r3aadmaa" -v "{{$PATH_TO_SOURCE}}:/usr/src/myapp" -w /usr/src/myapp python:creoleV2 
 
* Enter container
> docker exec -it pythonCreoleV2 /bin/bash

## Connecter les conteneur entre eux

* Create network
> docker network create creole-network

* Connect the mysql container to network 
> docker network connect creole-network mysqlCreoleV2

* Connect the python container to network
> docker network connect creole-network pythonCreoleV2

## Container mysql 8 DEV mut

### Récupération de l'image

> docker pull mysql:5.7

### Création du répértoire de configuration

> /DockerVolumes/mysql/creoleV2/conf.d/

### Création du fichier de configuration

> vi /DockerVolumes/mysql/creoleV2/conf.d/docker.cnf

```cnf
[mysqld]
skip-host-cache
skip-name-resolve
bind-address = 0.0.0.0
```

### Création du conteneur MySQL

* Environnements :
  * MYSQL_ROOT_PASSWORD : mot de passe root
* Volumes :
  * mysqlCreoleV2 : volume de données
  * /DockerVolumes/CreoleAPI/mysql/conf/ : volume de configuration
* Ports :
  * 3307:3306 : port de la machine host:port sur le conteneur
> docker run --name mysqlCreoleV2 -e MYSQL_ROOT_PASSWORD=creoleV2 -d -v "mysqlCreoleV2:/var/lib/mysql" -v "/DockerVolumes/CreoleAPI/mysql/conf/:/etc/mysql/conf.d/" -v "/DockerVolumes/CreoleAPI/mysql/mount:/hostVolume" -p 3307:3306 mysql:5.7

### Modification des droits pour la connexion à distance

* Connexion au conteneur
> docker exec -it mysqlCreoleV2 bash
* Connexion à la base de données :
> mysql -u root -p mysql
* Lancer la requête de modification des droits :

```SQL
GRANT ALL ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
```

## Container python

### Création de l'image

> docker build --rm -f Dockerfile -t python:creoleV2 ./
NB : Se positionner au niveau du dépôt GIT

### Création du conteneur python

> docker run -it --rm -d --name pythonCreoleV2 -p 5000:5000 -v "/DockerVolumes/CreoleAPI/python/r3aadmaa:/r3a/r3aadmaa" -v "/var/www/root/creoleAPI/CreoleAPI:/usr/src/myapp" -w /usr/src/myapp python:creoleV2

### DEV DISIT

## Installation des utilitaires

> yum install rpm-build

## Connexion au git-lab

* Création de la clé
> ssh-keygen -t rsa -C "GitLab" -b 4096

nb : Pour changer le mot de passe éxécuter la commande suivante
> ssh-keygen -p

* Se connecter sur l'IHM du gitlab à l'endroit suivant
> [git-dsi->/profile/keys](https://git-dsi.log.intra.laposte.fr/profile/keys)

* Récupérer la clé générée et lui donner un nom
> cat ~/.ssh/id_rsa.pub

* La copier dans la champ "key", elle doit ressembler au patron suivant :

> ssh-rsa {{clé}} GitLab

## Lancer le service en r3aadm

* Activation du venv
> source ~/creoleAPIVenv/bin/activate
* Lancement du service
>
* Desactivation du venv
> deactivate

### rpms

## Técharger rpm en local

> yumdownloader --resolve mysql-community-server

## Installer rpm présent en local

> sudo yum --disablerepo=* localinstall *.rpm

## Génération du rpm

> bash support/build_package.sh 15.0.0