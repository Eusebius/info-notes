# Logiciels divers

## Subversion : ajouter récursivement des fichiers avec `svn add`

```bash
svn add ––depth=infinity ––force *
```

Si ça ne fonctionne pas, c’est peut-être pour des histoires de droits insuffisants (auquel cas il faudra un `mv` du répertoire en cause puis un `svn delete` pour régler le problème), ou bien parce qu’il reste un répertoire `.svn` qui ne devrait pas être là (et qui empêche l’ajout au système de gestion de versions).
