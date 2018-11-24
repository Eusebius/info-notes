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

## Changer le mot de passe d'un volume LVM chiffré

On suppose que le volume chiffré est sur `/dev/sda5`. Il faut d’abord utiliser la commande suivante pour ajouter un nouveau mot de passe sur un des 8 slots de LUKS :

```bash
cryptsetup -v luksAddKey /dev/sda5
```

On commence par donner le mot de passe initial, LUKS identifie le numéro de slot sur lequel il est enregistré (supposons 0), à condition d’avoir utilisé l’option `-v`.
LUKS demande alors un nouveau mot de passe, qui sera attribué à un nouveau slot. Il faut alors détruire l’ancien slot (0) pour annuler l’ancien mot de passe :

```bash
cryptsetup -v luksKillSlot /dev/sda5 0
```

Il faut pour cela fournir le nouveau mot de passe, ou encore tout autre mot de passe valide sur un slot autre que 0. Après cette opération seul le nouveau mot de passe (et tous les autres qui pourraient éventuellement préexister) demeure valide.

## Lire des DVD avec CSS sous Ubuntu

Par défaut, les bibliothèques CSS permettant de déchiffrer les DVD protégés ainsi ne sont pas installées sous Ubuntu (ou Debian), parce qu’elles ne sont pas libres. Par contre, le package `libdvdread4` (ou son successeur) inclut un script d’installation de ces bibliothèques. La commande suivante permet leur installation :

```bash
sudo /usr/share/doc/libdvdread4/install-css.sh
```

## Changer la date de modification d'un fichier

```bash
touch -t [[YY]YY]MMDDhhmm[.ss] nomFichier
```

Par exemple, si l’on souhaite fixer la date de modification du fichier foobar au premier mars de l’année courante à 20h42 : `touch -t 03012042 foobar`

## find / grep : lister tous les fichiers contenant une chaîne donnée

```bash
find / -type f -exec grep -l "chaine" {} \;
```

## Forcer le chargement de GRUB au démarrage d'Ubuntu

Il suffit, au moment du chargement du système, d’appuyer sur shift (ou parfois sur échappement, apparemment) et de garder la touche appuyée jusqu’à l’apparition de l’écran GRUB.

## Effacer irrémédiablement les données de tout un disque dur

```
shred -fvz -n 5 /dev/sda
```

Où `/dev/sda` est bien entendu le disque que l’on souhaite effacer. `-f` change automatiquement les droits sur les fichiers pour pouvoir effectuer l’opération, `-v` désigne un mode *verbose* bien utile pour afficher la progression de cette très longue opération, `-n 5` fixe le nombre de passes (à ajuster suivant le niveau de paranoïa).
