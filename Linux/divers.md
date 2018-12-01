 # Linux / divers

## Lire des BluRay avec VLC

* Installer les paquets nécessaires :
```bash
sudo aptitude install vlc libbluray1 libbluray-bdj libaacs0 libbdplus0
```
* Installer le fichier de clés le plus récent :
```bash
mkdir ~/.config/aacs
wget http://vlc-aacs.whoknowsmy.name/files/KEYDB.cfg -O ~/.config/aacs/KEYDB.cfg
```
* Ouvrir le disque dans VLC en mode Blu-Ray (en cochant « pas de menus »).
