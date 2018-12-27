# MySQL

## Réinitialiser le mot de passe `root` de MySQL

Voici la manip à suivre si vous avez oublié le mot de passe `root` de votre serveur MySQL, et que bien sûr vous avez un accès administrateur sur le système d’exploitation du serveur (ici un Linux).

```
systemctl stop mysql
mysqld_safe --skip-grant-tables &
mysql -u root
mysql> use mysql;
mysql> update user set password=PASSWORD("nouveauMotDePasse") where User='root';
mysql> flush privileges;
mysql> quit
systemctl start mysql
```

Et voilà !
