################
uGUI
################

*****************************************
uGUIをスクリプトから利用する方法
*****************************************

1. スクリプトに以下の記述を追加してUIパッケージを追加します.

 .. code-block:: c#

	using UnityEngine.UI;


2. スクリプトに、追加したUI部品の変数を追加します。

 UI部品のクラス名は、追加するときのメニューと同じです。

 .. image:: images/use_ugui.png

 以下のようにpublic変数を追加します.

 .. code-block:: c#

	public Text msgText;
 	public InputField field;


3. Canvasに作成したスクリプトを追加します.

4. Inspectorで追加した変数に、	作成したUIを割り当てます.




