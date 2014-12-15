===============================
Xcode4以降でGCCを利用する方法
===============================

GCC4.2を利用する
==================

Xcode4では、「gcc-4.2」がインストール時に「{$XCODE_HOME}/usr/bin」に追加されています。
この「gcc-4.2」をXcodeから利用できるようにファイルを修正します。

1. 以下のディレクトリファイルをエディタで開きます.

 .. code-block:: bash

	$ subl "/Developer/Applications/Xcode.app/Contents/PlugIns/Xcode3Core.ideplugin/Contents/SharedSupport/Developer/Library/Xcode/Plug-ins/GCC 4.2.xcplugin/Contents/Resources/GCC 4.2.xcspec"

2. 以下の項目を修正します.

 .. code-block:: text

	ShowInCompilerSelectionPopup = NO;
	IsNoLongerSupported = YES;

	↓

	ShowInCompilerSelectionPopup = NO;
	IsNoLongerSupported = YES;

3. Xcodeを再起動する.

 Xcodeを再起動すると、コンパイラの選択項目に「GCC 4.2」が追加されています.


GCC 4.0を利用する
=======================

Xcode4.2等でGCC 4.0を利用する場合はもう少し複雑になります。順を追って見ていきましょう。

1. Xcode3 をインストールする
--------------------------------

1. 以下のコマンドを実行してディレクトリを作成しておきます.

 .. code-block:: bash

 	$ sudo mkdir /Xcode3

2. Mac Dev Center より、Xcode 3のインストーラーをダウンロードしてくる.

3. インストーラーを起動し「インストールの種類」の段階まで「続ける」ボタンを押して進めます.

4. パッケージ名の「SystemTools」「Unix Dev Support」「ドキュメンテーション」のチェックを外し、「Mac OS X 10.4 Support」にチェックします.

5. 場所の「Develop」となっているところを選択し、インストール先を1.で作成した「/Xcode3」に変更します.

6. 「続ける」を押して、インストールを実行します.


2. Xcode3のSDKをXcode4で利用できるようにする
---------------------------------------------

1. 以下のディレクトリに移動します

 .. code-block:: bash

 	$ cd /Developer/SDKs

2. 以下のコマンドを実行して、シンボリックリンクを作成します.

 ※10.4しか使用しない場合は、10.4だけで構いません。

 .. code-block:: bash

 	$ sudo ln -s /Xcode3/SDKs/MacOSX10.4u.sdk ./MacOSX10.4u.sdk
 	$ sudo ln -s /Xcode3/SDKs/MacOSX10.5.sdk ./MacOSX10.5.sdk

 ※ここではシンボリックリンクを作成していますが、直接コピーしても構いません。

3. GCC 4.0 を使用できるようにする
-------------------------------------

1. 以下のコマンドを実行して、「gcc-4.0」を利用できるようにします.

 .. code-block:: bash

 	$ cd /Developer/usr/bin
 	$ sudo ln -s /Xcode3/usr/bin/gcc-4.0 ./gcc-4.0
 	$ cd /Developer/usr/libexec/gcc/powerpc-apple-darwin10
	$ sudo ln -s /Xcode3/usr/libexec/gcc/powerpc-apple-darwin10/4.0.1 ./4.0.1

2. 以下のコマンドを実行して、Build Setting で「GCC 4.0」を選択できるようにします.

 .. code-block:: bash

 	$ cd /Developer/Library/Xcode/PrivatePlugIns
	$ cd Xcode3Core.ideplugin/Contents/SharedSupport/Developer/Library/Xcode/Plug-ins
	$ sudo ln -s "/Xcode3/Library/Xcode/Plug-ins/GCC 4.0.xcplugin" ./GCC\ 4.0.xcplugin


4. GCC 4.0用に、PPCに対応する
----------------------------------
Appleは、Xcdoe4では、Intelプラットフォームのみをサポートしているので、GCC4.0はPPCをサポートしてビルドされていません。
GCC4.0でPPC/PPC64バイナリをコンパイルするためには、それに対応した「as」という名前のGNUアセンブラが必要です。
そこで、PPCに対応したXcode3の「as」のシンボリックリンクを作成します。


1. 以下のディレクトリに移動する.

 .. code-block:: bash

 	$ cd /Developer/usr/libexec/gcc/powerpc-apple-drawin10/4.2.0

2. 元々の「as」のバックアップをとっておき、Xcode3の「as」のシンボリックリンクを作成する.

 .. code-block:: bash

 	$ sudo mv as as.bak
 	$ sudl ln -s /Xcode3/usr/bin/as ./as


