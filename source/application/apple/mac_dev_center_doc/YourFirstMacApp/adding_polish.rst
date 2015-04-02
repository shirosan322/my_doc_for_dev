======================
磨きをかけよう
======================

見栄えは優れたMac OS Xアプリケーションの重要な要素です。今回のアプリケーションは、今のところ正しく動作していますが、より良くすることができる改善点がいくつかあります。


Number Formatterを追加する
==============================

Sliderを移動すると、float値の最大桁をすべて表示しています。例えば3.141592653589793のように。
一般的にはすべての桁は必要ありません。おそらく3.14で十分です。
formatterオブジェクトを使用することで、数字を丸めた状態で表示することができます。
formatterを使用することで２つのさらなる利益が得られます。

 - formatterは数値入力に最大値と最小値を設定できます。
 - formatterはユーザーの地域によって適切な数値を提供できます。例えば、フランスではユーザーは「3.14」ではなく「3,14」を使用します。

------

number formatterを追加してみよう
-----------------------------------

1. ProjectナビゲータでMainMenu.xibを選択してTrackMixウィンドウを表示してください。

2. Object Library から Number Formatter をTextFieldにドラッグしてください。
 	.. image:: images/adding_polish/30a_dragnumberformatter.png

3. formatterの設定を行うために、canvasの左下にあるディスクロージャーボタンをクリックして、nibファイルのoutlineビューを表示してください。
	.. image:: images/adding_polish/30b_outlinedisclosurebutton.png

4. Number Formatterをクリックしてください。

5. Attributeインスペクターを表示して、Number Formatterを設定します。
	ユーザーの好みを考慮して、だいたいは、short, midium, longといった通常のフォーマットを選択します。今回の場合は、小数点以下第二位まで表示するので、カスタムformatterが必要です。

6. 以下の設定以外はデオフォル値を使用します。
	- Behavior: OS X 10.4+ Custom
	- Minimum: 0
	- Maximum: 11
	- Allows Floats: Yes
	- Localize: Yes
	- Fraction Digits: Minimum 0, Maximum 2

7. Runボタンを押してください
	TextFieldの表示が正しくフォーマットされており、TextFieldに設定した範囲外の値が許可されていないことが分かるはずです。

--------

ウィンドウのリサイズ
======================

現在は、ウィンドウのサイズを変更すると、すべてのUI部品は中心にあり続け、TextFieldとButtonは常に同じサイズで、SliderはWindwサイズに比例してリサイズされます。
残念ながら、Sliderを使えなくなるまでウィンドウを小さくできてしまいます。
これでは、以下の画像のような貧相なレイアウトになってしまいます。

 	.. image:: images/adding_polish/31_badwindowresize.png

 	.. Note::

 		ウィンドウサイズが変更されたとき、UI部品は自分自身をリサイズ、再配置します。これは、「Cocoa Auto Layout」設定を使用しているからです。「Cocoa Auto Layout」はUI部品間の特定の関係を定義したシステムのルールに則っています。
 		このチュートリアルでは、これらの設定を変更する必要はありません。

Windowのリサイズ動作を変更することで、この問題を解決することができる。
ウィンドウのサイズが変更されたときにSliderのサイズが変わらないようにするためのオプションもありますし、ウィンドウの最小サイズを設定することもできます。

ウィンドウのリサイズ動作を変更しよう
------------------------------------

1. MainMenu.xibファイルを選択して、TrackMixウィンドウを表示します。

2. ウィンドウを選択します。

3. Utilityエリアで |size_inspector_icon| のようなアイコンをクリックして、Sizeインスペクターを表示してください。

.. |size_inspector_icon| image:: images/adding_polish/size_inspector_icon.png

4. 「Constraints」にある「Minimum Size」チェックボックスを選択します。

	.. image:: images/adding_polish/32_windowsizeinspector.png

---------

Cocoaシミュレータを使ってアプリケーションをテストしよう
========================================================

時間を節約するために、ビルドやアプリケーションの実行をせずにこれらの変更をテストすることができます。Cocoa Simulatorを使用することで、UI部品が期待通りに動作するかどうかのテストを行えます。
しかし、UI部品が作り直されていることに注意してください。
Cocoa Simulatorはapp delegateを生成ませんし、アプリケーションのロジックはシミュレートしません。
ですので、リサイズ動作やButtonのクリックはテストできますが、SliderやTextFieldは0に設定されません。


Cocoa Simulator を使用してUI操作をテストしよう
-----------------------------------------------

1. 「Editor > Simulate Document」を選択してください。
	Cocoa Simulatorが起動し、nibファイルが読み込まれ操作できるようになります。

2. シミュレータを終了するには、「Cocoa Simulator > Quit Cocoa Simulator」を選択してください。

----------

もしも、インタフェースが期待通りに動作しなかったら、Autosizing設定を見直して、再度試してみてください。
ただし、実際のアプリケーションのテストも行ってください。

-----------

アプリケーションをテストしよう
-------------------------------

- 「Run」ボタンをクリックしてください。
	インタフェースの動作がCocoa Simulatorでテストしたときと同じになっていることを確認してください。

要約
======

以下の内容を実施しました。
	- TextFieldにNumber Formatterを追加
	- ウィンドウリサイズ時の問題を修正
	- コードをコンパイルすることなくUIをテストできるCocoa Simulatorの使い方の学習
