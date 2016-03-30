###################
Google Test
###################

******************************
XCodeでGoogleTestを利用する
******************************

gtest.frameworkを作成する
===================================

1. 以下のサイトから「googletest」をダウンロードします。「googletest」は「Google Code」で公開されています。

 https://code.google.com/p/googletest/

 もしくは、以下のコマンドを実行してリポジトリからチェックアウトしてください。

 .. code-block:: bash

	$ svn co http://http://googletest.googlecode.com/svn/trunk/ googletest-read-only

 「googletest-read-only」はディレクトリ名なので、何を指定しても構いません。

2. 「xcode」というディレクトリがあるので、その中の「gtest.xcodeproje」を開きます。

3. 開いたプロジェクトをビルドし、gtest.frameworksを作成します。

4. 「Product - Archive」メニューを選択し、「Export」ボタンを押して、「Save Built Products」が選択されている事を確認し、「Next」ボタンを押します。

5. 出力先を選択し「OK」ボタンを押します。

6. 選択した出力先にディレクトリが作成され、「Library - Frameworks」に「gtest.framework」が保存されている事を確認します。

GoogleTestを使用する
===================================

1. テストを実行したいプロジェクトに「Command Line Tools」のターゲットを追加し、「UnitTests」等の適当な名前を付けておきます。

2. 「gtest.framework」をプロジェクトに追加します。すると、「UnitTests」の「Build Phases - Link Binary with Libraries」に「gtest.framework」が追加されます。

3. 「UnitTests」の「Build Settings」の「Apple LLVM 6.0 - Language - C++ - C++ Standard Library」の項目を「libstdc++(GNU CLL standard library)」に変更します。

 ※これをしないとリンクエラーが発生します。




