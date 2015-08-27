######################
Style
######################

==============================
style（スタイル）とは
==============================
スタイルとは、レイアウト属性とその値のセットをいくつか組み合わせて、1つのIDで使用できるように定義したものです。
スタイルを使うことでビューやウィンドウの持ついくつもの属性に関する設定値をまとめて扱うことができます。

たとえば、TextViewの場合、テキストのフォントやサイズ、ビューの幅・高さといった属性がありますが、
これらの属性に関する設定値をひとつのスタイルとして定義しておくことができます。
そして、TextViewをしようするとこきに、TextViewのstyle属性に定義したスタイルを指定すれば、
定義したスタイルに記述されている各属性を一括で設定することが可能です。

属性値を一括で管理できるため、属性値の変更を行う際に変更箇所を減らすことができます。



======================
styleの定義
======================

style定義ファイルを置く場所
================================
スタイルファイルは、"res/values" に配置する事で、レイアウト定義ファイルやソースコードからアクセスできるようになります。
ソースコードからはリソースインデックス（R.style.***）でアクセスします。


style定義の書き方
======================
styleの定義は、style要素(<style>～</style>)に、name属性とitem要素(<item>～</item>)を定義します。

.. code-block:: xml
	:linenos:

 	<style name="myButtonStyle1">
	    <item name="android:textSize">15sp</item>
	    <item name="android:textStyle">bold</item>
	    <item name="android:textColor">#FFFFFF</item>
	    <item name="android:gravity">center</item>
	    <item name="android:background">@drawable/my_button</item>
	    <item name="android:padding">10dip</item>
	</style>

もしも、styleを継承する場合は、parent属性に親となるスタイル（@style/親のスタイル名）を設定します。

.. code-block:: xml
	:linenos:

 	<style name="myButtonStyle2" parent="@style/myButtonStyle1">
	    <item name="android:shadowColor">#000000</item>
	    <item name="android:shadowDx">1</item>
	    <item name="android:shadowDy">1</item>
	    <item name="android:shadowRadius">0.6</item>
	</style>

システムのButtonのスタイルを継承する場合は、以下のようにします。

.. code-block:: xml
	:linenos:

 	<style name="myButtonStyle" parent="@android:style/Widget.Button">
 	    :
 	    :
	</style>


style定義用 xml ファイルの記述例
=======================================

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="utf-8"?>
	<resources>
	    <style name="myTextStyle">
	        <item name="android:layout_width">fill_parent</item>
	        <item name="android:layout_height">wrap_content</item>
	        <item name="android:background">#ffffff</item>
	        <item name="android:textColor">#000000</item>
	    </style>

 	    <style name="myButtonStyle1" parent="@android:style/Widget.Button">
	        <item name="android:textSize">15sp</item>
	        <item name="android:textStyle">bold</item>
	        <item name="android:textColor">#FFFFFF</item>
	        <item name="android:gravity">center</item>
	        <item name="android:background">@drawable/my_button</item>
	        <item name="android:padding">10dip</item>
	    </style>

	    <style name="myButtonStyle2" parent="@style/myButtonStyle1">
	        <item name="android:shadowColor">#000000</item>
	        <item name="android:shadowDx">1</item>
	        <item name="android:shadowDy">1</item>
	        <item name="android:shadowRadius">0.6</item>
	    </style>
	</resources>


======================
styleを使用する
======================

レイアウトやウィジェットのstyle属性に"@style/スタイル名"を指定することで、定義したスタイルを適用することができます。

例）

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:orientation="vertical"
	    android:layout_width="fill_parent"
	    android:layout_height="fill_parent"
	    >
	    <TextView
	        style="@style/myTextStyle"
	        android:text="MyText" />

	    <Button
	        style="@style/myButtonStyle1"
	        android:layout_width="fill_parent" 
	        android:layout_height="wrap_content" 
	        android:text="Button1" />

	    <Button
	        style="@style/myButtonStyle2"
	        android:layout_width="fill_parent" 
	        android:layout_height="wrap_content" 
	        android:text="Button2" />
	</LinearLayout>

