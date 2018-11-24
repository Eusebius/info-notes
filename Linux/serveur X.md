# Linux / serveur X

## Forcer ou restaurer la résolution des polices de caractères

Sous Linux, lorsque l’on installe les drivers propriétaires de sa carte graphique Nvidia (paquet `nvidia-driver`, qui désactive le driver libre `nouveau`), il est possible de se retrouver dans une situation où la définition globale de l’écran est correcte (si vous avez de la chance) mais où la résolution des polices de caractères de l’interface est beaucoup trop élevée. C’est juste que le driver Nvidia a décidé de les calculer lui-même, et qu’il fait de la merde. Le résultat, c’est que toute l’interface a l’air énorme, bien que la résolution d’affichage semble correcte (i.e. les icônes sont affichées avec un niveau de détail normal).

On peut vérifier la résolution des polices de caractères actuellement utilisées avec la commande suivante :

```bash
cat /var/log/Xorg.0.log | grep -i dpi
```

qui renverra, entre autres, quelque chose du genre :

```
[    18.242] (--) NVIDIA(0): DPI set to (139, 144); computed from "UseEdidDpi" X config
```

Pour résoudre le problème, on peut bien sûr aller dans les réglages de son gestionnaire de bureau pour forcer la résolution des polices. Dans KDE, c’est dans « Configuration du système », « police », « forcer le PPP des polices ». La valeur standard, chez moi, se situe vers 96 (ajustez selon votre niveau de presbytie).

Toutefois, ça ne résoud le problème que pour le gestionnaire de bureau (KDE, Gnome, Cinnamon ou je ne sais quoi), mais pas pour l’ensemble du système X et notamment pas pour votre gestionnaire de session (écran d’authentification). Il est donc plus utile d’aller faire le réglage directement à cet endroit, puisque c’est ce composant qui va lancer le serveur X.

Dans sddm, il faut aller ajouter la ligne suivante à `/usr/share/sddm/scripts/Xsetup` :

```
xrandr --dpi 96
```

et rebooter le système (ou juste relancer le service sddm, je suppose — non testé, j’ai la flemme).

Sources :

* [[kubuntu] fonts too big after installing nvidia driver](https://ubuntuforums.org/showthread.php?t=2201820)
* [Set "ForceFontDPI" globally such that it applies to SDDM](https://forum.kde.org/viewtopic.php?f=66&t=128244)

