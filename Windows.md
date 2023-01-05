# Windows

## Créer une partition EFI sur un disque Windows qui n'en a pas

Lorsque l'installeur Windows détecte qu'une autre installation existe sur un autre disque, avec une partition EFI valide, il choisit de ne pas créer de 
nouvelle partition EFI et de plutôt réutiliser l'ancienne. Cela peut poser problème lorsque le disque de l'ancienne installation est destiné à disparaître. 
Il faut donc en recréer une nouvelle, ce qui peut nécessiter de faire un peu de place sur le disque. Heureusement, c'est beaucoup plus pratique dans un 
monde UEFI/GPT qu'avec un BIOS _legacy_ et du MBR.

1. Booter sur le nouveau système, en utilisant la partition EFI de l'ancien disque.
2. Utilisez le gestionnaire de disques pour identifier le disque de la nouvelle installation (le système en cours d'exécution). S'il n'y a pas d'espace disque suffisant, dégagez 512Mo d'espace disque contigu en diminuant la taille de la partition courante (ou d'une autre partition du même disque).
4. Lancer `cmd.exe` en mode administrateur.
5. Lancez `diskpart` :
   - Utilisez `list disk` pour trouver le numéro du disque courant ;
   - Le sélectionner avec `select disk` ;
   - Lister les partitions avec `list partitions` ;
   - Créez une nouvelle partition EFI avec `create partition efi size=512` ;
   - Formatez-la avec `format quick fs=fat32` ;
   - Assignez-y une lettre de volume avec `assign letter=z` (par exemple) ;
   - Quittez diskpart avec `exit`.
6. Installez les fichiers nécessaires au boot avec `bcdboot C:\Windows /s Z:` (si C est votre disque système et Z la lettre de volume que vous venez d'affecter à votre partition EFI).
7. Éteignez votre machine, débrancher le disque devenu inutile si vous le souhaitez, redémarrez en vous assurant de bien booter en UEFI sur le bon disque.

Source : [Move EFI partition to another drive – Windows 10](https://www.tomica.net/blog/2020/04/move-efi-partition-to-another-drive-windows-10/)
