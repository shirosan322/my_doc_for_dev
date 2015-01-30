=====================================
ドキュメントベース・アプリケーション
=====================================


Document Base Applicationで気をつけること
=============================================

Document Base Applicationを作っていると、まずApplication(NSApplicationのサブクラス)、myDocument(NSDocumentのサブクラス)とWindowControllerのサブクラスをどう協調させていけばいいかに悩みます。

そこで、まずはどういう順番で、どのクラスのどのメソッドが呼ばれるか調べてみました。
結果は以下の通りでした。

Application - init
Application - awakeFromNib
MyDocument - init
MyDocument - makeWindowControllers
WindowController - init
WindowController - awakeFromNib
MyDocument - awakeFromNib
Application - applicationDidFinishLaunching
あとは initとawakeFromNibの関係ですが、

initは、IBOutletではないインスタンスの初期化メソッド
awakeFromNibは、IBOutletとインターフェースビルダーでバインドしたオブジェクトがセットされた後呼び出され、outletの設定・初期化を行うためのメソッド
と、考えておけば良さそうです。
そう考えると、MyDocumnent.xibのFile's OwnerであるMyDocmentクラスが、xibの内部にある各オブジェクトの初期化が終わって、アウトレットとのバインドが終わるまでawakeFromNibが呼ばれない事に辻褄が合います。

