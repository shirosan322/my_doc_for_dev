=======
TIPS
=======

:ref:`カメラの向いている方向に移動する <move_to_camera>`


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


