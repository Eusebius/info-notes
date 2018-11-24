# Docker

## Lancer une application Linux en mode graphique

Pour pouvoir lancer une application X depuis un conteneur Docker, il faut réaliser les opérations suivantes :

* Donner à Docker les droits d’accès au serveur X (sur le système hôte, bien entendu) : `xhost +local:docker`
* Lancer le conteneur avec (au moins) les options `-e DISPLAY=$DISPLAY` et `-v /tmp/.X11-unix/:/tmp/.X11-unix`

## Se détacher d'un conteneur sans l'arrêter

Suivant la manière dont vous avez lancé votre conteneur Docker et la façon dont vous y êtes connectés (notamment si vous avez fait un `docker attach` plutôt qu’une connexion SSH), si vous tapez simplement `exit` dans votre console, il y a des chances que vous arrêtiez le conteneur en sortant, ce qui n’est peut-être pas ce que vous souhaitez. Si vous voulez quitter le terminal du conteneur mais laisser celui-ci tourner (par exemple parce que c’est un serveur), il faut taper la séquence `Ctrl+p Ctrl+q`.
