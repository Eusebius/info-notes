# Thunderbird

## Désactiver le blocage des contenus distants

Par défaut, Thunderbird ne télécharge pas les images dans les messages dont les expéditeurs ne sont pas dans le carnet d’adresse. Pour désactiver cette « fonctionnalité » (et donc lire ses mails normalement), il faut aller dans l’éditeur de configuration et passer manuellement la valeur de `mailnews.message_display.disable_remote_image` à `false`.

## Ajouter les flèches d’affichage des dossiers

Dans les versions antérieures de Thunderbird, il y avait en haut de la colonne d’affichage des dossiers deux flèches « gauche » et « droite » permettant de basculer entre l’affichage de toute l’arborescence, des dossiers récents, des dossiers préférés ou des dossiers contenant des messages non lus.

Dans leur grande sagesse, les développeurs de Thunderbird ont décidé que nous n’avions plus besoin de cette fonctionnalité. Il est toutefois possible de la restaurer (elle n’a été désactivée que par bêtise, pas par cruauté), en éditant le fichier `chrome/userChrome.css` dans le répertoire de profil de Thunderbird (au besoin, créer le répertoire et le fichier) et en y ajoutant la section suivante :

```CSS
#folderPaneHeader, #abDirTreeHeader {
  display: -moz-box !important;
}
```
