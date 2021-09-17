---
layout: post
title:  "Les 5 étapes d'un projet d'Intelligence Artificielle"
categories: Data IA
excerpt: "Les projets data et IA peuvent durer de quelques semaines à quelques mois. Comment s'organiser pour mener à bien de tels projets et avec quels jalons ?"
thumbnail: 'project_planning.jpg'
thumbalt: 'un graphe de projet'
closingthumb: 'cat05.jpg'
closingthumbdesc: "Un projet bien préparé est un projet serein... comme mon chat !"
---

Le développement d'un algorithme d'intelligence artificielle, qu'il s'agisse de traitement des langues, d'analyse d'images, de classification ou de prédiction, répond à des exigences similaires à celles d'un développement informatique classique.
Il diffère néanmoins par une estimation de la faisabilité souvent moins robuste et un temps de construction souvent plus long et plus difficile à prédire précisément.

Qu'ils soient entrepris en interne ou pour le compte d'un client, la plupart des projets d'IA peuvent suivre un plan en cinq étapes, de l'analyse du besoin à l'exploitation.

Avant de décrire ces cinq étapes, faisons un détour par un cas trop fréquemment rencontré, le projet en une unique étape.

# Le projet en 1 étape, ou la meilleure façon de planter un projet

Qui s'imaginerait donner à un excellent cuisinier des ingrédients dont il ne connaît ni la provenance ni la qualité, une plaque de cuisson au gaz alors qu'il n'utilise que l'électrique et des ustensiles exotiques, tout en "l'aidant" en lui fournissant une recette dirigiste dont il ne pourra pas s'écarter, et espérer dans le même temps obtenir un plat d'exception ?

Étrangement, il est fréquent pour les informaticiens d'être confrontés à cette situation avec des cahiers des charges techniques très précis, dont les méthodes et outils sont imposés, mais dont les objectifs finaux ne peuvent être devinés qu'entre les lignes. Si certains projet simples peuvent parfois réussir avec cette approche, les projets d'IA, plus sensibles, y échouent presque systématiquement.

Le projet en une étape consiste à faire intervenir le spécialiste en développement d'IA en lui fournissant une vue très superficielle de la problématique ("nous devons faire augmenter telle valeur"), et en lui expliquant par quel moyen il doit résoudre le problème ("j'ai entendu dire que les RNN étaient très efficaces, je veux que vous les testiez sur ce cas d'usage") et avec quelles données. Il n'a pas à comprendre, simplement à faire.

Une personne à qui vous confiez la tâche de manipuler des données complexes, d'architecturer des réseaux de neurones innovants et d'évaluer précisément leurs résultats doit avoir l'intelligence nécessaire à la compréhension du problème que vous tentez de résoudre et à la sélection des outils les plus appropriés.

Les projets d'Intelligences Artificielles sont encore plus sensibles à ce besoin d'informations : les données d'entrées sont souvent complexes et peu documentées, leur variété sous-estimée ; les objectifs finaux pas toujours clairs même pour le donneur d'ordres et les outils très rarement maîtrisés par le demandeur.

Le projet en 1 étape n'aboutit que rarement. Parfois l'approche choisie ne fonctionnera pas, sans que personne ne comprenne vraiment pourquoi ("normalement ça aurait dû fonctionner"). Parfois, malgré de bons résultats, l'IA ne sera pas utilisée ("la solution temporaire mise en place le temps que le projet aboutisse est finalement peu coûteuse et efficace"). Pire, parfois elle sera utilisée malgré des biais non identifiés, une performance mal évaluée, menant à la fois à un effet déceptif sur les technologies employées ("L'IA c'est du vent") et à un risque important (utilisation contre-productive).


# Les 5 étapes d'un projet réussi

Si un projet peut généralement être résumé à trois étapes : étude, construction et exploitation, on se propose ici de le découper en cinq : analyse du besoin, analyse et préparation des données, construction d'une baseline, construction et évaluation de l'algorithme, et enfin bilans et clôture.

![Les 5 étapes décrites dans ce post](/images/content/5steps.png){:style="display: block; margin-left: auto; margin-right: auto; width: 80%"}

