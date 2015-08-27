=======
TIPS
=======

- :ref:`カメラの向いている方向に移動する <move_to_camera>`
- :ref:`uGUIの部品を解像度に合わせて表示する <scale_canvas_ugui>`


------

.. _move_to_camera:

カメラの向いている方向に移動する
====================================

``t.TransformDirection(方向)``

Vector3クラスにオブジェクトの方向を表すstaticバリューが宣言されているので、「方向」の部分に以下のいずれかを指定します。

============== 	==========================================
 方向         	value
============== 	==========================================
back	 		Vector3(0, 0, -1)
down 			Vector3(0, -1, 0)
forward 		Vector3(0, 0, 1)
left 			Vector3(-1, 0, 0)
one 	 		Vector3(1, 1, 1)
right 			Vector3(1, 0, 0)
up 				Vector3(0, 1, 0)
zero 			Vector3(0, 0, 0)
============== 	==========================================

例）Y軸方向を固定しながら、カメラが向いている方向にカメラを移動する。

.. code-block:: c#
	:linenos:

	public class Main : MonoBehaviour {
	    public float fSpeed = 0.0f;
	    public GameObject camera = null;

	    // Use this for initialization
	    void Start () {		
	    }
		
	    // Update is called once per frame
	    void Update () {
	        _updatePosition();
	    }

	    private void _updatePosition() {
	        Transform t = camera.transform;
			
	        t.position += t.TransformDirection(Vector3.forward) * fSpeed;
			
	        Vector3 pos = t.transform.position;
	        pos.y = 0.25f;
	        t.transform.position = pos;
	    }
	}



.. _scale_canvas_ugui:

uGUIの部品を解像度に合わせて表示する
====================================

uGUIで画面を作っていて、右上にスコアを表示していた。

Gameビューでゲーム画面を確認しているときは正しく右上に表示されていましたが、
Android端末にインストールして実行したところ、スコア表示が真ん中に寄ってしまい、
テキストの文字も非常に小さくなってしまいました。

どうすりゃいいか分からなかったので、Facebookの「Unityユーザー助け合い所」で質問してみた。
そしたら、超的確な回答をもらったので記録しておく。

1. Canvasのインスペクタより、Canvas Scaler の「Scale Mode」を「Scale With Screen Size」にする
2. Reference Resolution のX, Yを、基準としたい解像度(720*1280など)に設定する
3. 「Screen Match Mode」を「Expand」に変更する。
4. Textのインスペクタより、Rect Transform の Anchor Presets(インスペクタ内左寄りの四角いマーク)をクリックしShift+Altを押しながら右上を指定

これで、バッチリGameビューと同じように右上に表示された。

