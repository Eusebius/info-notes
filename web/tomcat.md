# Tomcat

## Accéder aux application `manager` et `host-manager` après l’installation de Tomcat

Après une installation standard de Tomcat et de ses outils d’administration (packages `tomcat7` et `tomcat7-admin`), les applications `manager` et `host-manager` sont disponibles, respectivement, sur `/manager/html` et `/host-manager/html` (port 8080 par défaut). Par défaut, aucun utilisateur ne peut y accéder. Il faut pour cela éditer le fichier `tomcat-users.xml` (dans `/etc/tomcat/` sous Linux) pour y ajouter les utilisateurs et les rôles qui vont bien. Un utilisateur du groupe `manager-gui` peut accéder à l’application `manager`, un utilisateur du groupe `admin-gui` peut accéder à l’application `host-manager` ([plus de détails ici](http://tomcat.apache.org/migration-7.html#Manager_application)). Attention, les rôles affichés dans la page d’accueil de Tomcat7 ne sont pas à jour !

```XML
<tomcat-users>
  <role rolename="manager-gui"/>
  <role rolename="admin-gui"/>
  <user username="login" password="password"
      roles="manager-gui,admin-gui"/>
</tomcat-users>
```
