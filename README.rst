API Web
=======

Cours d'introduction à l'utilisation des API Web,
enseigné par `Pierre-Antoine Champin`_ et `Michael Mrissa`_
au département informatique de l'`IUT de Lyon 1`_.

Il est publié à http://champin.net/enseignement/webapi .

.. _Pierre-Antoine Champin: http://champin.net/
.. _Michael Mrissa: http://liris.cnrs.fr/~mmrissa
.. _IUT de Lyon 1: http://iut.univ-lyon1.fr/

Contribuer
++++++++++

Toute contribution à ce cours est la bienvenue.

Après avoir cloné ce dépôt,
vous devez exécuter une fois les commandes suivantes
afin de récupérer le thème utilisé ::

  git submodule init
  git submodule update

Vous devez ensuite installer les dépendances (vous aurez besoin de Python 3):

  python3 -m pip install -r requirements.txt

puis, pour générer les documents ::

  make publishable
