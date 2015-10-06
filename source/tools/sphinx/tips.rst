########################
TIPS
########################


目次
=======

- :ref:`自動ビルドできるようにしたい<add_auto_build>`
- :ref:`"sphinx-quickstart"で生成されるデフォルトのMakeifileの内容を変更したい<change_default_makefile>`


----


.. _add_auto_build:

---------------------------------
自動ビルドできるようにしたい
---------------------------------

Sphinxでhtmlのドキュメントを生成するときは以下のコマンドを実行します。

 .. code-block:: bash

	$ make html

ですが、ドキュメントを更新するたびにコマンドを打ち込むのは非常に面倒なので、この作業を自動化したい。

「sphinx-autobuild」を利用することで、rstファイルを変更し、保存した時点で自動的にビルドされブラウザに反映されるようになります。

手順を見ていきましょう。

1. sphinx-autobuildをインストールします

 .. code-block:: bash

	$ pip install sphinx-autobuild

2. Makefile を編集し、自動ビルド用の target を「livehtml」という名前で追加します

 - help の表示項目に「livehtml」を追加

  .. code-block:: makefile

  	 :
  	 :
	help:
	    @echo "Please use \`make <target>' where <target> is one of"
	    @echo "  html       to make standalone HTML files"
	     :
	     :
	    @echo "  livehtml   to run sphinx autobuild" <-- この行を追加
	     :
	     :

 - targetを追加する

  .. code-block:: makefile

  	 :
  	 :
	xml:
	    $(SPHINXBUILD) -b xml $(ALLSPHINXOPTS) $(BUILDDIR)/xml
	    @echo
	    @echo "Build finished. The XML files are in $(BUILDDIR)/xml."

	pseudoxml:
	    $(SPHINXBUILD) -b pseudoxml $(ALLSPHINXOPTS) $(BUILDDIR)/pseudoxml
	    @echo
	    @echo "Build finished. The pseudo-XML files are in $(BUILDDIR)/pseudoxml."

	livehtml:
	    sphinx-autobuild -b html $(ALLSPHINXOPTS) $(BUILDDIR)/html
	    @echo
	    @echo "sphinx autobuild started."
	 :
	 :

3. SphinxのMakefileがあるディレクトリで以下のコマンドを実行する

 .. code-block:: bash

	$ make livehtml

4. ブラウザで「http://127.0.0.1:8000/」を開く

これで、rstファイルを変更して保存した場合に、自動的にビルドが実行され、ドキュメントが更新されます。

.. note::

	**ドキュメントが更新されない場合は、ページをリロードしてみましょう！**

.. note::

	毎回Makefileを変更するのが面倒な場合は、"sphinx-quickstart"でMakefileが生成されるときに追加されているようにしましょう。

	デフォルトのMakefileを変更する場合は :ref:`こちら <change_default_makefile>` を参照してください。

	


-----

.. _change_default_makefile:

------------------------------------------------------------------------
"sphinx-quickstart"で生成されるデフォルトのMakeifileの内容を変更したい
------------------------------------------------------------------------

以下の場所にある「quickstart.py」ファイルを編集します。

 .. code-block:: bash

	~/.pyenv/versions/2.7.8/lib/python2.7/site-packages/sphinx/quickstart.py

 .. note::

	**※上記の例では「pyenv」でインストールしたpythonのsphinxを使用している場合なので、
	環境によってはパスが異なります。**

	**※"2.7.8" は、使用しているpythonのバージョンなので、この部分はお使いの環境に合わせて変更して下さい。**

quickstart.py をエディタで開くと以下のような内容になっています。

 .. code-block:: python

	# -*- coding: utf-8 -*-
	"""
	    sphinx.quickstart
	    ~~~~~~~~~~~~~~~~~

	    Quickly setup documentation source to work with Sphinx.

	    :copyright: Copyright 2007-2014 by the Sphinx team, see AUTHORS.
	    :license: BSD, see LICENSE for details.
	"""

	import sys, os, time, re
	from os import path

	TERM_ENCODING = getattr(sys.stdin, 'encoding', None)

	from docutils.utils import column_width

	from sphinx import __version__

	 :
	 :
	 :

このファイルの「MAKEFILE」の項目を編集することで、"sphinx-quickstart"で生成されるデフォルトのMakefileの内容を変更することができます。


