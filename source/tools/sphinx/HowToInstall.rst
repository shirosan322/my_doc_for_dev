=============
インストール
=============

ここでは、各環境にSphinxをインストールする手順を紹介します。


Mac
===

------------------------
Pythonをインストールする
------------------------


1.1. 「pyenv」をインストールする
--------------------------------

「pyenv」はPythonのバージョン管理ツールで、複数のバージョンのPythonを使い分けたりする場合に非常に便利です。rubyでいう「rbenv」と同じようなものです。
「pyenv」はHomebrewでインストールできるので、以下のコマンドを実行しましょう。

.. code-block:: bash

   $ brew install pyenv


インストールが完了したら、「~/.bash_profile」に以下の記述を追加する

.. code-block:: bash

   if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi


1.2. pyenvでPythonをインストールする
------------------------------------

1. Pythonのバージョンを確認する
まずは、以下のコマンドを実行してインストールできるPythonのバージョンを確認しましょう。

.. code-block:: bash

   $ pyenv install -l
   Available versions:
      2.1.3
      2.2.3
      :
      2.7.7
      :
      3.4.1
      anaconda-1.4.0
      :

2. Pythonをインストールする
以下のコマンドを実行してバージョンを指定してPythonをインストールします

.. code-block:: bash

   $ pyenv install <インストールするバージョン>

   例えば、2.7.7をインストールする場合は...

   $ pyenv install 2.7.7 

これで、指定したバージョンのpythonのインストールが始まる

3. 使用しているPython（がインストールされている場所）を確認する
※システムのpythonでなく、pyenvでインストールしたpythonが使用されているかを確認するために行います
以下のコマンドを実行してください。

.. code-block:: bash

   $ which python
   /Users/hoge/.pyenv/shims/python

となっていればOK。

4. pyenvでインストールしたpythonのバージョンを確認する
以下のコマンドを実行することで、pyenvでインストールしたPythonのバージョンが一覧表示されます。
例）2.7.7と3.4.1がインストールされている場合

.. code-block:: bash
   
   $ pyenv versions
     system
   * 2.7.7 (set by /Users/hoge/.pyenv/version)
     3.4.1

5. 以下のコマンドを実行して使用するPythonを決定する

.. code-block:: bash

   $ pyenv global 2.7.7
   $ pyenv rehash


---------------------------
2. Sphinxをインストールする
---------------------------

2.1. pipをインストールする
---------------------------

「pip」とはPythonのパッケージ管理システムで、rubyでいうところの「gem」のようなものです。
Pythonのパッケージ管理システムには「easy_install」というツールもありますが、「pip」はこの「easy_install」に置き換わる存在として開発が進められているようです。
ということで、ここでは「pip」を利用することにします。

.. raw:: html

   <font color="red">pyenvを利用している場合は、pipもインストールされているので、この手順は省いても構いません。</font><br>

   <font color="blue">もしも、システムのPythonをそのまま利用している方は、以下のコマンドを実行して「pip」をインストールしましょう。</font>


.. code-block:: bash

   $ easy_install pip


2.2. Sphinxをインストールする
------------------------------

SphinxをPythonのパッケージとして提供されているので、以下のコマンドを実行し、「pip」を利用して「Sphinx」をインストールしましょう。

.. code-block:: bash

   $ pip install sphinx


以上で「Sphinx」のインストールは完了です。