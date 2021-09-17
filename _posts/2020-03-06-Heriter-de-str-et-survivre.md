---
layout: post
title:  "Python : Hériter de str et survivre"
categories: Python
excerpt: "Hériter de str en Python est en règle générale une mauvaise idée : mieux vaut encapsuler. Qu'importe, lançons-nous dans l'aventure et voyons ce qu'il en retourne."
thumbnail: 'inheritstr.jpg'
thumbalt: 'la princesse de Princess Bride met en garde contre un danger'
closingthumb: 'cat06.jpg'
closingthumbdesc: "Mon chat a des journées passionnantes !"
---

Python est un langage de programmation très utilisé pour la programmation d'intelligences artificielles, et pour le traitement des langues (ou NLP, qui comprend par exemple la traduction automatique, la classification de textes, ...).
Il est donc très fréquent d'y utiliser des chaînes de caractères, ou *str*, un type de base du langage. Il peut devenir tentant, pour rajouter des fonctionnalités aux *str*, d'en hériter pour créer des objets plus polyvalents.
Malheureusement, c'est généralement une mauvaise idée et de nombreux problèmes difficiles à anticiper risquent de se présenter.
Qu'importe, tentons l'expérience et utilisons l'occasion pour comprendre un peu mieux certaines particularités du langage Python !

