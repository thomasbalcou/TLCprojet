
# TLC projet

## Tache 1

Le repository contient un DockerFile dans le dossier front pour créer une image de l'application angular. Il utilise Node.js pour construire l'application et Nginx pour la déployer. Les étapes incluent la copie du code source, l'installation des dépendances, la construction de l'application et la copie des fichiers de build pour les intégrer à Nginx.  

Le repository contient aussi un DockerCompose à la racine pour executer tout les conteneurs. Il définit donc plusieurs services, notamment Nginx qui contient le front et agit en tant que reverse proxy, une API Quarkus, PhpMyAdmin, une base de données MySQL, un serveur de courrier et Etherpad. Les différents services dépendent les uns des autres (voir diagramme de déploiement) et leurs ports sont exposés pour permettre les communications entre eux.  

## Tache 2

Le fichier de configuration nginx et à la racine du projet. Ce fichier de configuration NGINX définit trois serveurs en écoutant sur le port 80. Chacun de ces serveurs correspond à un nom de domaine différent, ""ThomasBaTLC" et "doodle.balcou.reverse-team.fr"", "myadmin.balcou.reverse-team.fr", et"pad.balcou.reverse-team.fr".  

Pour le premier serveur, "ThomasBaTLC" et "doodle.balcou.reverse-team.fr", la requête pour l'URI "/api" sera acheminée vers l'adresse "http://api:8080/api". Les autres requêtes seront servies à partir du répertoire "/usr/share/nginx/html", avec un fichier d'index par défaut "index.html" ou "index.htm". Les erreurs de type 500, 502, 503, 504 seront redirigées vers le fichier "50x.html".  

Le second serveur, "myadmin.balcou.reverse-team.fr", redirigera toutes les requêtes vers "http://phpmyadmin:80". Les erreurs seront gérées de la même manière que pour le premier serveur.  

Enfin, le troisième serveur, "pad.balcou.reverse-team.fr", redirigera toutes les requêtes vers "http://etherpad:9001". Des en-têtes supplémentaires seront ajoutés à ces requêtes pour gérer la mise à niveau et la version HTTP. Les erreurs seront gérées de la même manière que pour les autres serveurs.

## Tache 3

Pour deployer l'application. Il faut d'abord installer git et maven sur la machine. Puis clonner le repo git. Ensuite lancer le docker compose et l'application est disponible sur la VM. je n'ai pour l'instant pas reussi à faire fonctionner en fonction des sous domaine la page me renvoyant "Reason: DNS resolve failed".  

![App Screenshot](https://github.com/thomasbalcou/TLCprojet/blob/main/captureVM.png)

![App Screenshot](https://github.com/thomasbalcou/TLCprojet/blob/main/captureVM2.png)

## Tache 4

![App Screenshot](https://github.com/thomasbalcou/TLCprojet/blob/main/DiagrammeDeploiement.png)

## Tache 5

J'ai utilisé travis ci pour le deploiement automatisé en construisant un script qui:  

Commence par installer le client SSH sur la machine de déploiement. Ensuite, il crée une sauvegarde de la version actuelle du projet sur le serveur distant, en créant une archive tar gz dans le dossier home de l'utilisateur distant.  

Ensuite, le script clone la dernière version du projet à partir du dépôt GitHub en utilisant la commande git clone.  

Le script construit ensuite les images Docker pour la partie front et API de l'application.  

Enfin, le script lance Docker Compose pour exécuter l'application dans un conteneur Docker.  

 Si une erreur se produit lors de l'exécution de l'une des commandes, le script restaure la sauvegarde du projet précédent à partir de l'archive tar gz en utilisant la commande tar.  
 
Le script utilise une variable d'environnement $PASSWORD définie dans Travis ci pour stocker le mot de passe requis pour se connecter au serveur distant.  
