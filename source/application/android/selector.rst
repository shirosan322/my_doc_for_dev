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


shape属性
=============
shapeタグ（<sahpe></shape>）には、shape属性（android:shape）が指定できます。
この属性に、以下の表の値をセットする事で形状を変更する事が出来ます。

========== =================================================
値	        概要
========== =================================================
rectangle   四角形(shapeを省略した場合のデフォルト形状)
oval        楕円形
line        線形
ring        同心円形
========== =================================================


cornersタグ
===============
shapeタグの要素としてcornersタ（<corners></corners>）グを記述する事が出来ます。
cornersタグには角の半径を設定するので、角の丸いボタン等を作成する事が出来ます。

============================ ===========================
属性値                        概要
============================ ===========================
android:radius                すべての角に対する半径
android:topLeftRadius         左上の角に対する半径
android:topRightRadius        右上の角に対する半径
android:bottomLeftRadius      左下の角に対する半径
android:bottomRighttRadius    右下の角に対する半径
============================ ===========================


paddingタグ
=============
shapeタグの要素としてpadding（<padding></padding>）タグを記述する事が出来ます。
paddingタグには内側の余白を指定します。

================= =========================
属性値             概要
================= =========================
android:left       左側のパディングを指定
android:top        上側のパディングを指定
android:right      右側のパディングを指定
android:bottom     下側のパディングを指定
================= =========================


sizeタグ
=============
shapeタグの要素としてsizeタグ（<size></size>）を記述する事が出来ます。
sizeタグには、高さと横幅を指定します。

================= =========================
属性値             概要
================= =========================
android:height     高さを指定
android:width      横幅を指定
================= =========================


solidタグ
=============
shapeタグの要素としてsolidタグ（<solid></solid>）を記述する事が出来ます。
solidタグには、色を指定します。

================= =========================
属性値             概要
================= =========================
android:color      色を指定
================= =========================


strokeタグ
=============
shapeタグの要素としてstrokeタグ（<stroke></stroke>）を記述する事が出来ます。
strokeタグには、枠線の太さ、色、点線の間隔等を指定します。

================== =========================================================
属性値              概要
================== =========================================================
android:width       枠線の太さを指定
android:color       枠線の色を指定
android:dashGap     枠線の点線の間隔を指定（これを指定すると枠線が点線になる）
android:dashWidth   枠線の点線の太さを指定
================== =========================================================


gradientタグ
==============
shapeタグの要素としてgradientタグ（<gradient></gradient>）を記述する事が出来ます。
gradientタグの属性値を設定する事で、グラデーションを書ける事が可能です。

========================== ===================================================================
属性値                      概要
========================== ===================================================================
android:angle               グラデーションをかける角度。0は左から右、90は下から上を指す。
                            ※45の倍数である必要がある。デフォルトは0
android:centerX             グラデーションの中心に対する相対的なX座標位置。範囲は0 - 1.0
android:centerY             グラデーションの中心に対する相対的なY座標位置。範囲は0 - 1.0
android:startColor          開始色を設定する。
android:endColor            終了色を設定する。
android:centerColor         開始色と終了色の間の中間色を設定する。
android:gradientRadius      グラデーションの半径を指定する。
android:type                グラデーションパターンの種類を指定する(後述)
========================== ===================================================================

android:typeに指定できるグラデーションパターン
-----------------------------------------------

======= ============================================
設定値    概要
======= ============================================
inear	 線形のグラデーション(デフォルト)
radial	 放射線状のグラデーション
sweep	 走査線のグラデーション
======= ============================================


shapeの記述例
================

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="utf-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android" >
	     <item android:state_pressed="true" >
	         <shape android:shape="oval"  >
	             <corners android:radius="3dip" />
	             <stroke android:width="1dip" android:color="#b7b9ac" />
	             <gradient  android:angle="-90" android:startColor="#a3a890" android:endColor="#d3d5c9"  />            
	         </shape>
	     </item>
	    <item android:state_focused="true">
	         <shape android:shape="oval"  >
	             <corners android:radius="3dip" />
	             <stroke android:width="1dip" android:color="#b7b9ac" />
	             <solid  android:color="#d3d8c2"/>       
	         </shape>
	     </item>  
	    <item >
	        <shape android:shape="oval"  >
	             <corners android:radius="3dip" />
	             <stroke android:width="1dip" android:color="#b7b9ac" />
	             <gradient  android:angle="-90" android:startColor="#fefefe" android:endColor="#d3d8c2" />            
	         </shape>
	     </item>
	</selector>
