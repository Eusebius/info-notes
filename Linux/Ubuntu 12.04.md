 # Linux / Ubuntu 12.04

## Réactiver le clic à trois doigts sur un *touchpad*

Au passage à Ubuntu 12.04, le clic à trois doigts (bouton du milieu) s’est trouvé désactivé. On peut récupérer cette fonctionnalité avec les commandes de configuration suivantes (les valeurs initiales étaient à 0) :

```
synclient ClickFinger3=2
synclient TapButton3=2
```
