** **Projet de conteneurisation application php+bdd mysql** ** 



Application de création de fiche salariés

_Frontend_ : Apache 2.4 + Application : PHP 7.2.7

_Backend_ : Mysql 5.7

Faire un **docker compose** qui permettra d'orchestrer le lancement de images dockers necessaires


**Infos Frontend**
- Un dockerfile pour Conteneuriser l'apache en copiant le fichier apache_php.conf vers le dossier du conteneur /usr/local/apache2/conf et ensuite rajouter l'instruction suivante 
"Include /usr/local/apache2/conf/apache_php.conf" dans le fichier /usr/local/apache2/conf/httpd.conf local au conteneur
- Un autre Dockerfile pour conteneur l'applicatif php et y installer l'extension _mysqli_ qui lui permettra de faire l'interconnexion avec la bdd mysql.
  commande à executer dans le conteneur docker du php --> docker-php-ext-install mysqli

Monter également le dossier public dans le dossier /var/www/html du conteneur Docker de l'apache et du php (ce dossier contient le code source de l'application ainsi que l'initialisation de la bdd)

Port où publier le service apache --> 8080 ou 8081


**Infos Backend**
- bdd mysql 5.7
- port d'écoute : 3306
  
Persister les données de la bdd qui sont contenues dans ce dossier /var/lib/mysql
Infos envrionnement de la bdd à faire passer au conteneur
      MYSQL_ROOT_PASSWORD: "passwd"
      MYSQL_DATABASE: "mydb"
      MYSQL_USER: "user1"
      MYSQL_PASSWORD: "passwd"

au lancement du conteneur, créer et initialiser la table des employés qui est dans un script sql présent dans le dossier _public/dump_
