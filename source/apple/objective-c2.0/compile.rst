
.. index:: Compile(コンパイル方法)

コンパイル
=====================

- コンパイルとリンクを同時に行う

.. code-block:: bash

	$ clang -o xxx main.m hoge.m -framework Foundation

- オブジェクトを作成してからリンクする方法

.. code-block:: bash

	$ clang -c main.m
	$ clang -c hoge.m
	$ clang -o xxx main.o hoge.o -framework Foundation

.. Note::

	「xxx」は実行ファイル名