Ces étapes sont conçues pour permettre une sortie "sans regrets" à la fin de chacune d'entre elle, dans l'objectif de minimiser les pertes en cas d'échec et de pouvoir capitaliser sur l'expérience acquise en cas de succès.

## 1. Analyser le besoin

Comme pour tout projet, l'étape d'analyse est très souvent la plus négligée, alors qu'il s'agit de l'étape la plus critique. Bien comprendre un problème, c'est déjà le résoudre à moitié.

Cela inclut les raisons pour lesquelles le besoin existe et en quoi il n'est pas satisfait aujourd'hui, les tentatives précédentes pour y répondre, la façon dont il est traité aujourd'hui, les différents acteurs qui sont intervenus, interviennent et interviendront dessus, ...
C'est aussi la délimitation des données et cas d'usages concernés par le projet.
C'est enfin la définition de métriques claires sur lesquelles le succès ou l'échec du projet pourra être évalué.

Ce n'est qu'à l'issue de cette étape que sont réalisables les estimations de faisabilité et de temps nécessaire au projet. L'ensemble des informations récoltées à cette étape doit faire l'objet d'un rapport listant notamment les livrables attendus et les risques anticipés.

## 2. Préparer les données

Il est très fréquent que la qualité et le volume de données disponibles soient surestimés par les donneurs d'ordre.
L'étape de préparation des données, indispensable de toute manière pour chaque projet data, est l'occasion de vérifier l'essentiel des prérequis exposés dans l'expression de besoin.
L'analyse statistique des données permettra ainsi de valider la fiabilité, de lever les doutes sur la faisabilité, d'exposer les imprécisions et les biais qui risquent d'être posés en aval, de s'assurer que l'intégralité des cas d'usages sont couverts par la donnée.

C'est un moment sur lequel il est facile de passer trop rapidement : les étapes intéressantes se trouvent juste après et tout le monde a hâte d'obtenir des premiers résultats tangibles.
Or, une analyse froide avant l'obtention de tout résultat permet d'anticiper la plupart des problèmes, de les prévenir et de vérifier lors des étapes suivantes si ces problèmes surviennent ou non.
On est alors sur une pente ascendante : prudence et alertes en début de projet, levée des doutes et résultats certifiés en fin de projet.
Le risque d'une analyse trop rapide est d'engendrer au contraire une pente descendante : engouement en début de projet, premiers résultats prometteurs suivis de la mise en évidence de tout un tas de biais tempérant largement les bons résultats.

Un projet réussi mené avec une pente ascendante laisse une bonne impression, un sentiment de maîtrise tout au long du projet, et l'assurance de résultats solides.
Un même projet aux résultats identiques mené avec une pente descendante laisse quant à lui planer le doute sur la fiabilité et laisse craindre l'existence de biais supplémentaires non identifiés, menant à une défiance importante et à un risque de non adoption de la solution.

Malheureusement, pour l'exécutant, la pente descendante est le pari le plus rentable à court terme : l'obtention de premiers résultats rapides, même s'il ne sont pas fiables, encourage les donneurs d'ordre à poursuivre le projet, tandis que la levée des incertitudes tôt dans le projet peut mener à un abandon prématuré.
Sur le long terme néanmoins, il est évident que la mémoire d'un projet ascendant encouragera le renouvellement de projets d'IA, tandis qu'un projet descendant ne sera probablement pas reconduit.

L'analyse des données doit venir confronter les attendus de l'expression de besoins en présentant de nouveaux risques non anticipés ou au contraire en validant la qualité attendue de la donnée à disposition.

Un bon moyen pour ne pas abandonner trop tôt un projet pour lequel des incertitudes planent consiste à constuire une baseline, un premier algorithme simpliste développé en quelques jours, qui permette de lever la plupart des craintes soulevées lors de la préparation des données. C'est d'ailleurs une étape qu'il est bon d'inclure dans tout projet d'IA.

## 3. Construire une baseline

