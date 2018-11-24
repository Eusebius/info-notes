# Docker

## Lancer une application Linux en mode graphique

Pour pouvoir lancer une application X depuis un conteneur Docker, il faut réaliser les opérations suivantes :

* Donner à Docker les droits d’accès au serveur X (sur le système hôte, bien entendu) : `xhost +local:docker`
* Lancer le conteneur avec (au moins) les options `-e DISPLAY=$DISPLAY` et `-v /tmp/.X11-unix/:/tmp/.X11-unix`
