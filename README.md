# Documentation Stage

## Docker

C'est une plateforme logiciel, en partie en open-source, qui permet de créer, déployer et gérer des applications dans des **conteneurs** sur un seul et même système d'exploitation.

![Logo Docker](https://crunchytechbytz.files.wordpress.com/2018/01/docker2.png?w=1024)

### Conteneur

D'abord étant une image de **conteneur** dans la plateforme logiciel, donc un fichier immuable et ayant une taille très faible, une fois exécutée l'image devient un **conteneur**

Un **conteneur** est un processus logiciel indépendant et léger qui permet d'exécuter les applications qu'il contient à partir du système d'exploitation de la machine hôte (la machine qui contient tous les conteneurs.

On peut le comparer à une VM (Virtual Machine ou Machine Virtuelle, en français). 
La VM est une matérialisation d'un ordinateur/matériel (système d'exploitation, applications ...)
Les **conteneurs** virtualise le système d'exploitation et non le matériel.

![Docker VS VM](https://www.docker.com/sites/default/files/d8/2018-11/docker-containerized-and-vm-transparent-bg.png)

### Avantages
En terme d'avantages on peut parler :
* *Du poids* : Ne demandant pas la mise en place d'un second OS (au contraire d'une VM) et composé d'image de **conteneur** qui seront ensuite lancés, l'ensemble des conteneurs prends beaucoup moins de place qu'une VM en elle même. On peut ainsi gérer plus d'applications.
* *De la vitesse de lancement* : Toujours avec le fait de ne pas imposer de second OS, le lancement se fait donc beaucoup plus rapidement.
* *De la réduction de consomation* : Ne prenant pas en compte la virtualisation, Docker permet de réduire la consommation de RAM.
* *Du partage* : A partir de Docker Hub, un registre commun aux utilisateurs de Docker, on peut récupérer d'autres conteneurs qui ont été partagé.


### Inconvénients
Pour les inconvénients on a :
* *portabilité entre différents serveurs* : Les Machines Virtuelles, bien que plus imposante avec leur second OS permette de continuer à travailler sur le même type de serveur (Lynux, Microsoft ...), mais avec un conteneur utilisant l'OS d'une machine hôte de Linux, passé sur Microsoft ne sera pas aussi simple.
*  *en terme de sécurité* : Les logiciels de cybersécurité n'inspecte, en général, pas les données dans les contenaires, plus propice donc aux attaques de malwares. Mais aussi du fait qu'ils partage tous le même OS, un problème (attaque, faille ou autre) à ce niveau pourrait compromettre tous les **conteneurs**.

### Docker n'est pas seul

Cependant, Docker n'est pas la seule plateforme logiciel de **contenaire**, elle est la plus utilisée, mais il existe des concurrents tel que CoreOS rkt ou aussi Canonical LXD et d'autres.
