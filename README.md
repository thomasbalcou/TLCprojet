
# TLC tp 1

## Tache 1

Le repository contient un DockerFile dans le dossier front pour créer une image de l'application angular. Il utilise Node.js pour construire l'application et Nginx pour la déployer. Les étapes incluent la copie du code source, l'installation des dépendances, la construction de l'application et la copie des fichiers de build pour les intégrer à Nginx.  

Le repository contient aussi un DockerCompose à la racine pour executer tout les conteneurs. Il définit donc plusieurs services, notamment Nginx qui contient le front et agit en tant que reverse proxy, une API Quarkus, PhpMyAdmin, une base de données MySQL, un serveur de courrier et Etherpad. Les différents services dépendent les uns des autres (voir diagramme de déploiement) et leurs ports sont exposés pour permettre les communications entre eux.  

## Tache 2

Le fichier de configuration nginx et à la racine du projet. Ce fichier de configuration NGINX définit trois serveurs en écoutant sur le port 80. Chacun de ces serveurs correspond à un nom de domaine différent, "localhost doodle.tlc.fr", "myadmin.tlc.fr", et "pad.tlc.fr".  

Pour le premier serveur, "localhost doodle.tlc.fr", la requête pour l'URI "/api" sera acheminée vers l'adresse "http://api:8080/api". Les autres requêtes seront servies à partir du répertoire "/usr/share/nginx/html", avec un fichier d'index par défaut "index.html" ou "index.htm". Les erreurs de type 500, 502, 503, 504 seront redirigées vers le fichier "50x.html".  

Le second serveur, "myadmin.tlc.fr", redirigera toutes les requêtes vers "http://phpmyadmin:80". Les erreurs seront gérées de la même manière que pour le premier serveur.  

Enfin, le troisième serveur, "pad.tlc.fr", redirigera toutes les requêtes vers "http://etherpad:9001". Des en-têtes supplémentaires seront ajoutés à ces requêtes pour gérer la mise à niveau et la version HTTP. Les erreurs seront gérées de la même manière que pour les autres serveurs.

## Tache 3

Déploiement

## Tache 4

![App Screenshot](https://github.com/thomasbalcou/TLCprojet/blob/main/DiagrammeDeploiement.png)
