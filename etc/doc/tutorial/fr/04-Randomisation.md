4 Aléatoire

# Aléatoire

Une façon très intéressante de rendre votre musique plus intéressante
est d'utiliser des nombres aléatoires. Sonic Pi a de très bonnes
fonctionnalités pour rendre votre musique plus aléatoire, mais avant
de voir cela nous devont apprendre une vérité choquante : dans Sonic
Pi l'aléatoire n'est pas vraiment aléatoire. Mais qu'est-ce que cela
signifie ? Eh bien, voyons cela.

## Reproductibilité

Une fonction aléatoire très intéressante est `rrand` qui vous donne
une valeur aléatoire entre deux nombres - un *minimum* et un
*maximum*. (`rrand` est une abbréviation de 'ranged random' :
aléatoire dans un intervalle). Essayons de jouer une note aléatoire :

```
play rrand(50, 100)
```

Oh, ça a joué une note aléatoire. Ca a joué la note `77.4407`. Une
bonne note bien aléatoire entre 50 et 100. Oh, attendez, est-ce que
j'ai prédit exactement la note aléatoire que vous avez eue aussi ? Il
y a quelque chose de louche ici.  Essayons d'exécuter le code de
nouveau. Comment ? Ca a joué `77.4407` de nouveau ? Ca ne peut pas
être aléatoire !

La réponse est que ce n'est pas vraiment aléatoire, c'est
pseudo-aléatoire. Sonic Pi vous donne des nombres semblant
aléatoires d'une manière répétable. C'est très utile pour s'assurer
que la musique que vous créez sur votre machine sonne de la même
manière sur les machines de tout le monde, même si vous utilisez de
l'aléatoire dans votre composition.

Bien sûr, dans un morceau donné, si on choisissait aléatoirement
`77.4407` tout le temps, ce ne serait pas très intéressant. Mais ce
n'est pas la cas. Essayons ceci :

```
loop do
  play rrand(50, 100)
  sleep 0.5
end 
```

Oui ! Ca a enfin l'air aléatoire. Pendant une *exécution* donnée, les
appels successifs aux fonctions aléatoires retourneront des valeurs
aléatoires. Mais la prochaine exécution produira exactement la même
séquence de valeurs aléatoires et sonnera exactement pareil. C'est
comme si le code de Sonic Pi voyageait dans le temps chaque fois qu'on
clique sur le bouton 'Run'. C'est le 'Un Jour sans fin' de la
synthèse musicale !

## Cloches hantées

Un bel exemple de nombres aléatoires en action est l'exemple des
cloches hantées qui lance en boucle le sample `:perc_bell` à une
vitesse aléatoire et attend une durée aléatoire entre chaque son de
cloche :

```
loop do
  sample :perc_bell, rate: (rrand 0.125, 1.5)
  sleep rrand(0.2, 2)
end
```

## Coupure aléatoire

Un autre exemple amusant est de modifier la coupure d'un synthé de
manière aléatoire. Un super synthé pour essayer ceci est l'émulateur
`:tb303` :

```
use_synth :tb303

loop do
  play 50, release: 0.1, cutoff: rrand(60, 120)
  sleep 0.125
end
```

## Graines aléatoires

Vous n'aimez pas la séquence particulière de nombres aléatoires que
Sonic Pi propose ? Eh bien il est tout à fait possible de choisir un
point de départ différent via `use_random_seed`. La graine par défaut
vaut 0, en choisissant une autre graine vous aurez une autre
expérience aléatoire !

Considérons ceci :

```
5.times do
  play rrand(50, 100)
  sleep 0.5
end
```

Chaque fois que vous exécutez ce code, vous entendrez la même séquence
de 5 notes. Pour obtenir une séquence différente il suffit de changer
la graine :

```
use_random_seed 40
5.times do
  play rrand(50, 100)
  sleep 0.5
end
```

Ceci produira une différente séquence de 5 notes. En changeant la
graine et en écoutant le résultat vous pouvez trouver quelque chose
qui vous plaît. Et quand vous partagerez le code, tout le monde
entendra exactement la même chose.

Regardons d'autres fonctions aléatoires utiles.


## choose

Une chose qu'on fait souvent est de choisir un élément au hasard dans
une liste d'éléments connus. Par exemple, je peux vouloir jouer une
note parmi celles-ci : 60, 65 ou 72. Je peux utiliser pour ceci
`choose` qui me permet de choisir un élément dans une liste. D'abord
je dois mettre mes nombres dans une liste en les entourant par des
crochets et en les séparant par des virgules : `[60, 65, 72]`. Ensuite
je peux juste les passer à `choose` :

```
choose([60, 65, 72])
```

Ecoutons comment ça sonne :

```
loop do
  play choose([60, 65, 72])
  sleep 1
end
```

## rrand

Nous avons déjà vu `rrand`, mais révisons un peu. Cette fonction
retourne un nombre aléatoire entre deux valeurs exclusives. Cela
signifie qu'elle ne retournera jamais la borne du haut ou du bas :
toujours quelque chose entre les deux. Le nombre sera toujours
décimal : ce ne sera pas un nombre entier mais une fraction. Voici
quelques exemples de décimaux retournés par `rrand(20, 110)` :

* 20.343235
* 42.324324
* 100.93423

## rrand_i

De temps en temps on a besoin d'un nombre entier aléatoire, pas un
décimal. `rrand_i` vient à notre aide ici. Elle fonctionne de manière
similaire à `rrand` mais elle peut retourner la borne inférieure et
supérieure (elle est inclusive au lieu de exclusive). Voici des
exemples de nombres retournés par `rrand_i(20, 110)` :

* 20
* 46
* 99

## rand

Cette fonction retourne un décimal aléatoire entre 0 (inclus) et la
valeur maximale que l'on spécifie (exclue). Par défaut elle retourne
une valeur entre 0 et un. Elle est donc utile pour choisir des valeurs
aléatoires de `amp:` :

```
loop do
  play 60, amp: rand
  sleep 0.25
end
```

## rand_i

Similairement à ce qu'on a vu sur la relation entre `rrand_i` et
`rrand`, `rand_i` retourne un nombre entier entre 0 et la valeur
maximale spécifiée.

## dice

Parfois on a envie d'émuler un lancer de dé : c'est un cas particulier
de `rrand_i` où la valeur minimale est toujours 1. Un appel à `dice`
vous demande de spécifier le nombre de faces du dé. Un dé standard a 6
faces, donc `dice(6)` agira de manière semblable : elle retournera une
valeur parmi 1, 2, 3, 4, 5 et 6.  Cependant, comme dans des jeux de
rôles, vous pouvez trouver utile d'avoir un dé à 4 faces, ou à 12
faces, ou à 20 faces, parfois même à 120 faces !

## one_in

Enfin on peut avoir envie d'émuler le fait de lancer le dé et
d'obtenir la face avec la plus grande valeur, comme 6 dans un dé
standard. `one_in` retourne `true` (vrai) avec une probabilité de un
sur le nombre de faces du dé. Ainsi `one_in(6)` retournera `true` avec
une probabilité de 1 sur 6 et `false` (faux) dans les autres cas. Les
valeurs `true` et `false` sont très utiles dans les conditions `if`
que nous couvrirons dans une section ultérieure de ce tutoriel.

Maintenant allez secouer un peu votre code avec des nombres
aléatoires !
