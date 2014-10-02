=======================
PDFファイルを作成する
=======================

SphinxではPDF形式でドキュメントを作成することができます。
ここでは、LaTexを経由してPDFを作成する手順を記載します。


MacTeXのインストール
======================

1. MacTeXの `ダウンロードサイト <http://tug.org/mactex/>`_  からインストーラをダウンロードして、MacTeXをインストールします。
	
※そこそこ、時間がかかります。


2. インストールが完了したら、以下のコマンドを実行してTexを更新します。

.. code-block:: bash

	$ sudo tlmgr update --self
	$ sudo tlmgr update --all


-----

Sphinxで行うこと
=================

conf.pyに以下の記述を追加します。

.. code-block:: c

	# 言語の設定
	language = 'ja'

	# LaTeX の docclass 設定
	latex_docclass = {'manual': 'jsbook'}


以下のコマンドを実行します。

.. code-block:: bash

	$ make latex
	$ make latexpdfja



