=============================
おすすめテーマ一覧
=============================

sphinxjp.themes.bizstyle
=============================

URL
------

 http://pypi.python.org/pypi/sphinxjp.themes.bizstyle/

 .. image:: images/theme_bizstyle.png


インストール方法
--------------------

 .. code-block:: bash

	easy_install sphinxjp.themes.bizstyle

conf.pyの書き換え
--------------------

 .. code-block:: python

	html_theme = 'bizstyle'

	# 下記オプションでバックグラウンドの色を変更する事が可能です。※必須ではありません
	html_theme_options = {'maincolor' : "#696969"}

--------

Read the Docs Theme（sphinx_rtd_theme）
=============================================

デフォルトのテーマに比べて見やすい。
ウィンドウを大きくしても、画面の横幅がある一定上大きくならないのでページが大きくなると見にくいかもしれない。
ただ、スマートフォン用のWebページには最適かもしれない。

URL
-----

 http://docs.readthedocs.org/en/latest/theme.html
 http://read-the-docs.readthedocs.org/en/latest/theme.html

インストール方法
--------------------

 .. code-block:: bash

	$ pip install sphinx_rtd_theme

conf.pyの書き換え
--------------------

 .. code-block:: python

	import sphinx_rtd_theme

	html_theme = 'sphinx_rtd_theme'

	html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]

--------

Sphinx.Jp
==============

Sphinx.jpのサイトと同じテーマ。

URL
-----

 https://pypi.python.org/pypi/sphinxjp.themes.sphinxjp/0.3.1
 http://pythonhosted.org/sphinxjp.themes.sphinxjp/

インストール方法
--------------------

<pre>$ easy_install sphinxjp.themes.sphinxjp </pre>

conf.py の設定
--------------------

 .. code-block:: python

	extensions = ['sphinxjp.themecore']

	html_theme = 'sphinxjp'

--------

S6
=====

Sphinxを使用してhtmlスライドを作成できるテーマ。

URL
-----

https://pypi.python.org/pypi/sphinxjp.themes.s6/0.3.0
http://pythonhosted.org/sphinxjp.themes.s6/

インストール方法
------------------

 .. code-block:: bash

	$ easy_install sphinxjp.themes.s6

conf.py の設定
--------------------

 .. code-block:: python

	extensions = ['sphinxjp.themes.s6']
	html_theme = 's6'





