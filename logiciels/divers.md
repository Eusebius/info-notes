# Logiciels divers

## Subversion : ajouter récursivement des fichiers avec `svn add`

```bash
svn add ––depth=infinity ––force *
```

Si ça ne fonctionne pas, c’est peut-être pour des histoires de droits insuffisants (auquel cas il faudra un `mv` du répertoire en cause puis un `svn delete` pour régler le problème), ou bien parce qu’il reste un répertoire `.svn` qui ne devrait pas être là (et qui empêche l’ajout au système de gestion de versions).

## Altera Quartus sous Ubuntu : faire reconnaître un « USB Blaster »

Il y a énormément de problèmes qui peuvent survenir lorsque l’on veut faire fonctionner Altera Quartus avec une plate-forme FPGA. Pour ma part (Quartus 11.1, Ubuntu 11.10, carte Altera Cyclone II) j’avais une erreur au moment de la programmation du FPGA, qui affichait :

```
unexpected error in JTAG server -- error code 89
```

La manipulation suivante m’a permis de résoudre le problème :

```
sudo vi /etc/udev/rules.d/51-usbblaster.rules
```

Contenu du fichier (le code est en réalité sur une seule ligne) :

    # Altera USB-Blaster rule to set mode to 666.
    SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device",
        SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6001",
        MODE="0666", NAME="bus/usb/$env{BUSNUM}/$env{DEVNUM}",
        RUN+="/bin/chmod 0666 %c"

```
sudo udevadm control –reload-rules
```

## Installer Altera Quartus sous Linux

Je viens de rencontrer quelques soucis mineurs à l’installation de ce logiciel. Je ne prétends pas avoir cerné tous les problèmes ni avoir les meilleures solutions qui soient, mais je vais tout de même noter ce qui m’a aidé...

* Le script d’installation est un `.sh`, mais il faut bien le lancer avec `/bin/bash ./blabla.sh`, sinon ça foire. Même comme ça, il finit par s’arrêter sur une erreur, après avoir décompressé ses fichiers dans un répertoire temporaire. Il suffit alors d’aller dans ledit répertoire et de lancer `/bin/bash ./setup.sh` ;
* J’ai installé le logiciel en `root` dans `/usr/share`. C’est peut-être la cause du problème suivant : Quartus ne semble pas apprécier être lancé via un lien symbolique venant d’un autre répertoire. Le `ln -s /.../quartus /usr/bin/quartus` ne fonctionne donc pas. J’ai plutôt créé un micro-script `/usr/bin/quartus` avec le contenu suivant :

  #!/bin/bash
  /bin/bash /usr/share/altera/.../quartus/bin/quartus

