# Wireshark

## Linux : utiliser un utilisateur non `root` à utiliser Wireshark

* Lancez `sudo dpkg-reconfigure wireshark-common` pour autoriser les membres du groupe `wireshark` à écouter sur les interfaces ;
* Ajoutez l’utilisateur au groupe wireshark : `sudo usermod -a -G wireshark login`

