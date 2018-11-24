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

