---
layout: post
title:  "Quels livrables pour un projet de datascience ?"
categories: Data BI IA
excerpt: "On parle rarement des documents à rédiger et à livrer dans le cadre des projets data. Or, ils sont indispensables à tout projet bien mené."
thumbnail: 'reporting.jpeg'
thumbalt: "une femme devant un ordinateur"
closingthumb: 'cat08c.jpg'
closingthumbdesc: "Après l'effort, le repos."
sharethumb: '/images/thumbs/reporting.jpeg'
---


La documentation des projets data, et plus particulièrement de la documentation non technique, n'est que rarement le sujet de billets de blogs qui décrivent plus volontier les projets que les comptes-rendus qui les accompagnent.
Même en Entreprise, la liste des livrables attendus n'est pas toujours explicite, d'autant plus lorsqu'il s'agit de projets internes.
On traite alors entre collègues, et on imagine qu'en cas de besoin on pourra toujours retrouver la datascientist en charge du projet dans le bureau d'à côté.
C'est oublier le [fort taux de turnover](https://swiss-sdi.ch/externaliser-conseils-data-science-eviter-fort-taux-turnover/) qui existe dans cette profession très en demande.
On risque alors de se retrouver sans aucune documentation, avec un algorithme en production qui fonctionne mais dont les rouages ne sont connus que d'un unique collègue, voire de plus personne.

Il est alors fréquent de se retrouver après quelques mois avec des algorithmes qui perdent en efficatité, qui ne sont plus mis à jour, ou qui cessent tout bonnement de tourner.
Il faut alors demander au nouveau datascientist de se plonger dans le code, tenter de comprendre le besoin qui existait, comment on y a répondu, et ce qui a changé depuis pour que les performances baissent.
Ce qui aurait dû être un *fix* de quelques heures de travail ou une mise à jour de quelques jours se transforme alors en une reprise complète de projet qui pourra demander jusqu'à plusieurs semaines de travail.

La solution pour éviter ces écueils est connue de tous mais souvent négligée : la documentation.
Utile non seulement pour reprendre un projet vieux de plusieurs mois ou années, elle est également indispensable au bon déroulement d'un projet.
C'est elle qui permet de fixer par écrit les attendus du client (même lorsque le client est en fait un collègue) ainsi que les risques anticipés.
On s'intéresse dans ce billet à la documentation pour deux types de projets data : ceux qui aboutissent à un algorithme mis en production (algorithmes de recommandation, classification, ...) et ceux qui débouchent sur un conseil business (analyse d'usage, pricing, ...).

