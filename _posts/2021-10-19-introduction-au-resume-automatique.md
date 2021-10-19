---
layout: post
title:  "Introduction au résumé automatique"
categories: IA NLP Python
excerpt: "Tour d'horizon du résumé automatique, une tâche classique du NLP."
thumbnail: 'computer_books.jpg'
thumbalt: "Un ordinateur et des livres"
closingthumb: 'catme.jpg'
closingthumbdesc: "Pour une fois, je pose avec mon chat."
sharethumb: ''
---

Le résumé automatique consiste à prendre un long texte, ou même un ensemble de textes, et à générer
de façon automatique un texte beaucoup plus court qui contient la majorité des informations. Simple ?
Pas tant que ça. D'abord, il faut se mettre d'accord sur quelles informations sont réellement importantes.
Ensuite, il faut pouvoir les extraire correctement, les réorganiser, le tout dans un texte grammatical et 
sans intervention humaine. Et c'est sans compter sur le grand nombre de variantes de types de résumés possibles !

J'ai pu travailler pendant environ un an sur cette thématique passionnante juste avant mon doctorat, ce billet est
donc l'occasion pour moi de me replonger dans ce sujet et de faire le point sur les dernières nouveautés du domaine.

Faisons donc un tour d'horizon de cette thématique, en commançant par décrire les différents types de résumés
qui existent, avant de s'attarder sur deux types de systèmes un peu plus en détails : ceux issus de l'IA et des réseaux 
de neurones, et ceux qui sont plutôt portés sur l'extraction optimale d'informations.

## Les différents types de résumé

Quand on parle de résumé, on pense souvent à la quatrième de couverture d'un livre ou à la description du 
scénario d'un film. Généralement, ils évitent de spoiler la fin, alors que c'est précisément ce qu'on demanderait
à un outil de résumé automatique classique : raconter l'intrigue, de sorte que le résumé puisse suffire pour connaître
l'essentiel. Ici, il s'agit de **résumés mono-document**, c'est à dire qu'on ne résume qu'un unique document (un film, un livre, un article, ...).

On pourrait au contraire vouloir un **résumé multi-documents**, qu'on rencontre plus fréquemment dans le cadre
de revues de presse : on veut disposer d'un condensé des informations les plus importantes telles que rapportées
par divers organismes de presse.

Une fois que l'on a décidé du type de données que l'on cherche à résumer, mono ou multi-documents, on a le choix entre
deux approches : l'**extractive**, qui consiste à extraire telles quelles des informations avant de les recoller pour créer
un résumé, et l'approche **générative**, qui consiste à créer de nouvelles phrases, qui n'apparaissent pas à l'origine dans les
documents, afin d'avoir un résumé plus fluide et plus libre.

En plus de ces critères, il existe divers styles de résumés, que nous n'aborderons pas ici : résumés de mise à jour qui
consistent à résumer les informations apparaissant dans un nouveau document et qui n'étaient pas recensées jusqu'ici, résumés
dirigés qui consistent à adopter un angle précis donné par l'utilisateur, ...

## L'IA et les réseaux de neurones révolutionnent le résumé automatique

