# MySQL

## Réinitialiser le mot de passe `root` de MySQL

Voici la manip à suivre si vous avez oublié le mot de passe `root` de votre serveur MySQL, et que bien sûr vous avez un accès administrateur sur le système d’exploitation du serveur (ici un Linux).

```
/etc/init.d/mysql stop
mysqld_safe --skip-grant-tables &
mysql -u root
mysql> use mysql;
mysql> update user set password=PASSWORD("nouveauMotDePasse") where User='root';
mysql> flush privileges;
mysql> quit
/etc/init.d/mysql restart
```

Et voilà !
