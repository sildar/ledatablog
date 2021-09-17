---
layout: post
title:  "Visualisation : faire passer un message avec la data"
categories: Data Visualisation Covid
excerpt: "Comment faire passer différents messages via la data. Exemple au travers d'une carte publiée par l'INSEE et d'une version alternative dans le contexte du covid-19."
thumbnail: '2choro.png'
thumbalt: "deux cartes juxtaposées montrant l'avant et l'après"
closingthumb: 'cat07.jpg'
closingthumbdesc: "Chat en attente d'un jeu de plateau !"
sharethumb: '/images/content/2choro.png'
---

Avoir des données c'est bien. Les enrichir, les étendre, s'en servir pour faire de la prédiction, c'est mieux. Mais ce n'est souvent pas suffisant.
Pour que la donnée serve vraiment, il faut qu'elle nous apprenne, à nous humains, à mieux comprendre les phénomènes qui nous entourent.
La visualisation joue un rôle crucial à cet étape, et il existe des dizaines de façons de représenter la donnée, des "camemberts" aux [diagrammes de Sankey](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Energy_US_2015.png/1920px-Energy_US_2015.png).
Le but d'une visualisation est le plus souvent de faire passer un message, et de multiples paramètres existent pour donner forme à ce message : choix de la représentation, couleurs, seuils, ...

Je vous propose aujourd'hui de nous attarder sur un format particulier : les choroplèthes. Derrière ce nom un peu barbare ce cache un type de visualisation familier de tous : les cartes colorées.
Dans le contexte actuel de covid, nous allons regarder une [carte fournie par l'INSEE le 12 Mai 2020](https://insee.fr/fr/statistiques/4488433#consulter), qui montre la surmortalité dans chaque département français en mars et avril 2020.
On va d'abord lire "naïvement" cette carte, chercher à en tirer les principaux enseignements sans regarder les données exactes qui ont servi à la générer (et que l'INSEE rend disponible par ailleurs).
Nous iront ensuite regarder de plus près les données afin de vérifier que les intuitions que la carte nous a donné sont exactes.
Enfin, nous verrons comment, à partir des mêmes données, nous pouvons générer une carte différente, qui fait passer un message complètement différent, sans pour autant être déloyal.


# La carte de la surmortalité covid-19 en France

Sans plus attendre, jetons un oeil à la carte de l'INSEE. On va ensuite séparer sa lecture en deux phases : une lecture générale (légende, couleurs, ...) et une lecture de compréhension (ce que la carte nous apprend).

![Carte INSEE sur la surmortalité covid-19 en Mars-Avril 2019](/images/content/surmortalite_insee.png){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}

## Informations générales

Il s'agit donc d'un choroplèthe avec 4 couleurs, allant du bleu clair au rouge, une échelle "froid-chaud" dont on peut deviner sans avoir à lire la légende que les zones "froides" (bleues) sont celles avec une mortalité faible, et que plus on tire vers le rouge, plus la mortalité est élevée.
Les couleurs sont appliquées sur les départements, les outre-mer sont bien présents, et on a, comme souvent, un zoom sur le centre de l'Île de France pour pouvoir constater les différences entre les trois départements entourant Paris : le Val de Marne, la Seine Saint Denis, et les Hauts de Seine.

L'échelle semble logique, avec la couleur bleue appliquée aux départements ayant une surmortalité négative ("moins de 1.0"), c'est à dire qu'il y a moins de décès que d'habitude, du orange clair vers le rouge pour les départements où la surmortalité est positive.
Le rouge est réservé aux départements où le nombre de décès est à 200% ou plus, c'est à dire que la mortalité y a plus que doublé.

La période considérée va du 2 mars au 19 avril 2020, et la surmortalité est logiquement comparée à la moyenne des décès dans chaque département entre 2015 et 2019 sur les mêmes mois.