Jusqu'au milieu des années 2010, la plupart des résumés étaient extractifs. Une grande diversité existait pourtant déjà dans
ces algorithmes qui pouvaient aller de la sélection et extraction de phrases entières à l'extraction d'informations précises
recollées ensuite dans des textes à trous préparés à l'avance appelés templates. L'arrivée de nouvelles approches fondées sur
les réseaux de neurones a considérablement changé la donne. Ces algorithmes sont bien plus efficaces que les précédents pour
générer du texte grammatical et fluide, à l'image de ce qu'on peut faire avec [cette démo de GPT](https://transformer.huggingface.co/doc/gpt2-large).

Les réseaux de neurones nécessitent cependant de grandes quantités de données pour être entraînés et sont relativement peu modulables.
Ils fonctionnent parfaitement pour générer des commentaires pour lesquels la véracité a peu d'importance, mais risquent
fortement de générer des informations contradictoires ou simplement incorrectes ce qui est problématique dans le cadre de résumés d'articles de presse par exemple. De nombreux articles de recherche
s'intéressent à ces ["hallucinations" des réseaux de neurones](https://arxiv.org/pdf/2005.00661.pdf).

## Un exemple d'outil hybride : potara

Le résumé automatique a été le premier sujet de recherche auquel je me suis intéressé, et j'ai eu l'occasion de développer pendant mon
master un système hybride de résumé par extraction/génération pour une approche multi-documents, c'est à dire résumer un ensemble de documents parlant du même sujet.

L'idée était de partir d'une extraction classique, à savoir repérer les phrases les plus importantes et les assembler pour générer un résumé.
Le problème avec cette approche, c'est que les phrases les plus importantes pourraient souvent être encore améliorées.
Par exemple, dans un article parlant d'un déplacement présidentiel, la phrase "Emmanuel Macron a rencontré son homologue Américain et discuté économie"
pourrait être améliorée en "Emmanuel Macron a rencontré Joe Biden et discuté économie". Les journalistes évitant soigneusement les répétitions, on se retrouve fréquemment confronté à ce genre de phénomène.

Pour palier ce défaut, on peut repérer des phrases similaires présentes dans différents documents et tenter de les fusionner afin d'obtenir une phrase meilleure. Ansi, à partir des deux phrases suivantes :

- Emmanuel Macron a rencontré son homologue Américain à Washington et parlé longuement d'économie.
- Le président Français a rencontré Joe Biden et discuté économie.

On peut créer une phrase courte et informative :

- Emmanuel Macron a rencontré Joe Biden à Washington et discuté économie.

Plusieurs étapes sont nécessaires pour arriver à ce résultat : trouver les phrases similaires, trouver la meilleure fusion, vérifier que la fusion est bien meilleure qu'une phrase originale. Elles tirent partie de nombreuses technologies : réseaux de neurones
type [Word2Vec](https://en.wikipedia.org/wiki/Word2vec) pour trouver les phrases similaires,
[graphes de co-occurence](https://en.wikipedia.org/wiki/Co-occurrence_network) pour les fusionner,
[optimisation ILP](https://en.wikipedia.org/wiki/Integer_programming) pour sélectionner les meilleures fusions.

Si vous voulez en voir davantage, [potara est open-source](https://github.com/sildar/potara), mais n'a pas été maintenu depuis un moment.
Ce projet m'avait notamment servi de vitrine à ma sortie d'étude et avait donc une documentation, des tests, de l'intégration continue, un déploiement sur Pypi, ...

## Qu'est-ce qu'un bon résumé automatique ?

Si certains critères semblent évidents et relativement simples à évaluer (la grammaticalité des phrases par exemple), d'autres sont beaucoup plus complexes.
Décider quelles sont les informations les plus importantes d'un texte est déjà une tâche très subjective en soi. En évaluer la fluidité, le bon choix des mots employés, revient à un travail d'édition, et ne parlons pas de l'orientation politique que peut prendre un résumé !

Les nouveaux modèles génératifs à base de réseaux de neurones risquent par exemple d'introduire des jugements ou des qualificatifs péjoratifs
(ou mélioratifs), effet recherché lorsqu'il s'agit de générer une critique de cinéma,
mais beaucoup moins lorsqu'on parle du programme d'un candidat à l'élection présidentielle !

Le résumé automatique reste donc un sujet très actif en recherche, et risque de l'être pour un moment, particulièrement en ce qui
concerne la capacité à orienter le résultat de l'algorithme, justement vers un sentiment en particulier, un style spécifique, une coloration
politique donnée.
Dans l'industrie, il commence juste à faire son entrée dans des cadres bien spécifiques (résumé de réunions par exemple).