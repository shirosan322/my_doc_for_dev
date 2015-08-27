=======
TIPS
=======

- :ref:`カメラの向いている方向に移動する <move_to_camera>`
- :ref:`uGUIの部品を解像度に合わせて表示する <scale_canvas_ugui>`
- :ref:`別のSceneを開く <open_other_scene>`
- :ref:`Thetaの画像をUnityで見る <view_image_of_theta>`
- :ref:`カメラの向いている方向に移動する <move_to_camera>`
- :ref:`PointerEventData から Hit したオブジェクトを取得する <raycast_hit_obj>`


------

.. _open_other_scene:

別のSceneを開く
===========================

1. [File - Build Settings...]を選択して、[Scenes in Build]にロードしたいSceneをドラッグ＆ドロップで追加する.

2. 以下の関数を呼び出す.

 .. code-block:: c#

 	public static void LoadLevel(int index);
 	public static void LoadLevel(string name);


 ============= ==========================
 パラメーター
 ============= ==========================
 index		  ロードするレベルのインデックス
 name		  ロードするレベルの名前
 ============= ==========================


.. _view_image_of_theta:

Thetaの画像をUnityで見る
===========================

1. Thetaで撮影した全天球画像を取り込む.

2. 取り込んだ画像を選択して、Inspectorから[Texture Type]を[CubeMap]に変更し、[Mapping]を[Latitude-Longitude Layout(Cylindrical)]にして[Apply]を押す.

 .. image:: images/theta_image_for_unity1.png

3. 新しくマテリアルを作成する.

 .. image:: images/theta_image_for_unity2.png


4. 作成したマテリアルの[Shader]を[Skybox]->[CubeMap]に変更する.

 .. image:: images/theta_image_for_unity3.png

5. CubeMapという項目のCubemap(HDR)の[Select]ボタンを押して、先ほど[Texture Type]を[CubeMap]に変更した全天球画像をセットする.

 .. image:: images/theta_image_for_unity4.png

6. メニューの[Window - Lighting]を選択する.

 .. image:: images/theta_image_for_unity5.png

7. [Lighting]ウィンドウの[Scene]タブを選択し、[Environment Lighting]の[Skybox]にさっき作ったマテリアルをセットする.

 .. image:: images/theta_image_for_unity6.png


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


.. _raycast_hit_obj:

PointerEventData から Hit したオブジェクトを取得する
========================================================

Ex. PointerDownのEventDataから、反応したGameObjectを取得して、HogeHogeと同じかチェックする.

.. code-block:: c#
	:linenos:

	public void OnPointerDown(PointerEventData eventData) {
		if (eventData.pointerPressRaycast.gameObject == HogeHoge) {
		}
	}

>>>>>>> Stashed changes

