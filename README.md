# cub3D

Moteur de rendu 3D par raycasting en C, dans l'esprit de Wolfenstein 3D.
Projet du cursus 42 Paris, fait en binôme avec Ali Siavoshi Fard
([@ft-Ali](https://github.com/ft-Ali)).

Le programme lit une carte `.cub`, vérifie qu'elle est valide, puis affiche
le labyrinthe en vue subjective : une texture par orientation de mur, une
couleur pour le sol et une pour le plafond, et des déplacements en temps réel
avec collisions.

## Compilation et lancement

Linux, avec les paquets de développement X11 :

```sh
sudo apt install libx11-dev libxext-dev libbsd-dev
make
./cub3D maps/good/subject_map.cub
```

Le premier `make` télécharge la [MiniLibX](https://github.com/42Paris/minilibx-linux)
de 42, la bibliothèque graphique imposée par le sujet.

## Contrôles

| Touche | Action |
|---|---|
| `W` `A` `S` `D` | avancer, aller à gauche, reculer, aller à droite |
| `←` `→` | tourner la caméra |
| `Échap` ou la croix | quitter |

## Le format `.cub`

```
NO textures/wolfenstein/grey_stone.xpm
SO textures/wolfenstein/purple_stone.xpm
WE textures/wolfenstein/red_brick.xpm
EA textures/wolfenstein/wood.xpm

F 220,100,0
C 225,30,0

        1111111111111111111111111
        1000000000110000000000001
        1011000001110000000000001
        1001000000000000000000001
111111111011000001110000000000001
100000000011000001110111111111111
11110111111111011100000010001
11110111111111011101010010001
1100000011010101110000000001
10000000000000001100000010001
10000000000000001101010010001
11000001110101011111011110N0111
11110111 1110101 101111010001
11111111 1111111 1111111111111
```

Quatre textures (nord, sud, ouest, est), la couleur du sol `F` et du plafond
`C` en RGB, puis la carte : `1` pour un mur, `0` pour le sol, et `N`, `S`, `E`
ou `W` pour la position et l'orientation de départ du joueur. La carte doit
être fermée par des murs.

Une carte invalide est refusée avec `Error` suivi de la raison, sur la sortie
d'erreur.

## Organisation

```
srcs/main.c          lancement, boucle d'événements de la MiniLibX
srcs/checker/        lecture et validation du fichier .cub
srcs/graphics/       raycasting, calcul vectoriel, textures
srcs/mov.c           déplacements et collisions
libft/               notre libft, avec get_next_line et ft_printf
```

## Crédits

Les cartes de test de `maps/` et les textures de `textures/` viennent de
[mcombeau/cub3D](https://github.com/mcombeau/cub3D). Les textures elles-mêmes
sont issues du pack Minecraft SimonKraft et de Wolfenstein 3D (id Software),
voir les README de chaque dossier.
