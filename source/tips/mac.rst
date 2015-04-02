=================
MAC関係TIPS
=================

Finderのクイックルックでテキストのコピーを可能にする
====================================================
デフォルトの設定では、クイックルックでファイルを開いた場合はテキストがコピーできません。
ちょっとコピーするだけなら、クイックルックからできると楽です。
そこで、ターミナルで以下のコマンドを入力すると設定を変更できます。

- コピー可能にする

 .. code-block:: bash

	$ defaults write com.apple.finder QLEnableTextSelection -bool true
	$ killall Finder


- コピー不可にする（元に戻す）

 .. code-block:: bash

	$ defaults write com.apple.finder QLEnableTextSelection -bool false
	$ killall Finder


Terminal.appの「ls」の表示を色分けする
==========================================
macのターミナルで「ls」と実行すると色分けがされない。
「ls」のオプションで「-G」を付けて、以下のように実行すると色分けされる

 .. code-block:: bash

	$ ls -G

ただし、毎回これを入力するのは面倒なので、「.bash_profile」でエイリアス設定しておきます
「.bash_profile」を編集し以下の記述を追加して下さい。

 .. code-block:: text

	alias ls='ls -G'

隠しファイル・フォルダの表示／非表示
=========================================

- 表示

 .. code-block:: bash

	$ defaults write com.apple.finder AppleShowAllFiles TRUE
	$ killall Finder

- 非表示

 .. code-block:: bash

	$ defaults write com.apple.finder AppleShowAllFiles FALSE
	$ killall Finder