Ce billet vient en complément de l'article "[Les cinq étapes d'un projet data réussi](https://www.ledatablog.com/data/ia/2020/01/16/5-etapes-projet-data.html)" et propose une liste de livrables à fournir afin de garder une trace durablement exploitable des travaux réalisés.

---

## Deux ingrédients pour des livrables utiles : la structure et les illustrations

On ne rédige pour ainsi dire jamais une documentation pour soi-même.
Les documents que je décris dans ce billet sont donc avant tout pensés pour être lus par d'autres personnes que leur rédacteur : ses donneurs d'ordres d'une part, et ses futurs remplaçants d'autre part.
Les formats conseillés sont dédiés à un public large, ce qui les rend pratiques pour se remémorer un projet réalisé plusieurs années auparavant, de façon bien plus efficace qu'une plongée dans un vieux code source.

À cette fin, l'ensemble des livrables doivent obéir à deux règles : clarté et compréhensibilité.
La première s'obtient grâce à une structure claire et aérée : des sections bien titrées, une table des matières, une charte graphique cohérente et régulière, des légendes, ...
La seconde s'obtient par des paragraphes bien construits, des idées claires et clairement exprimées, des enchaînements logiques et des visualisations efficaces.

Attention cependant à ne pas inclure trop d'illustrations. Parfois, une ou deux phrases sont plus claires qu'un tableau ou qu'un graphique.
D'autre part, les rapports trop longs ne sont pas lus, il faut donc arbitrer et n'inclure que les éléments importants.
Cet équilibre ne s'obtient qu'à force d'entraînement, et lorsqu'on a de la chance, par les retours que l'on veut bien nous donner.

---

## Rapport d'analyse des besoins

Le principal risque d'échec des projets data, comme pour la plupart des projets informatiques, se situe dans une mauvaise compréhension du besoin client.
Le risque est encore plus grand lors d'une reprise de projet, pour laquelle le client souhaite une amélioration des performances ou une mise à jour des données du modèle.
La datascientist, si elle n'a pas de documentation à disposition, risque alors de ne pas avoir une vision claire des exigences et des attendus du client, et d'apporter des améliorations qui s'avèreront au final contre-productives (par exemple intégrer un segment de clientèle non pertinent, déséquilibrer le compromis rappel/précision, ...).

C'est pourquoi le premier livrable à fournir, indispensable à la bonne conduite de tout projet data, est un rapport des besoins exprimés et des solutions envisagées.
Ce rapport, rédigé généralement sur Word ou autre traitement de texte (et pas Powerpoint!), fait généralement quelques pages et décrit les éléments suivants :

1. Problématique générale : état actuel, personnes ou services concernés, besoins exprimés, ...
2. Objectifs chiffrés visés : performance minimale permettant l'amélioration de la situation courante
3. Exigences non négociables : temps de calcul, précision, réactivité, ...
4. Périmètre des données utilisées : périodes, volume, champs et types, sensibilité durée de conservation, ...
5. Solution générale envisagée : méthodologie
6. Risques, limites et impacts attendus : prérequis, durabilité, fiabilité, saisonnalité, ...
7. Récurrence envisagée : fréquence et automatisation des mises à jour, validité de l'étude dans le temps, ...

Ces 7 points permettent de valider avec le donneur d'ordres (ou *stakeholder*) le réalisme de la solution et surtout sa viabilité pour une utilisation en production ou pour une prise de décision.
Ce dialogue avec le *stakeholder* est central dans tout projet de datascience, et je vous conseille [la lecture de cet article](https://towardsdatascience.com/how-to-work-with-stakeholders-as-a-data-scientist-13a1769c8152) (en anglais) si vous souhaitez creuser le sujet.
Ces 7 points permettent également d'estimer le temps nécessaire au projet, les risques qu'il comporte, les besoins de mise à jour anticipés, et permettent éventuellement d'établir les prochains points d'étape.
Ils sont indispensables au chiffrage du projet et forment la base de travail, le *contrat* que vous passez avec le porteur de projet.

Ce livrable porte essentiellement sur les besoins et les aspects techniques doivent y être très légers.
D'abord parce qu'ils n'intéresseront probablement pas le destinataire de ce rapport, ensuite parce qu'ils pourront évoluer au fur et à mesure que le projet avance.

De manière générale, on pourra se passer de mentionner l'algorithme précis, le langage de programmation, les librairies utilisés.
Il s'agit à ce stade d'une part de rassurer le donneur d'ordres sur la capacité à faire, et d'autre part de mieux estimer le temps de développement nécessaire, la construction d'un réseau de neurones complexe ne nécessitant pas le même travail qu'un K-NN (ni le même volume de données, ni les mêmes ressources).
Par exemple, pour un besoin de type segmentation de clientèle, dire que des méthodes de *clustering* sont envisagées suffira amplement.

L'analyse de besoins n'est pas toujours lue avec attention pas le porteur de projet.
Il revient au datascientist de le rendre le plus lisible et le moins technocentré possible pour faciliter sa lecture.
Un soin particulier doit être apporté aux trois premiers items qui sont ceux qui intéressent le plus le donneur d'ordre, les items suivants servant essentiellement à se prémunir contre des imprévus et à préciser les besoins de l'analyste (volume de données par exemple).

---

## Livrables intermédiaires

Les livrables intéremédiaires sont les moins critiques dans le sens où certains d'entre eux risquent d'être rendus invalides au cours du projet (jeu de données vicié, bugs non détectés, ...).
Il y en a néanmoins un qui a une utilité indéniable : l'étude du corpus.

### Etude des données

Ce document est essentiellement à l'usage des datascientists pour leur permettre de recenser tous les biais et autres limites d'un jeu de données.
Anomalies, absences, complétude, saisonnalité, suspicions d'erreurs, fraîcheur, le moindre doute doit y être consigné, que l'on puisse le confirmer ou non.
Cet inventaire peut être en partie partagé avec le donneur d'ordres afin d'envisager des améliorations en termes de récolte ou de maintenance des données.
Il permet également d'affiner l'évaluation des risques et l'estimation de la durée du projet (une phase de nettoyage ou de redéfinition du périmètre devant généralement intervenir à cette étape).

Une fois l'étude de corpus réalisée, le projet peut réellement débuter, et les analyses statistiques ou le développement d'algorithmes démarré.
Intervient alors une phase plus où moins longue de travail, qui va donner lieu à des résultats intermédiaires.

### Résultats intermédiaires et baseline

Si le projet dure longtemps, il est important de faire des points d'avancement réguliers.
Ceux-ci serviront d'une part à rassurer le porteur de projets que le sujet avance, mais peut également permettre de remettre en question certains besoins, de poser des questions sur certaines données semblant abbérantes, ... autant d'éléments qu'il vaut mieux prendre en considération le plus tôt possible.

Néanmoins, ces résultats intermédiaires ne sont pas toujours entièrement fiables : le périmètre de données continue d'évoluer au fur et à mesure que de nouvelles anomalies sont détectées, les tests s'assurant de la correction du code n'ont pas tous été écrits, les attentes peuvent évoluer à la marge.
Pour cette raison, les échanges avec les *stakeholders* se font essentiellement à l'oral, avec un support Powerpoint qui n'est pas nécessairement partagé, ou alors avec une notice d'avertissement sur la fiabilité des résultats.

La seule exception concerne le développement éventuel d'une *baseline*, qui doit être correctement testée et qui doit fixer définitivement le jeu de données utilisé.
Si *baseline* il y a, un rapport fonctionnel présentant la méthode utilisée et les résultats obtenus doit être rédigé.
On y retrouvera les informations suivantes :

* Rappel du sujet et référence à l'étude de besoins et à l'étude de corpus
* Description du jeu de données utilisé, des traitements réalisés, des limites et des principaux biais
* Présentation de la méthode sélectionnée pour la baseline
* Liste des principaux paramètres de la baseline
* Affichage des résultats et performances
* Rédaction du différentiel de performance attendu par rapport à la méthode complète

À mon sens, il n'y a pas besoin à ce stade de Powerpoint, sauf à l'utiliser comme un support de communication orale au même titre que les autres résultats intermédiaires (1 ou 2 slides sur la baseline seront de toute manière repris dans le rapport final).
Il doit néanmoins être rédigé de façon détaillée afin de permettre de bien comprendre les résultats obtenus et le périmètre sur lequel ils s'appliquent.
Il peut arriver qu'à la lecture de ce rapport, le projet soit arrêté.
Soit la *baseline* fait le job, soit on est trop loin et on estime les chances de succès trop faibles pour poursuivre.
Un rapport de post-mortem doit alors être rédigé, sur le modèle des livrables de fin de projet décrits après.

---

## Livrables de fin de projet

Arrive la fin du projet. Les résultats sont là, ils sont vérifiés, l'algorithme fonctionne et a été testé. Il ne reste plus qu'à fournir la documentation.
À cette étape, il me semble indispensable de fournir deux supports : un rapport fonctionnel, rédigé et donnant les détails permettant de comprendre comment les analyses ont été menées, et un *executive summary*, c'est à dire un Powerpoint d'une dizaine de slides qui récapitule le projet et les résultats obtenus.
Ce dernier support sera souvent le seul lu et conservé précieusement par le *stakeholder*.
Si vous avez suffisamment bien fait votre travail, il y a de grandes chances qu'il en extraie même quelques slides pour en rapporter à sa direction.
Il est donc dans votre intérêt de rendre le document le plus propre et exploitable possible.

### Executive summary et rapport fonctionnel

L'*executive summary* doit reprendre les élements suivants :

* Expression du besoin : Besoin, contraintes, amélioration par rapport à l'existant
* Choix méthodologiques : Philosophie, quelles contraintes ont mené à la solution choisie
* Présentation de la solution : Intuition derrière la méthode (*look-alike*, *réseau de neurones*, *scoring*, ...)
* Résultats : Chiffres bruts obtenus par la méthode
* Limites : Cas d'erreur, validité temporelle, biais, ...
* Impact et suites à donner : Evolution attendue des KPI, actions à mettre en place, ...

Chaque élément ne devrait pas faire plus de 2 slides et chaque slide ne devrait comporter que quelques lignes de texte.
En particulier, les points techniques n'ont pas à y figurer, et l'explication de la solution doit être simple, intuitive et courte.
La lecture de ce document doit permettre de comprendre ce qui a été fait, pourquoi, et avec quels impacts attendus.

Il s'accompagne d'un rapport fonctionnel détaillé, qui reprend ces différents points en les précisant, et en décrivant succintement les choix technologiques.

### Algorithmes

Si l'un des attendus est un algorithme, celui-ci doit logiquement être livré proprement (code commenté, dépendances, entrées et sorties, ...) et débarrassé de tout le code mort, y compris celui ayant servi aux diverses expériences n'ayant pas abouti.
Il est également essentiel de décrire les outils ou bibliothèques dont il dépend, les versions utilisées, bref, tout ce qui permettra de reproduire vos résultats sans avoir à se poser de questions.
De nombreuses ressources s'intéressent à comment documenter correctement du code, à comment le versionner et le distribuer efficacement ([en voici un exemple arbitraire](https://towardsdatascience.com/clean-code-for-a-data-scientist-f4b760374b74)).

---

## Les autres types de rapports

À mon sens, la liste des livrables indispensables s'arrête ici. J'ai néanmoins l'habitude d'en préparer d'autres, que je ne distribue pas systématiquement :

* Un état de l'art explicitant les alternatives possibles en termes d'algorithmes ou d'architectures
* Une analyse précise des cas d'erreurs avec leur recensement, des explications, des suppositions (Word + Excel pour des données structurées)
* Un mémo des améliorations possibles (un simple fichier .txt y suffit)
* Une version courte et interactive de l'algorithme via [un notebook](https://jupyter.org/index.html).

Tous ces supports ne se justifient pas pour tous les projets (par exemple l'état de l'art n'a pas grand intérêt pour une analyse statistique classique), néanmoins ils peuvent s'avérer pratiques par la suite.
Je pense notamment à la version courte de l'algorithme, qui permet d'avoir une version nettoyée de tout l'historique du projet et allant à l'essentiel, utile lorsqu'il n'y a pas de code livré mais que l'on souhaite garder une trace.
Cela permet également une vérification supplémentaire de la fiabilité des résultats en réécrivant *from scratch* l'algorithme afin de vérifier l'absence de bug ou d'effet de bord.

L'analyse des cas d'erreurs peut s'avérer précieuse, elle devrait être réalisée, a minima partiellement, avant la fin du projet afin d'assurer sa robustesse.
Néanmoins, il faut prendre garde à ne pas conserver de données qui pourraient tomber sous le coup de la RGPD (et donc veiller a minima au cycle de vie des données personnelles).

Le mémo des améliorations possibles est le seul document que je conseille de rédiger au format .txt.
Ce document est pour vous, et pour vous seul.
Il n'a pas à être compris par quelqu'un d'autre, il peut être truffé d'abbréviations, d'approximations, d'idées farfelues, sans structures et rempli de fautes : lâchez-vous !

---

## Les risques inhérents aux livrables

Tout ce qui a été dit ici peut paraître évident : documenter et avoir des livrables clairs semble être bénéfique a tout le monde.
Pourquoi alors est-il fréquent de se retrouver avec des projets sans aucune documentation ?

Trois facteurs majeurs entrent pour moi en compte.

D'abord, et c'est certainement le point le plus critique, rédiger ces documents engage le datascientist.
Cela l'amène à écrire noir sur blanc ses suppositions, et peut mettre en lumière des risques mal anticipés, des prédictions trop optimistes, des intuitions erronnées.
Écrire ces rapports, c'est accepter d'assumer ses erreurs, y compris face à des clients qui peuvent prendre ces erreurs pour de l'incompétence.
Dans un domaine ou le [syndrôme de l'imposteur est extrêmement présent](https://caitlinhudon.com/2018/01/19/imposter-syndrome-in-data-science/), la réticence à documenter précisément ses travaux pour se protéger est donc un mécanisme de défense naturel.

Ensuite, la plupart des livrables à fournir nécessitent une simplification des approches utilisées, et omettent généralement une grande partie des expérimentations réalisées.
Ceci peut aboutir à un sentiment de simplicité du travail réalisé, pour lequel on peut finir par se demander si tant de temps était nécessaire et si des compétences spécifiques étaient réellement indispensables.
Le risque, bien plus critique que le fait de renvoyer une image peu flatteuse au datascientist, est que des travaux similaires soient plus tard confiés à des personnes moins compétentes, qui travailleront sans se rendre compte de la myriade de pièges dans lesquels elles tombent.

Enfin, la description précise des méthodes employées a pour but d'éviter la concentration des connaissances sur une ou quelques personnes.
En conséquence, cette mise à disposition des connaissances rend la datascientist moins indispensable.
Fréquemment, lorsqu'une question se pose sur le fonctionnement de l'algorithme, un simple coup d'oeil à une documentation bien construite permet de trouver la réponse.
L'absence de documentation, au contraire, risque de mener le datascientist a être systématiquement dérangé pour répondre à des questions, souvent les mêmes.
Ces deux postures ont des avantages et des inconvénients : temps libéré d'un côté au prix d'une dépossession, contrôle renforcé de l'autre en contrepartie d'un service après-vente alourdi.

Mon choix personnel est de parier sur une documentation large et exhaustive.
D'abord parce que cela me permet régulièrement de corriger des présupposés (sur les besoins, les données, ...) qui auraient pu mettre en difficulté le projet.
Ensuite parce qu'il aide grandement à tisser une relation de confiance avec ses interlocuteurs.
La crédibilité des résultats s'en trouve renforcée et on augmente la probabilité que les travaux réalisés soient effectivement utilisés.
Enfin parce que j'estime que ma valeur ne réside pas tant dans le fait d'être capable d'implémenter et de paramétrer des algorithmes complexes, mais dans ma capacité à choisir la meilleure solution pour un problème donné en fonction des besoins et des contraintes.
Les rapports rédigés sont la meilleure démonstration possible de ces compétences, et tout le monde y gagne.

---
