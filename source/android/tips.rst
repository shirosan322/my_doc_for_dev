==========
TIPS
==========

目次
=======

- :ref:`EditTextのカーソルの色を変更したい<change_edittext_cursor_color>`



.. _change_edittext_cursor_color:

------------------------------------
EditTextのカーソルの色を変更したい
------------------------------------

背景色を黒にしたときにEditTextが編集状態になってもカーソルが表示されない問題がありました。
これは、カーソルの色が黒なので背景と同化してしまっているためです。
そこで、EditTextの色を変更してあげればいい見えるようになるだろうと考えました。
「プロパティかなんかで簡単に変更できるやろう」と思っていましたが、ありませんでした。。。
それくらい用意しといてくださいよ Google さん(-3-)

代わりにカーソルの画像を変更するプロパティがあったので、これを利用します。
手順としては以下の通りです。

1. 白い長方形を作成する.
2. EditTextの背景に1.の長方形を指定する.

では、順番に見ていきましょう。

1. 白い長方形を作成する
--------------------------
「res/drawable」ディレクトリに「edit_text_cursor.xml」作成し、以下のように記述します。

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="utf-8"?>
	<shape
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:shape="rectangle">

		<size android:width="1dp" />
		<solid android:color="#ffffff" />
	</shape>

2. EditTextの背景に1.の長方形を指定する
--------------------------------------------
「textCursorDrawbale」要素に1.で作成したxmlを指定する.

.. code-block:: xml
	:linenos:

	<EditText 
        android:id="@+id/file_name_edit"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:textSize="20sp"
        android:textColor="#FFFFFF"
        android:textCursorDrawable="@drawable/edit_text_cursor" />





