# Stage chez Braincities

## Projet
Documentation sur GitLab (voir lien plus bas) pour présenter le travail et les rechercher plus tard sur un site.
Mise en place d'un projet pour toute la durée du stage.

## Test Docker

### Création d'un conteneur avec un serveur Httpd Apache 

([image source](https://hub.docker.com/_/httpd))

Commancer par créer un dossier contenant un fichier html, un fichier css et un autre js. (index.html, script.js et style.css)
Lancé DOcker Desktop et un terminal.
Dans le fichier, créer un fichier **Dockerfile** et à l'interieur écrire :
> FROM httpd:2.4

> EXPOSE 80

Le **FROM** indique l'image source utilisée.
Le **EXPOSE** indique le port exposé

Une fois fait on peut alors construire l'image à partir de ce Dockerfile, avec la commande suivante :

`docker build -t nomImage .`

L'image est construire, il ne reste plus qu'à contruire le conteneur à partir d'elle avec la commande :

`docker run -dit --name nomDuSite -p 5000:80 -v $pwd\public-html:/usr/local/apache2/htdocs/ nomImage `

Ici nous indiquons plusieurs choses. En premier on veut construire le conteneur, que lon nommera **nomDuSite** avec la partie *--name nomDuSite*.

On indique le port avec lequelle il va communiquer (5000) et le port exposé de plus tôt (80) avec *-p 5000:80*.

On lui demande de créer un volume dans **/usr/local/apache2/htdocs/** à partir des fichiers d'où on se trouve **$pwd\public-html** avec *-v $pwd\public-html:/usr/local/apache2/htdocs/*.

Et enfin on lui indique l'image à partir de laquelle il va faire le conteneur : **nomImage**.

## Liens

[Journal de bord du stage](https://docs.google.com/document/d/1-oNKVyZcu4cHrA2IedEGQzcLc9lk6CN1mWdfnECaG6Q/edit?usp=sharing)

[Documentation pendant le stage](https://github.com/clara952/Stage2021/wiki)

[GitLab pour le stage](https://gitlab.com/braincities_rbu/apps/tests/clara#)

