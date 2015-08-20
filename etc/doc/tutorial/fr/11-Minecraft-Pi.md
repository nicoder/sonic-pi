11 Minecraft Pi

# Minecraft Pi

Sonic Pi propose maintenant une API simple pour interagir avec
Minecraft Pi, l'édition spéciale de Minecraft qui est installée par
défaut sur Raspbian, le système d'exploitation basé sur Linux du
Raspberry Pi.

## Pas besoin d'importer de librairies

L'intégration avec Minecraft Pi est conçue pour être très facile à
utiliser. Tout ce dont vous avez besoin est de lancer Minecraft Pi et
de créer un monde. Vous pouvez ensuite utiliser les fonctions
commençant par `mc_` comme on utiliserait `play` et `synth`. Pas
besoin d'importer quelque chose ou d'installer des librairies, tout
est prêt à l'emploi.

## Connection automatique

L'API Minecraft Pi s'occupe de gérer votre connexion à l'application
Minecraft Pi. Cela signifie que vous ne devez vous soucier de rien. Si
vous essayez d'utiliser l'API Minecraft Pi et que Minecraft Pi n'est
pas ouvert, Sonic Pi vous le dira poliment. De même, si vous fermez
Minecraft Pi pendant qu'un `live_loop` qui utilise l'API est exécuté,
la boucle s'arrêtera et vous dira poliment qu'elle ne peut pas se
connecter. Pour se reconnecter, il suffit de relancer Minecraft Pi et
Sonic Pi le détectera automatiquement et créera une nouvelle connexion
pour vous.

## Conçu pour être codé de manière interactive

L'API Minecraft Pi a été conçue pour fonctionner sans problème dans
les `live_loop`s. Cela veut dire qu'il est possible de synchroniser
des modifications dans vos mondes Minecraft Pi avec vos sons Sonic Pi.
Des vidéos musicales instantanées basées sur Minecraft ! Notons
cependant que Minecraft Pi est un logiciel en version alpha et qu'on
lui connait quelques bugs. Si vous tombez sur des problèmes redémarrez
juste Minecraft Pi et continuez comme avant. La fonctionnalité de
connexion automatique de Sonic Pi gère bien cela.

## Nécessite un Raspberry Pi 2.0

Il est fortement recommandé d'utiliser un Raspberry 2 si vous voulez
utiliser Sonic Pi et Minecraft en même temps, surtout si vous voulez
exploiter les capacités sonores de Sonic Pi.

## Fonctionnalités de l'API

A ce point, Sonic Pi supporte des manipulations de base de blocs et de
joueurs qui sont détaillées dans la Section 11.1. Le support de
réaction à des événements déclenchés par des interactions de joueurs
dans le monde est prévu pour une future version.