Ce billet est une adaptation de mon talk à la PyconFr 2019, un événement annuel qui regroupe les utilisateurs du langage Python.
Les slides de ma présentation sont [visibles ici](https://sildar.github.io/pyconfr2019/), et la vidéo devrait arriver dans les prochains mois.


# L'objectif

On souhaite créer une classe, qu'on nommera **PyconStr**, et qui hérite de *str* en lui rajoutant des fonctionnalités.
Pour l'occasion, on va créer une méthode *shout()* qui ajoute un point d'exclamation à notre **PyconStr**.
Le but sera de **pouvoir enchaîner de façon transparente** les appels aux fonctions standard de *str* comme *strip()* (suppression des espaces en début et fin de chaîne) ou *capitalize()* (mise en majuscule de la première lettre) **et nos propres méthodes**.

Notre **PyconStr** pourra prendre deux paramètres, un premier correspondant à la chaîne de caractère que l'on souhaite avoir, et un second dont on ne s'occupera pas vraiment, qui pourrait être une autre chaîne de caractère, un entier, ou quoi que ce soit d'autre.
Voici à quoi ça va ressembler :

```python
# Notez le str dans la définition de la classe
# indiquant que la classe hérite de str
class PyconStr(str):
  # Magic code


s = PyconStr(" bonjour ", "Pycon")
print(s)
" bonjour "
s = s.strip().shout().capitalize()
print(s)
"Bonjour!"
```

Tout l'enjeu sera de remplacer le *# Magic code* par du vrai code.

![Challenge accepted!](/images/content/challenge.webp){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}

---

# Ce qu'il faudrait faire

J'ai précisé dans l'introduction qu'hériter de *str* était une mauvaise idée, et plutôt que d'attendre la fin pour vous donner la *bonne* façon de faire, autant s'en débarasser tout de suite.
L'objectif est davantage de montrer ce qui ne va pas fonctionner lors de l'héritage de *str* que de discuter de la solution optimale.

Une bonne façon de faire, c'est d'encapsuler la *str* dans un attribut de notre classe, et d'appliquer les méthodes de *str* qui nous intéressent à cet attribut.
Voici un exemple nommé **JolieStr**, qui reproduit le fonctionnement souhaité plus haut, mais sans hériter de *str* : 



```python
class JolieStr:
  def __init__(self, content, info):
    # on enregistre la chaîne dans un attribut _content
    self._content = content
    self._info = info

  # on "réimplémente" les méthodes standard str qui nous intéressent
  def capitalize(self):
    self._content = self._content.capitalize() 
    return self

  def strip(self):
    self._content = self._content.strip()
    return self
	
  # on rajoute notre shout()
  def shout(self):
    self._content = self._content + '!'
    return self

  # on renseigne __repr__ pour que lors d'un print
  # seul l'attribut _content soit affiché
  def __repr__(self):  
    return self._content


s = JolieStr(" bonjour ", "Pycon")
print(s)
" bonjour "
s = s.strip().shout().capitalize()
print(s)
"Bonjour!"
```

L'inconvénient est ici principalement qu'il faut réimplémenter toutes les méthodes standard de *str* pour bien les appliquer au bon attribut.
On retourne systématiquement *self* dans nos méthodes afin de pouvoir les enchaîner, et si jamais il est fait appel à une méthode standard de *str* qu'on a pas pris la peine de réimplémenter, une erreur se produira.

Il existe quelques options pour éviter ces problèmes, dont certaines seront évoquées plus loin.
Mais laissons de côté cette **JolieStr** et concentrons nous sur l'implémentation de la **PyconStr** héritant directement de *str*.

---

# BasicStr, un monde merveilleux ou tout est simple

Le premier réflexe qu'aurait un développeur ayant à créer une classe héritant de *str* serait probablement de s'y essayer comme si tout allait se passer au mieux.
Sa classe, qu'on appelera **BasicStr**, pourrait ressembler à ça :

```python
class BasicStr(str):
  def __init__(self, content, info):
    # on fait appel à l'init de str
    # en se disant qu'en lui envoyant la chaîne
    # il va créer une str directement
    super().__init__(content)
    self._info = info


s = BasicStr(" bonjour ", "Pycon")
print(s)
```

Hélas, ces quelques lignes de code ne fonctionnent absolument pas.

```
Traceback (most recent call last):
File "basicstr.py", line 6, in module
   s = BasicStr(" bonjour ",  "Pycon")
TypeError: decoding str is not supported
```

![I don't get it!](/images/content/waitwhat.webp){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}

L'erreur est un peu cryptique, et lorsque l'on essaye de la débugger, on se rend compte que le programme plante avant même d'arriver dans la méthode *\_\_init\_\_()* !

En [fouillant un peu](https://docs.python.org/3/reference/datamodel.html#object.__new__) on réalise qu'il existe une méthode *\_\_new\_\_()* qui est appelée avant *\_\_init\_\_()* et sert à instancier les objets, notamment les types de base dont *str* fait partie.
On trouve la défintion suivante dans la documentation, bien utile :


> object.\_\_init\_\_(self[, ...]):
>
>   Called after the instance has been created (by \_\_new\_\_()), but before it is returned to the caller.

> object.\_\_new\_\_(cls[, ...]):
>
>   \_\_new\_\_() is intended mainly to allow subclasses of immutable types (like int, str, or tuple) to customize instance creation. It is also commonly overridden in custom metaclasses in order to customize class creation.


# NewStr, où l'on a appris de nos erreurs

Après avoir lu la documentation, la solution semble claire : il faut faire appel à *\_\_new\_\_()*.
Sa syntaxe est un peu différente de *\_\_init\_\_()*, mais on s'y retrouve vite, et voici à quoi ressemblerait une **NewStr** :


```python
class NewStr(str):
  def __new__(cls, content, info):
    obj = super().__new__(cls, content)
    return obj

  def __init__(self, content, info):
    super().__init__()
    self._info = info

  def shout(self):
    return self + "!"


s = NewStr("bonjour", "Pycon")
print(s)
"bonjour"
# upper() fonctionne sans que l'on ai eu besoin de l'implémenter
print(s.upper())
"Bonjour"
print(s.shout())
"bonjour!"
```

A première vue, tout fonctionne comme prévu ! Mais dès qu'on essaye d'enchaîner les méthodes...

```python
s = NewStr("bonjour", "Pycon")
print(s.shout().shout())
```

```
Traceback (most recent call last):
File "newstr.py", line 6, in module
  print(s.shout().shout())
AttributeError: 'str' object has no attribute 'shout'
```

![I knew it!](/images/content/knewit2.webp){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}


L'erreur est cette fois-ci moins crytique : on nous dit que *str* n'a pas de méthode *shout()*, et c'est logique ! Notre méthode *shout()*, lorsqu'elle concatène le "!" renvoie en effet une chaîne de caractères.
Pas de panique, la solution est simple, il suffit de faire en sorte que *shout()* renvoie une NewStr à la place.

```python
class NewStr(str):
  def __new__(cls, content, info):
    obj = super().__new__(cls, content)
    return obj

  def __init__(self, content, info):
    super().__init__()
    self._info = info

  def shout(self):
    return NewStr(self + "!", self._info)

s = NewStr("bonjour", "Pycon")
print(s.shout().shout())
"bonjour!!"
```
![Happy face!](/images/content/excited.webp){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}

Malheureusement, les méthodes de *str* retournent toujours des *str*, et pas des **NewStr**, ce qui empêche l'enchaînement de méthodes str->NewStr :


```python
print(s.upper().shout())
```

```
Traceback (most recent call last):
File "newstr.py", line 6, in module
  print(s.upper().shout())
AttributeError: 'str' object has no attribute 'shout'
```

![Sad face!](/images/content/disappointed.webp){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}

Il va donc falloir intercepter les méthodes de *str* pour transformer le type de leurs retours !


# InterceptStr, où on attrape les résultats au vol

L'idée consiste à s'apercevoir, lors des appels de méthodes sur notre objet, si la méthode appelée dépend de *str*, ou si elle est implémentée "chez nous" dans **InterceptStr**.
Heureusement, une méthode existe pour ça, il s'agit de *\_\_getattribute\_\_()* :


> object.\_\_getattribute\_\_(self, name):
>
>    Called unconditionally to implement attribute accesses for instances of the class.

Côté implémentation, c'est un peu plus complexe, et on va faire ça en deux temps.
Notre classe **InterceptStr** va donc implémenter *_\_getattribute\_\_()*, qui indiquera le nom de la méthode appelée.
Si la méthode appartient à la classe *str*, ce qu'on peut vérifier en regardant si elle apparaît dans *dir(str)* (une fonction standard servant à vérifier tous les attributs accessibles de l'instance passée en paramètre), on... verra ce qu'on fait un peu plus tard !
Dans le cas contraire, c'est que la méthode appartient à notre classe **InterceptStr**, et on se contente de poursuivre le chemin classique en faisant appel à *super().\_\_getattribute\_\_()*.

On obtient la classe (incomplète!) suivante :

```python
class InterceptStr(str):

  def __new__(cls, content, info):
    obj = super().__new__(cls, content)
    return obj

  def __init__(self, content, info):
    super().__init__()
    self._info = info

  def __getattribute__(self, name):
    if name in dir(str):
      # on à affaire à une méthode de str
      return # TODO !
    else:
      # on suit le chemin normal en laissant getattribute gérer.
      return super().__getattribute__(name)

    def shout(self):
      return InterceptStr(self + "!", self._info)
```

Dans notre return, on aimerait bien pouvoir directement appeler la méthode concernée, le problème est que dans *\_\_getattribute\_\_()*, nous n'avons accès qu'au nom de la méthode, et pas à ses arguments.
Il va donc falloir ruser et passer par une fonction annexe qui elle acceptera les arguments.
Elle se chargera alors d'appliquer la méthode à partir de son nom et des arguments grâce à fonction standard *getattr()*.
On s'assurera juste du type de valeur retournée par la méthode executée : si c'est un *str*, on le transformera en **InterceptStr**, sinon on lui laissera son type par défaut.

```python
def applymethod(self, funcname, *args, **kwargs):
  value = getattr(super(), funcname)(*args, **kwargs)
  if isinstance(value, str):
    return InterceptStr(value, self._info)
  return value
```

Il n'y a alors plus qu'à utiliser *applymethod()* dans notre *\_\_getattribute\_\_()*.

Dernière subtilité, *\_\_getattribute\_\_()* doit absolument retourner une fonction ou une méthode, et pas une valeur !
Plutôt que de retourner directement le résultat de *applymethod()*, on va donc retourner une fonction créée à la volée avec les bons paramètres.
On va utiliser pour cela *functools.partial()*, qui est un module standard de Python.

```python
  def __getattribute__(self, name):
    if name in dir(str):
      # on à affaire à une méthode de str
      return functools.partial(self.applyfunction, name)
    else:
      # on suit le chemin normal en laissant getattribute gérer.
      return super().__getattribute__(name)
```


# PyconStr, la solution complète

Nous arrivons au bout du chemin. On a résolu presque tous les problèmes, et on a une classe **PyconStr** qui se comporte comme on le souhaite :

```python
class PyconStr(str):

  def __new__(cls, content, info):
    obj = super().__new__(cls, content)
    return obj

  def __init__(self, content, info):
    super().__init__()
    self._info = info

  def applyfunction(self, funcname, *args, **kwargs):
    value = getattr(super(), funcname)(*args, **kwargs)
    if isinstance(value, str):
      return PyconStr(value, self._info)
    return value

  def __getattribute__(self, name, *args, **kwargs):
    if name in dir(str):
	  # on à affaire à une méthode de str
      return functools.partial(self.applyfunction, name)
    else:
	  # on suit le chemin normal en laissant getattribute gérer.
      return super().__getattribute__(name)

  def shout(self):
    return PyconStr(self + "!", self._info)
```

```python
s = PyconStr(" bonjour ", "Pycon")
print(s)
" bonjour "
s = s.strip().shout().capitalize()
print(s)
"Bonjour!"
```

![Well done!](/images/content/done.gif){:style="display: block; margin-left: auto; margin-right: auto; width: 60%"}


# L'heure du bilan

Réimplémenter quelques méthodes comme vu avec **JolieStr** pouvait sembler laborieux, mais notre expérimentation d'héritage de *str* s'avère finalement bien plus complexe !

Au final, on aura vu quatre fonctions qui peuvent s'avérer très utiles :


1. *\_\_new\_\_()* pour l'initialisation des objets immutables
2. *\_\_getattribute\_\_()* pour intercepter les méthodes
3. *getattr()* pour appliquer une méthode à partir de son nom
4. *functools.apply()* pour fixer un paramètre d'une fonction et retourner une nouvelle fonction


Cette expérimentation a pour origine mon envie naïve d'hériter de str, et n'ayant trouvé comme plus simple explication à mes problèmes que [ce post StackOverflow](https://stackoverflow.com/a/33272874),
j'ai décidé de creuser et d'en faire un talk à la PyconFr 2019, un événement que j'apprécie particulièrement et que je conseille à tous les utilisateurs de Python !


