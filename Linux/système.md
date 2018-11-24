 # Linux / système

## Raccourcis clavier utiles

* `Ctrl + Alt + Fn` : bascule sur le terminal n (7 pour l’interface X)
* `Ctrl + Alt + Backspace` : tue le serveur X
* `Alt + Print + S` : synchronisation des disques (pour éviter les pertes de données, équivalent de sync)
* `Alt + Print + U` : remontage des systèmes de fichier en lecture seule
* `Alt + Print + B` : reboot
* `Alt + Print + K` : tue tous les processus de la session courante (serveur X inclus)
	
## `error: no video mode` sur un LVM chiffré

Si vous avez installé Linux sur un LVM chiffré, il est possible que GRUB refuse de se lancer en affichant cette erreur. C’est dû au fait que GRUB démarre depuis une partition `/boot` et que certains fichiers dont il a besoin sont sur `/usr/share/grub`, qui est sur un volume encore chiffré, donc inaccessible.

Pour ce qui est de l’accès immédiat au système, un `Ctrl-Alt-Suppr` devrait vous renvoyer sur un GRUB fonctionnel. Pour résoudre le problème par contre, il vous faudra copier les fichiers de police dans un endroit accessible :

```bash
$sudo cp /usr/share/grub/*.pf2 /boot/grub/
```

Ensuite, éditez `/etc/default/grub` pour pointer sur une police disponible :

```
GRUB_FONT="/boot/grub/unicode.pf2"
```

Puis demandez à GRUB de prendre en compte la nouvelle version de votre fichier de configuration :

```bash
$sudo update-grub
```

Référence : [error:: no video mode activated](https://bugs.launchpad.net/ubuntu/+source/grub2/+bug/699802)
