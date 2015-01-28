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

Pour installer localement les sources et générer les fichiers HTML,
vous avez besoin de Sphinx_ et Hieroglyph_ ,
ainsi que de l'extension Seqdiag_.

Après avoir cloné ce dépôt,
vous devez exécuter une fois les commandes suivantes
afin de récupérer le thème utilisé ::

  git submodule init
  git submodule update

puis, pour générer les documents ::

  make publishable

.. _Sphinx: http://sphinx-doc.org/
.. _Hieroglyph: http://hieroglyph.io/
.. _Seqdiag: http://blockdiag.com/en/seqdiag/sphinxcontrib.html
