---
layout: post
title:  "Ne laissez pas vos données devenir des Gremlins !"
categories: Data BI
excerpt: "Ne pas prendre assez soin de ses données clients expose à de nombreux risques. Pourquoi avoir une source de données unique (single source of truth) est-il primordial, et à quels risques vous exposez-vous si vous n'en disposez pas ?"
thumbnail: 'gremlins.jpg'
thumbalt: 'des gremlins'
closingthumb: 'cat03.jpg'
closingthumbdesc: "Mon chat ressemble bien plus à Gizmo qu'à un Gremlins... la plupart du temps"
---


Tout comme les données que vous confient vos clients, particuliers ou professionnels, les [Mogwai](https://gremlins.fandom.com/wiki/Mogwai), sont de merveilleuses créatures, mais il faut leur accorder un soin particulier.
En effet, ne pas suivre quelques règles élémentaires peut rapidement les transformer en un véritable cauchemard.

Pourquoi avoir une source de données unique (single source of truth en anglais) pour vos données business est-il primordial, et à quels risques vous exposez-vous si vous ne disposez pas d'une telle source ? C'est à ces deux questions qu'on va tenter de répondre.


# Ne multipliez pas les données

Dans les films Gremlins, arroser un Mogwai le fait se multiplier.
Dupliquer les données est également une mauvaise idée pour plusieurs raisons.

## Où sont passées mes données ?

Prenons l'exemple du nombre de fois où votre  plus gros client a réalisé une commande en 2018.
Il s'agit du problème le moins préoccupant : en fouillant un peu, vous retrouverez très probablement la donnée que vous cherchiez.
Peut-être dans la base de données comptabilisant les commandes, peut-être dans la base clients même si, comme il l'a été répété plusieurs fois en réunion, elle n'a rien à y faire.
Peut-être dans un rapport qui vous avait été confié, peut-être dans un mail reçu l'année dernière qui dressait la liste de vos meilleurs clients avec quelques informations supplémentaires.

Si vous ne parvenez toujours pas à la trouver, pas de panique, peut être que votre data scientist en avait une copie sur son poste pour ses analyses, que le marketing a des slides le présentant ou qu'un fichier Excel existe sur le poste du directeur commercial.

Donnée trouvée ? Parfait, car le vrai problème arrive.

## Laquelle est la bonne ?

Avec un peu de malchance, vous vous êtes arrêté à la première donnée trouvée et vous vous êtes planté.
Le nombre de commandes est-il celui qui correspond aux factures émises en 2018 ? Ou bien aux livraisons effectuées en 2018 ?
Les commandes annulées sont-elles bien retranchées ? Et celles qui sont en défaut de paiement ? Tous les canaux de vente sont-ils bien pris en compte ?
Une commande ayant donné lieu à des livraisons récurrentes est-elle comptée une fois ou plusieurs fois ?

Si vous avez trouvé votre donnée dans un fichier Excel, sur des slides, ou plus généralement sur un poste de travail, il y a de grandes chances qu'il soit difficile de répondre à ces différentes questions. Vous pourriez même trouver des données qui se contredisent en fonction de leur provenance.
En ayant multiplié la donnée, vous avez perdu sa définition, sa tracabilité. Il n'y a plus qu'à trouver la personne qui a manipulé cette donnée en dernier, et espérer qu'elle se souvienne des traitements réalisés (si cette personne fait toujours partie de votre Entreprise !).

## Une source de données unique

Un principe important en data science BI est la source de données unique. Une base de données documentée, qui fait consensus dans la mesure du possible, et autorité dans tous les cas. Sans une source unique, la donnée a toutes les chances d'être ou de devenir mauvaise. Et une mauvaise donnée, c'est une donnée qui fait prendre de mauvaises décisions.

La construction d'un socle de données de référence est complexe, et est souvent un prérequis à la constitution, ou en tout cas au travail efficace, d'équipes dont le métier tourne autour de la donnée.

# La transformation en mauvaise donnée

Dans Gremlins, si un Mogwai est nourri après minuit, il se transforme en une créature maléfique.
En ce qui concerne vos données, la transformation peut être lente comme très rapide.

## La fuite

Le cas de figure extrême est la fuite de données. Hier elle était là, et aujourd'hui elle ne l'est plus. Pire encore, elle est partout, et surtout au délà de vos murs. D'un coup, vos concurrents ont accès à toutes les informations dont ils ont toujours rêvé.

Ceci peut arriver de tas de façons différentes, mais la plus fréquente n'est pas le piratage ou la malveillance, il s'agit plutôt de [la maladresse humaine](http://www.nbcnews.com/id/7032779/ns/technology_and_science-security/t/bank-america-loses-customer-data/#.WHPYpVMrJUQ).
Et plus vos données sont éparpillées entre vos murs, sur les postes de différents collaborateurs, dans les boîtes mails, plus vous êtes à risque de voir tout ou partie s'envoler.

Une seule façon de s'en prémunir, avoir un responsable de la sécurité fiable, compétent, à qui une très grande latitude est laissée et auquel des moyens sont fournis. Et vu que ce n'est pas mon métier et que ça ne s'improvise pas, je me garderai bien d'en dire davantage.

## L'obsolescence

La donnée périme. A minima sa définition périme. Les données doivent donc être entretenues, mises à jour, et supprimées lorsque nécessaire. Vos produits changent de prix, ils évoluent. Vos clients changent, leurs propiétés également.
Les données qui y sont liées doivent évoluer de façon synchrone, sans perdre d'historique.

Ces évolutions pourtant nécessaires sont souvent douloureuses lorsqu'elles ne sont pas anticipées, avec des bases de données mal agencées, mal documentées, peu exploitables.
Sans ces mises à jours, vos données finiront par mentir, ouvrant la voie à de mauvaises prises de décisions qu'il sera très complexe d'analyser.


# La destruction

Pour les Gremlins, c'est simple, il suffit de les exposer à une lumière vive.
Pour les données, sans source unique, c'est bien plus complexe.

## Une fausse impression de sécurité

Vous avez reçu un mail demandant à appliquer la RGPD et à supprimer toutes les données que vous avez sur un client ? Rien de plus facile, vous avez une procédure de prête pour ça, et en remplissant un simple formulaire, la donnée disparaît. Mais a-t-elle vraiment totalement disparu ?

Si vous n'avez pas de source de données unique, il y a fort à parier que des informations sur le client se trouvent sur les postes de travail de vos collaborateurs, sur des bases de données annexes, qui ne sont presque jamais utilisées. Presque. Et un jour, elles risquent d'être réinjectées par mégarde [ou même fuiter](https://www.theregister.co.uk/2017/10/30/heathrow_usb_security_blunder/).

La seule solution est alors de s'assurer que, dans chaque service, chaque collaborateur ait bien effacé la donnée s'il l'a déjà eu entre les mains. Un peu plus complexe qu'un simple formulaire à remplir, et surtout beaucoup moins fiable...


# Conclusion

Un socle de données unique est long et coûteux à mettre en place, et ses avantages ne sont visibles qu'à moyen et long terme.
Il est cependant indispensable de disposer de telles sources de données afin de mener des analyses business data poussées dans de bonnes conditions.

Beaucoup de sujets n'ont pas été abordés ici, comme les contrôles d'accès à ces socles, les différentes technologies permettant de mettre les mettre en place ainsi que les avantages en terme de productivité pour ses utilisateurs, et en termes de prise de décision pour les dirigeants. Peut-être l'objet pour un futur billet !
