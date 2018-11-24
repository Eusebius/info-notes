# LaTeX

## Texte barré (*strikeout*)

```LaTeX
\usepackage{soul}
 
...
 
\st{texte barré}
```

## Beamer : gras + italique impossible

Il peut arriver, avec certaines configurations de paquetages LaTeX, que la composition gras+italique soit indisponible dans la fonte chargée. On peut trouver dans le fichier `.log` des avertissements du type `Font shape 'T1/aess/bx/it' undefined`. Les polices de type AE (Almost European) semblent présenter cette lacune.

On s’en sort en ajoutant un `\usepackage{lmodern}` après les chargements de paquets qui imposent des polices.

## Prendre en compte les nouveaux fichiers `.sty`

Lorsqu’on ajoute des fichiers `*.sty` dans l’arborescence TeX, ils ne sont pas pris en compte tout de suite. La compilation d’un document LaTeX utilisant ce fichier de style débouche sur une erreur du type `file *.sty not found`. Pour régler le problème, il suffit de lancer la commande `texhash` (ou `sudo texhash` si c’est root qui a installé le fichier `*.sty`).
