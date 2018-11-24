# Linux / Réseau

## Noms d’interfaces wifi trop longs : `aborting authentication by local choice ` et `DEAUTH_LEAVING`

Sous un Linux utilisant systemd, une interface wifi peut échouer à se connecter en restant un moment au stade « configuration de l’interface » (tel qu’affiché dans les widgets francophones de NetworkManager). Dans `/var/log/syslog`, on peut voir des choses du genre :

```
kernel: [  57.123456] wlx00c0ca82e172: aborting authentication with xx:xx:xx:xx:xx:xx by local choice (Reason: 3=DEAUTH_LEAVING)
```

Dans certains cas, la cause du problème est simplement le nom d’interface à rallonge débile choisi par ce demeuré de systemd (`wlx00c0ca82e172`).
On peut forcer systemd à revenir à un nom d’interface plus court (du genre `wlan0`) de cette manière :

```bash
ln -s /dev/null /etc/systemd/network/99-default.link
```

Un redémarrage est ensuite (sans doute) nécessaire.

Source : [Stretch wifi error](https://www.reddit.com/r/debian/comments/5tdp8q/stretch_wifi_error/)

## Capturer les trames d'administration wifi

Avant de collecter ces trames, par exemple pour récupérer les trames *probe request*, il faut d’abord passer la carte wifi en mode *monitoring*. Ça peut se faire avec `airmon-ng` (`airmon-ng start wlan0`), ou bien sans :

```bash
sudo iw dev wlan0 interface add mon0 type monitor
ifconfig mon0 up
```

Puis capture, avec filtrage sur les trames de management :

```bash
tcpdump -i mon0 type mgt
```

Dans Wireshark, on peut ensuite filtrer le type de trame avec des filtres de type `wlan.fc.type_subtype eq n`, où n a la signification suivante :

* 0 : *Association request*
* 1 : *Association response*
* 4 : *Probe request*
* 5 : *Probe response*
* 8 : *Beacon*
* 11 : *Authentication*
* 12 : *Deauthentication*

