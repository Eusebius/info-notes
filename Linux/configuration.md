 # Linux / configuration

## Réactiver le clic à trois doigts sur un *touchpad*

Au passage à Ubuntu 12.04, le clic à trois doigts (bouton du milieu) s’est trouvé désactivé. On peut récupérer cette fonctionnalité avec les commandes de configuration suivantes (les valeurs initiales étaient à 0) :

```
synclient ClickFinger3=2
synclient TapButton3=2
```

## Gnome Classic : récupérer l'icône de volume

Au passage à la 12.04 LTS, l’icône de volume a disparu de la barre des tâches (`gnome-panel`). Pour la rajouter, il suffit de s’assurer que `gnome-sound-applet` est lancé au démarrage (via les préférences des programmes au démarrage, `gnome-session-properties`.

## Ubuntu 12.04 : réactiver l'hibernation

L’hibernation est désactivée par défaut pour tout un ensemble de machines. Pour la réactiver (si l’hibernation fonctionne correctement sur la machine en question), il faut éditer (ou créer) le fichier `/etc/polkit-1/localauthority/50-local.d/com.ubuntu.desktop.pkla` pour y ajouter :

```
[Re-active lhibernation]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes
```

Source : [Activer l’hibernation sous Ubuntu 12.04](http://korben.info/hibernation-ubuntu-12-04.html)
