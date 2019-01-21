:orphan:

Cache
=====

Diagrammes de séquence
++++++++++++++++++++++

.. TODO intro ?

.. rst-class:: scrollable

ETag
----

.. seqdiag::

   seqdiag {
      A [label=Client]
      B [label=Server]

      A  -> B [label="GET /foo"] ;
      A <-  B [label="200 OK\nEtag: \"abc\""] ;
      A  -> B [label="GET /foo\nIf-none-match: \"abc\""] ;
      A <-- B [label="304 Not Modified"] ;
      ... Resource changes ...
      A  -> B [label="GET /foo\nIf-none-match: \"abc\""] ;
      A <-  B [label="200 OK\nEtag: \"cde\""] ;
   }

Premier échange
---------------

.. seqdiag::

   seqdiag {
      A [label=Client]
      B [label=Cache]
      C [label=Server]

      A -> B -> C [label="GET /foo"] ;
      B <- C [label="200 OK\nEtag: \"abc\"",
              leftnote="store entity\nwith etag"] ;
      A <- B [label="200 OK\nEtag: \"abc\""] ;
   }

Échange suivant
---------------

.. seqdiag::

   seqdiag {
      A [label=Client]
      B [label=Cache]
      C [label=Server]

      A -> B [label="GET /foo"] ;
      B -> C [label="GET /foo\nIf-none-match: \"abc\""] ;
      B <-- C [label="304 Not Modified"] ;
      A <- B [note="retrieve entity\nfrom cache",
              label="200 OK\nEtag: \"abc\""] ;
   }

Après modification
------------------

.. seqdiag::

   seqdiag {
      A [label=Client]
      B [label=Cache]
      C [label=Server]

      A -> B [label="GET /foo"] ;
      B -> C [label="GET /foo\nIf-none-match: \"abc\""] ;
      B <- C [label="200 OK\nEtag: \"cde\"",
              leftnote="update entity\nand etag"];
      A <- B [label="200 OK\nEtag: \"cde\""] ;
   }

.. rst-class:: scrollable

Durée de validité
-----------------

.. seqdiag::

   seqdiag {
      A [label=Client]
      B [label=Cache]
      C [label=Server]

      A -> B -> C [label="GET /foo"] ;
      B <- C [label="200 OK\nEtag: \"abc\"\nCache-control: max-age=10",
              leftnote="store entity\nwith etag\nand max-age"];
      A <- B [label="200 OK\nEtag: \"abc\""] ;
      === 1s ===
      A -> B [label="GET /foo", note="cached entity\nis up-to-date"] ;
      A <- B [label="200 OK\nEtag: \"abc\""] ;
      === 20s ===
      A -> B [label="GET /foo", note="cached entity\nhas expired"] ;
      B -> C [label="GET /foo\nIf-none-match: \"abc\""] ;
      B <-- C [label="304 Not Modified\nCache-control: max-age=10",
               leftnote="update max-age"] ;
      A <- B [note="retrieve entity\nfrom cache",
              label="200 OK\nEtag: \"abc\""] ;
   }

Utilisation avec Apache Components
----------------------------------

Installation maven__

__ http://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient-cache

.. code-block:: java

        CacheConfig cacheConfig = CacheConfig.custom()
                .setMaxCacheEntries(1000)
                .setMaxObjectSize(8192)
                .build();
        CloseableHttpClient cachingClient = CachingHttpClients.custom()
                .setCacheConfig(cacheConfig)
                .build();
