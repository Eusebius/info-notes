# Linux / bash

## Copier une arborescence en préservant les *hardlinks*

Si on veut uniquement préserver les hardlinks :

```bash
cp --preserve=links src dest
```

Si on veut préserver tous les attributs possibles :

```bash
cp -a src dest
```

Il y a aussi une option `‐‐hard‐links` (ou `‐H`) dans `rsync`.

Source : [files – How to copy directories with preserving hardlinks?](https://unix.stackexchange.com/questions/44247/how-to-copy-directories-with-preserving-hardlinks)

## Corriger le fonctionnement de l'autocomplétion (espace supplémentaire)

Dans certaines distributions, il y a un bug dans le fichier de paramétrage de l’auto-complétion de bash, qui fait que des commandes comme `ls` ajoutent une espace au lieu d’un slash à la fin de la chaîne.

Le bug se corrige facilement en replaçant `-o default` par `-o filenames` à la ligne 1587 du fichier `/etc/bash_completion`.

Source : [Bash completion add extra space char](https://answers.launchpad.net/ubuntu/+source/bash-completion/+question/155411)

## Convertir l'encodage de fichiers (`.tex` par exemple)

Pour convertir de `Latin1` en `UTF-8` tous les fichiers `*.tex` du répertoire courant :

```bash
for i in *.tex; \
  do iconv -f iso8859-1 -t utf8 $i -o utf_$i; \
  rm $i; \
  mv utf_$i $i; \
done
```
