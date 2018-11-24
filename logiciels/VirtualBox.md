# VirtualBox

## Restauration d’un snapshot VirtualBox : `CPU model mismatch`

Une erreur de type `CPU model mismatch`, avec un code d’erreur `0x80004005` peut survenir lorsque l’on tente de démarrer un *snapshot* VirtualBox. La machine refuse alors de s’initialiser, parce que l’identifiant du CPU ne correspond pas avec sa configuration. Cela est généralement dû au fait que la machine virtuelle n’a pas été éteinte proprement (*snapshot* enregistré à partir d’une machine en activité ou en hibernation, situation apparemment mal gérée par VirtualBox), et le fait de redémarrer la machine virtuelle (par opposition à la restauration de l’état de sa mémoire) peut résoudre le problème. C’est à ça que sert le bouton « Oublier » dans l’interface de VirtualBox.
