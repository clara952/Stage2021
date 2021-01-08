# Stage chez Braincities

## Table des matières
* [Projet](https://github.com/clara952/Stage2021#projet)
* [Test Docker](https://github.com/clara952/Stage2021#test-docker)
* [Création conteneur Node.js](https://github.com/clara952/Stage2021#creation-conteneur-node.js)
* [Liens](https://github.com/clara952/Stage2021#liens)


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

## Création conteneur Node.js

### Installation Node.js

Commencez par installer [Node.js](https://nodejs.org/en/download/)

Une fois fait lancé un terminal (PwerShell par exemple) et vérifiez la bonne installation avec :

`node -v`

`npm -v`

### Création du dossier de base Node.js

 Créer un nouveau dossier (**docker_node**) et à l'intérieur ajouter un fichier **package.json** avec à l'intérieur : 
 
>{

>  "name": "nodejs-image-demo",

>  "version": "1.0.0",

>  "description": "nodejs image demo",

>  "author": "Sammy the Shark <sammy@example.com>",

>  "license": "MIT",

>  "main": "app.js",

>  "keywords": [

>    "nodejs",

>    "bootstrap",

>    "express"

>  ],

>  "dependencies": {

>    "express": "^4.16.4"

>  }

>}

Dans le terminal : `npm install`

Si cela à fonctionné alors dans votre dossier vous devriez retrouver un fichier **package-lock.json**

Maintenant vous allez pouvoir ajouter le site web en lui-même. On va commencer par le fichier **app.js**.  On y retrouvera les itinéraires du projet, le répertoire de base, le port et d'autres informations très importante pour la suite. 

#### App.js
D'abord nous allons créer les constante.
Pour l'application Express
> const express = require('express');
>  const app = express(); 


Puis les objets Routeur 
> const router = express.Router();

Indiquez aussi le répertoir de base pour votre site, ainsi que le port
> const path = __dirname + '/views/';
> const port = 8080;


Nous devons aussi donner les différentes route du site :

> router.use(function (req,res,next) {
>   console.log('/' + req.method);
>   next();
> });
> 
> router.get('/', function(req,res){
>   res.sendFile(path + 'index.html');
> });


Vous pouvez en ajouter autan que souhaiter, pouvant s'appliquer pour une page précise ou un ensemble.

Enfin on ajoute les actifs statiques, le router middleware et indiquer à l'application d'écouter sur le port 8080 :
> app.use(express.static(path));
> app.use('/', router);
> 
> app.listen(port, function () {
>   console.log('Example app listening on port 8080!')
> })



#### Dossier Views
Vous pourrez alors créer un dossier **views** que vous aurez mentionné dans le fichier précédent. Et c'est dans ce dossier **views** que vus retrouverez toutes vos pages html, le css et d'autres.
Donc dans ce dossier ajouter les fichiers de votre site. 

#### Vérifier que tout fonctionne
Pour vérifier que votre site fonctionne correctement avant de  créer une image à partir de celui-ci, dans un terminal vous pouvez lancer la commande :
`node app.js`

Normalement après cela, sur votre navigateur, si vous tapez votre adresse ip et e port choisit (exemple : **http://localhost:8080**), alors vous pourrez voir votre site. Si tout est bon, n'oublié pas de sortir du serveur dans le terminal en faisant un **ctrl + C** et vous pourrez passer à la suite.

### Création du Dockerfile

Pour la création de l'image vous devez d'abord faire un Dockerfile avec les bonne informations. 
Allez donc à la racine de votre dossier et créez le fichier **Dockerfile** 

Dedans on va indiquer l'image source, ici une image Linux de Node version 10
> FROM node:10-alpine

Créer un dossier pour tous les répertoires
> RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app

Indiquer le répertoire de travail
> WORKDIR /home/node/app

Copier tous les fichier package**.json
> COPY package*.json ./

Indiquer que l'utilisateur sera node pour l'installation de npm
> USER node

Installer npm
> RUN npm install

Copier le code d'application avec les bonnes autorisations 
> COPY --chown=node:node . .

Exposé le port 8080
> EXPOSE 8080

et démarrer l'application !
> CMD [ "node", "app.js" ]

Vous pourrez rajouter un fichier **.dockerignore** pour éviter de recopier des fichier qui ne changeront pas, donc avec dedans seulement :

> node_modules
> npm-debug.log
> Dockerfile
> .dockerignore
### Création de le conteneur Docker 
Créez tout d'abord votre image, pour par la suite faire le conteneur
`docker build -t nomImage`

Pour vérifier vous pouver utiliser : `docker images`

Créer le conteneur maintenant
`docker run --name nomConteneur -p 8080:8080 -d nomImage`

Pour vérifier vous pouver utiliser : `docker ps`

Une fois créer vous pouvez donc retrouver votre site sur la page **http://localhost:8080/**


## Liens

[Journal de bord du stage](https://docs.google.com/document/d/1-oNKVyZcu4cHrA2IedEGQzcLc9lk6CN1mWdfnECaG6Q/edit?usp=sharing)

[Documentation pendant le stage](https://github.com/clara952/Stage2021/wiki)

[GitLab pour le stage](https://gitlab.com/braincities_rbu/apps/tests/clara#)

