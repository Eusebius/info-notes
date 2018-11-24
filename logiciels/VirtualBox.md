# VirtualBox

## Restauration d’un snapshot VirtualBox : `CPU model mismatch`

Une erreur de type `CPU model mismatch`, avec un code d’erreur `0x80004005` peut survenir lorsque l’on tente de démarrer un *snapshot* VirtualBox. La machine refuse alors de s’initialiser, parce que l’identifiant du CPU ne correspond pas avec sa configuration. Cela est généralement dû au fait que la machine virtuelle n’a pas été éteinte proprement (*snapshot* enregistré à partir d’une machine en activité ou en hibernation, situation apparemment mal gérée par VirtualBox), et le fait de redémarrer la machine virtuelle (par opposition à la restauration de l’état de sa mémoire) peut résoudre le problème. C’est à ça que sert le bouton « Oublier » dans l’interface de VirtualBox.

## Récupérer eth0 après avoir cloné une machine virtuelle Linux

Si l’on clone une machine virtuelle Linux avec VirtualBox, il est possible que le réseau soit « cassé » sur le système résultant. En pratique, le système n’arrive pas à configurer son interface `eth0`.

Pour régler le problème, il faut supprimer le fichier suivant une fois la machine virtuelle lancée :

```
/etc/udev/rules.d/70-persistent-net.rules
```

Il contient un lien en dur entre l’interface `eth0` et l’adresse MAC de la carte réseau de la machine virtuelle d’origine. Comme cette dernière n’est plus valide, `eth0` est inutilisable. Si l’on supprime ce fichier, il est recréé correctement par Linux au démarrage.