Construire une baseline correspond à mettre en place un algorithme simple développé en quelques jours dont l'objectif est de vérifier d'une part la faisabilité globale du projet, et d'autre part à lever une partie des biais des données qui ont pu être identifiés plus tôt.
Il permet également de s'assurer que les données ont été correctement préparées et qu'elles sont suffisantes.
À l'issue de cette phase, plusieurs cas de figure peuvent se présenter :

* Des biais importants sont détectés dans les données, et il paraît compliqué de passer outre.
* La baseline donne des scores extrêmement faibles, laissant penser que la faisabilité du projet a été surestimée.
* La baseline obtient des résultats extrêmement élevés, il n'est donc pas nécessaire de développer un algorithme complexe.
* La baseline donne des résultats intermédiaires, insuffisants pour répondre aux besoins du projet.

Dans le premier cas, c'est à dire l'apparition ou la confirmation de biais importants, il est nécessaire de retravailler sur la donnée. En récupérer davantage, mieux la nettoyer, réevaluer le besoin afin de redéfinir le champ d'application, voire reporter le projet le temps d'avoir des données propres.

Dans le second cas, à savoir une baseline donnant des scores très faibles, le risque est que l'algorithme le plus efficace du monde ne parvienne pasnon plus à obtenir des résultats permettant de répondre au besoin. Une fois encore, il est alors nécessaire de rediscuter du besoin afin de s'attaquer potentiellement à un sous-problème. S'il n'est pas impossible de continuer malgré tout le projet, les risques de ne pas aboutir sont élevés.

Dans le troisème cas, où la baseline obtient des scores très élevés, il est possible de raccourcir le projet en sautant l'étape 4 et en passant directement à l'analyse et à la rédaction des rapports. S'il est décevant de devoir ignorer la partie la plus intéressante, celle du développement d'IA, les apports espérés ne valent certainement pas le temps qui y serait passé, sauf à compter sur des avantages connexes (familiarisation avec un technologie, communication, ...).

Enfin, le dernier cas est celui que l'on espère, qui conforte l'idée que le problème est solutionnable tout en ayant permis de lever des doutes sur les défauts éventuels de la donnée.

Dans tous les cas, cette étape est l'occasion de mettre à jour le rapport d'analyse des données.


## 4. Développer l'algorithme et l'évaluer

Il s'agit ici de la partie réellement intéressante pour le développeur d'intelligence artificielle. À cette étape, la plupart des craintes ont pu être levées, et la seule incertitude restante est la marge de progression entre la baseline et l'algorithme d'intelligence artificielle.
Cette étape peut représenter un temps conséquent d'autant plus qu'elle doit contenir une phase d'analyse précise des résultats montrant les forces et les faiblesses du système mis en place.

Elle aboutie à la rédaction d'un rapport technique, plus ou moins exhaustif selon les attentes.


## 5. Rédiger un bilan

Cette dernière étape, comme la première, est souvent trop négligée.
Or, un algorithme qui fonctionne parfaitement à la livraison peut tout à fait dériver peu à peu et baisser progressivement en performance.

L'une des principales causes potentielles à cette dérive est l'évolution des données : leur distribution change, leur définition même parfois.
Pour pouvoir dans le futur faire évoluer l'algorithme, il faut avant tout des rapports fonctionnels : quel problème devait être résolu, dans quelles conditions et sur quelles données ?
Comment a-t-il été résolu, avec quelle efficacité et quelles faiblesses ?
Comment la solution sera-t-elle utilisée, sous quelles contraintes ?

La documentation techique, bien qu'utile, est beaucoup moins sensible : son absence n'entraînera que des délais de mise à jour plus longs tandis que l'absence de documentation fonctionnelle risque de conduire la mise à jour à tomber dans les pièges soigneusement évités lors du projet initial.


# Conclusion

Les projets visant à construire une intelligence artificielle sont souvent risqués : les résultats sont incertains, la qualité des données quasi-systématiquement surestimée, les besoins pas toujours correctement définis.
Avoir une planification robuste avec des étapes permettant des sorties prématurées du projet, des opportunités de rediscuter les besoins et de lever progressivement les risques identifiés permet d'éviter tout un tas d'écueils, sans mentionner la sérénité associée.