La carte est par ailleurs accompagnée [sur la page de l'INSEE](https://insee.fr/fr/statistiques/4488433#consulter) d'autres graphiques présentant la surmortalité sous différentes formes. On peut notamment mentionner une série de cartes montrant l'évolution hebdomadaire du 2 mars au 13 avril.
Plusieurs paragraphes d'explications sont également présents, détaillants quelques chiffres et apportant des précisions. On y apprend par exemple qu'on décompte environ 22 140 décès supplémentaires sur la période étudiée par rapport à la normale.


## Ce que la carte nous apprend

Commençons par ce qui saute aux yeux, grâce aux couleurs : la surmortalité est très importante dans deux régions : l'Île de France et l'Alsace, avec des débords sur certains départements limitrophes (Doubs, Vosges, et Moselle à l'Est, Oise à proximité de l'Île de France).
**La situation est particulièrement alarmante autour de Paris (les trois départements limitrophes et le Val d'Oise), alors que la capitale elle-même est un peu moins touchée.**
5 départements seulement sont rouges, ils sont particulièrement impactés par la surmortalité (Val de Marne, Seine Saint Denis, Hauts de Seine, Val d'Oise, Haut-Rhin).

Le reste de la France est plutôt légèrement touché, avec du orange clair presque partout.

On note cependant quelques départements épargnés, avec une mortalité qui est même inférieure à la moyenne.
On peut imaginer plusieurs raisons à cela : une plus faible mortalité sur les routes, des variations statistiques, etc...
Côté outre-mers, la situation semble assez stable, à l'exception de Mayotte qui semble plus touchée.

On peut résumer les enseignements tirés à la liste suivante : 

* Deux régions sont particulièrement concernées : l'Alsace et l'Île de France
* Paris est relativement épargnée par rapport à la petite couronne (Val de Marne, Seine Saint Denis et Hauts de Seine)
* 5 Départements sont extrêmement touchés (Val de Marne, Seine Saint Denis, Hauts de Seine, Val d'Oise, Haut-Rhin)
* La situation est plutôt homogène sur le reste du territoire avec une surmortalité faible mais présente
* Pour une quinzaine de départements, le confinement a permis un recul de la mortalité par rapport à la situation normale

Plongeons maintenant dans les données afin de vérifier ces différents éléments.

![Plongée dans les données](/images/content/diveinto.jpg){:style="display: block; margin-left: auto; margin-right: auto; width: 50%"}

---

# Plongée dans les données

On va maintenant vérifier si les informations communiquées par la carte de l'INSEE se confirment dans le détail des données.
On va donc reprendre tour à tour les cinq enseignements tirés plus tôt et chercher si ils tiennent bien la route à l'épreuve du détail.


* **Deux régions sont particulièrement touchées : l'Alsace et l'Île de France**

C'est vrai.
En ce qui concerne l'Île de France, à l'exception de la Seine-et-Marne qui affiche 61% de surmortalité (1.61), les autres départements de la région sont à plus de 74% de surmortalité (1.74), ce qui les distingue du reste de l'hexagone.
Pour l'Alsace et ses départements limitrophes, cela se confirme également, avec deux nuances : le Doubs est moins impacté que les autres avec 54% de surmortalité, il passe de justesse dans la catégorie orange sombre.
La Moselle à 61% de surmortalité est également en deça des autres départements orange sombre.

On entend depuis plusieurs semaines que ces deux régions sont les deux foyers principaux de l'épidémie, cette carte et les données qui l'accompagnent le confirment, rien de vraiment surprenant donc.

* **Paris est relativement épargnée par rapport à la petite couronne**

Malheureusement, par le biais du zoom et des couleurs, c'est là l'un des éléments qui saute le plus aux yeux lorsque l'on regarde la carte, alors que cette conclusion est assez fausse.
Voici les chiffres pour les 4 départements :

Département | Mortalité
--- | ---
Paris |	1,98
Val-de-Marne | 2,05
Val-d'Oise | 2,10
Seine-Saint-Denis | **2,34**

Ce qu'on remarque surtout à la lecture de ces chiffres, c'est que la Seine-Saint-Denis a une surmortalité très éloignée des trois autres départements, et que Paris est très similaire au Val-de-Marne et au Val-d'Oise.
La conclusion que nous avions tirée d'un Paris relativement épargné par rapport à la petite couronne est donc fausse, on pourrait plutôt dire que la Seine-Saint-Denis est un département particulièrement touché.

* **5 Départements sont extrêmement touchés**

Comme on vient de le voir, c'est plutôt faux en ce qui concerne le Val-de-Marne et le Val-d'Oise, sauf à y rajouter Paris. Si on regarde les 5 départements les plus touchés et les 5 qui les suivent, on obtient :


Département | Mortalité
--- | ---
Haut-Rhin | **2,48**
Seine-Saint-Denis | **2,34**
Val-d'Oise | 2,10
Val-de-Marne | 2,05
Hauts-de-Seine | 2,04
Paris |	1,98
Essonne | 1,82
Yvelines | 1,74
Vosges | 1,72
Bas-Rhin | 1,70


On y voit plutôt une démarcation différente : deux départements très fortement touchés à savoir le Haut-Rhin et la Seine-Saint-Denis, quatre département fortement touchés (Val-d'Oise, Val-de-Marne, Hauts-de-Seine, Paris), l'Essonne dans une position intermédiaire, puis les départements un peu moins touchés.


* **La situation est plutôt homogène sur le reste du territoire avec une surmortalité faible mais présente**

La problématique ici est que les seuils choisis, de 1.0 à 1.5, comprennent à la fois des départements avec une quasi-absence de surmortalité, et des départements à la surmortalité forte.
Pour entrer dans le détail, on compte en orange clair pas moins de 30 départements avec une surmortalité inférieure à 10%, autant dire qu'il est difficile de conclure à une incidence significative du virus sur ces départements.
A tout le moins faudrait-il aller dans le détail, montrer que la mortalité a reculé par ailleurs (par exemple moins d'accidents, moins de pollution entraînant des troubles respiratoires, moins d'accidents du travail, ...) pour pouvoir conclure qu'une surmortalité de 10% est significative.

Dans la même catégorie, on trouve le Rhône et sa surmortalité de 48%. Ce genre d'effets de seuil arrive dans la quasi-totalité des choroplètes, il est impossible de trouver un seuil évitant cet inconvénient.
Néanmoins, on mélange ici des réalités très différentes.

* **Pour une quinzaine de départements, le confinement a permis un recul de la mortalité par rapport à la situation normale**

Encore une fois, l'effet de seuil à 1 mélange ce qui n'est probablement qu'anomalies statistiques avec la haute-Vienne à 0.99, et des données plus surprenantes, qu'il faudrait probablement fouiller pour mieux les comprendre (Tarn-et-Garonne ou Guyane à 0.83 par exemple).

---

# Construction d'une carte alternative

Lançons nous dans la construction d'une carte alternative.
Pour cela, on va énoncer les propriétés qu'on souhaite qu'elle ait, c'est à dire les messages qu'elle renverra.
Une fois les messages décidés, nous verrons quels seuils appliquer pour répondre aux mieux à nos besoins.

## Les messages à envoyer

On a vu que deux départements ont une mortalité très importante : le Haut-Rhin et la Seine-Saint-Denis.
On fera donc en sorte de leur consacrer une catégorie.

* **Mettre en avant la forte surmortalité en Haut-Rhin et Seine-Saint-Denis**

On a ensuite vu que plusieurs départements avaient des mortalités très proches de l'habituel, soit juste au dessus, soit juste en dessous. On ne peut pas vraiment les mettre dans l'une ou l'autre des catégories (hausse ou baisse), on va donc essayer de les mettre à part.

* **Pouvoir identifier les zones où la mortalité n'est pas très différente de d'habitude**

Quelques rares départements enregistrent un recul net de la mortalité. Montrons les.

* **Mettre en avant les départements où il y a un recul de la mortalité**

Enfin, il y a différents degrés de surmortalité. Mettre ensemble des départements avec une hausse de 20% ou une hausse de 80% n'aurait pas de sens.

* **Séparer en plusieurs catégories en fonction de la hausse de mortalité**

Maintenant que nous sommes au clair sur les messages que l'on veut transmettre, cherchons les paramètres qui permettront de construire cette carte.

## Choix des paramètres

On pourrait utiliser divers méthodes statistiques pour trouver "les meilleurs" seuils.
On s'expose néanmoins dans ce cas à donner l'impression que les seuils sont trop artificiels, qu'ils ont été créés spécifiquement pour tordre la réalité.
Ici, on cherche plutôt à trouver des seuils cohérents, sans pour autant les rendre artificiel, et on va donc réfléchir de manière fonctionnelle et par élimination.

* **Pouvoir identifier les zones où la mortalité n'est pas très différente de d'habitude**

Pour ce premier élément, on va vouloir choisir un seuil bas et un seuil haut entre lesquels on déterminera que la mortalité est "normale".
On va vouloir centrer ces valeurs autour de 1.0 afin de ne pas donner l'impression de seuils artificiels (on ne va pas choisir 0.85/1.13 par exemple).
Sans être spécialiste de l'analyse de mortalités, une variation de plus ou moins 10% autour de la moyenne ne me semble pas très probante. On peut donc décider de place ces seuils à 0.90-1.10.
Les départements ayant une mortalité dans cette zone seront affichés dans un bleu très pâle. En effet, le blanc est plus généralement représentatif de l'absence de données que de la neutralité.

* **Mettre en avant les départements où il y a un recul de la mortalité**

On a déjà répondu à ce besoin avec notre seuil à 0.90 défini juste au dessus.
Les départements en dessous de ce seuil seront donc indiqués en vert afin de communiquer l'aspect positif. On gardera le rouge/orange pour les endroits où la mortalité à augmenté, comme dans la carte originelle.

* **Mettre en avant la forte surmortalité en Haut-Rhin et Seine-Saint-Denis**

On a vu plus haut que ces deux départements avaient des chiffres très élevés. On peut les rappeler, avec les deux départements suivants en terme de mortalité :

Département | Mortalité
--- | ---
Haut-Rhin | **2,48**
Seine-Saint-Denis | **2,34**
Val-d'Oise | 2,10
Val-de-Marne | 2,05

Ici, on va choisir donc un seuil entre 2.10 (Val-d'Oise) et 2.34 (Seine-Saint-Denis). On sélectionne 2.20. C'est une valeur centrale, ronde, à peu près entre deux valeurs.

* Séparer en plusieurs catégories en fonction de la hausse de mortalité

Ici il y a davantage d'arbitraire. On peut choisir le nombre de couleurs et les seuils de plusieurs façons.
Les seuils existants à cette étape sont 0.90-1.10-?-2.20. J'ai choisi les seuils 1.40 et 1.70 afin d'avoir un pas de 0.30 pour les valeurs allant de 1.10 à 1.70.

## La carte

Voici le choroplèthe obtenu.

![Carte choroplèthe obtenue](/images/content/choroplethe.png){:style="display: block; margin-left: auto; margin-right: auto; width: 70%"}

La lecture de cette carte n'est pas du tout la même que celle de la carte originelle.
La première chose qui saute aux yeux, c'est que près d'un tiers des départements n'a pas vu de hausse sensible de la mortalité.
**Cela ne veut pas dire que le covid n'a pas tué dans ces régions**, la faible hausse pouvant être dûe à certains facteurs allant à la baisse (mortalité routière, accidents au travail, ...).

Le second élément visible est le fait que tout l'est de la france, ainsi qu'un axe Nantes-Bruxelles, sont concernés. A l'inverse, le sud-ouest et la Bretagne sont globalement épargnés.

Enfin, on remarque bien que l'Alsace et la région parisienne sont particulièrement touchées, et davantage encore la Seine-Saint-Denis et le Haut-Rhin qui paient le plus lourd tribut.

---

# Conclusion

Les choroplèthes sont des visualisations ingrates. Il faut nécessairement choisir des seuils, et ceux-ci ne peuvent jamais être parfaits.
Il faut donc les choisir en fonction du message que l'on cherche à faire passer pour accentuer ou atténuer certains aspects que l'on trouve peut pertinent.

Dans le cas de la carte de l'INSEE, le choix des seuils peut selon moi s'expliquer par deux éléments : montrer que l'essentiel de la France est impacté, même sensiblement (choix de colorer en orange tout ce qui est supérieur 1.0).
Cela amplifie le message donné par ailleurs de 22 000 morts supplémentaires en France. Le second choix compréhensible est d'utiliser des nombres simples comme seuils : 1.0, 1.5, 2.0.
Il est alors difficile de leur reprocher d'avoir joué avec les seuils pour trafiquer la perception que l'on peut avoir.

Ici, je suis en désaccord avec ce dernier choix car il nous fait tirer de mauvaises conclusions lors d'une lecture rapide.
Fort heureusement, les données et les textes associés à cette carte sur le site de l'INSEE ainsi que le fait qu'elle soit interactive et permette de voir les chiffres au survol d'un département.
Cela permet d'apporter nuances et informations complémentaires, ce qui n'est pour ainsi dire jamais le cas lorsque la carte est partagée sur des réseaux sociaux ou commentée sur les plateaux TV.


![Comparaison des deux cartes](/images/content/2choro.png){:style="display: block; margin-left: auto; margin-right: auto; width: 70%"}
<figcaption>Comparaison des deux cartes</figcaption>

---


