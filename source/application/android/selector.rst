######################
selector
######################

==============================
selectorとは
==============================
SelectorはAndroidのdrawableリソースの１つです。

以下のように記述することで、Button等の背景の色や画像を変更することができます。

- 画像を変える場合
	.. code-block:: xml

		android:background="@drawable/button_image"

- 色を変える場合
	.. code-block:: xml

		android:background="#ff0000ff"

しかし、これでは「フォーカスがあるとき」「ボタンが押されたとき」「無効のとき」といった状態によって変化することはありません。
そこで、Selectorを使用する事で **「状態によって」** 画像をや色を差し替えるということが簡単に出来るようになります。


======================
selectorの定義
======================

selector定義ファイルを置く場所
=================================

前述の通り、SelectorはAndroidのdrawableリソースの１つなので、drawableディレクトリに置いておきます。
drawableディレクトリは、"drawable-hdpi", "drawable-ldpi"等がありますが、単なる"drawble"ディレクトリを作成し、
そこに置いておくと、共通で使用できます。


selector定義の書き方
========================

selecterで表現できる状態は、主に下記の５つです。

#. 有効でフォーカスがある状態
#. 無効でフォーカスがある状態
#. 押下状態
#. 無効状態
#. 通常状態（有効でフォーカスがない）

それぞれの状態を、itemタグで（<item></item>）記述していきますが、以下の３つの属性に **true / false** を指定することでこれらの状態を表現します。

* state_focused
* state_enabled
* state_pressed

==================================== =============== =============== ===============
状態                                  state_focused   state_enabled   state_pressed
==================================== =============== =============== ===============
有効でフォーカスがある状態                 true             true          false
無効でフォーカスがある状態                 true             false         false
押下状態                                  true             true          true
無効状態                                  --               false         --
通常状態（有効でフォーカスがない）          --               --            --
==================================== =============== =============== ===============

selecterのxmlで指定する<item>タグは、上から順に評価されるため、各々の状態で別のdrawableを指定したい場合は、
順番に注意して記述しましょう。


selector 定義用 xml ファイルの記述例
=======================================

例）color_button.xml

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="UTF-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android">
	    <!-- 有効でフォーカスがある状態 -->
	    <item
	        android:state_focused="true"
	        android:state_enabled="true"
	        android:state_pressed="false"
	        android:drawable="@drawable/undo_focused" />

	    <!-- 無効でフォーカスがある状態 -->
	    <item
	        android:state_focused="true"
	        android:state_enabled="false"
	        android:state_pressed="false"
	        android:drawable="@drawable/undo_disabled_focused" />

	    <!-- 押下状態 -->
	    <item
	        android:state_focused="true"
	        android:state_enabled="true"
	        android:state_pressed="true"
	        android:drawable="@drawable/undo_pressed" />

	    <!-- 無効状態 -->
	    <item
	        android:state_enabled="false"
	        android:drawable="@drawable/undo_disabled" />

	    <!--通常状態（有効でフォーカスがない） -->
	    <item
	        android:drawable="@drawable/undo_normal" />
	</selector>

状態によって変更したいのが画像ではなく背景色の場合は、上記のdrawable属性をcolor属性に変更して色を指定すれば良い。

 .. code-block:: xml

	    <!-- 有効でフォーカスがある状態 -->
	    <item
	        android:state_focused="true"
	        android:state_enabled="true"
	        android:state_pressed="false"
	        android:color="#ff00ff" />


======================
selectorを使用する
======================

Button等のbackground属性に"@drawable/セレクター名"を指定することで、ウィジェットの状態によってselectorで指定した画像や背景色に自動的に切り替わります。

例）

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:orientation="vertical"
	    android:layout_width="fill_parent"
	    android:layout_height="fill_parent"
	    >
	    <Button
	        style="@style/myButtonStyle1"
	        android:layout_width="fill_parent" 
	        android:layout_height="wrap_content" 
	        android:text="Button1"
	        android:background="@drawable/color_button" />
	</LinearLayout>


======================
shapeを使ってみる
======================

shapeタグを使うと、「形状を変える」「角を丸くする」「背景色をグラデーションにする」等のことが簡単に実現できます。

------------------------
shape属性
------------------------
========== =================================================
値	        概要
========== =================================================
rectangle   四角形(shapeを省略した場合のデフォルト形状)
oval        楕円形
line        線形
ring        同心円形
========== =================================================




