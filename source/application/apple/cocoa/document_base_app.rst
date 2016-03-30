=====================================
ドキュメントベース・アプリケーション
=====================================

WindowControllerをサブクラス化するときとしないとき
===================================================

WindowControllerをサブクラス化しない場合
-----------------------------------------
WindowControllerをサブクラスかしない場合は、デフォルトのWindowControllerが使用されます。

NSDocumentのサブクラスでオーバーライドする関数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- \- (NSString*)windowNibName
	- DoumentのNibファイルのファイル名を返します。(拡張子は除く)
	- ここで、DocumentとデフォルトのWindowControllerが関連づけられる。

 .. code-block:: objective-c

	- (NSString*)windowNibName
	{
	    /// Override returning the nib file name of the document
	    /// If you need to use a subclass of NSWindowController or 
	    /// if your document supports multiple NSWindowControllers,
	    /// you should remove this method and override -makeWindowControllers instead.
	
	    return @"MyDocument";
	}


- \- (void)windowControllerDidLoadNib:(NSWindowController \*) aController

	- DocumentがNibファイルの「File's Owner」である場合に、Nibファイルがロードされた後に呼び出される。
	- Controllerの初期化等をここで行う.


 .. code-block:: objective-c

	- (void)windowControllerDidLoadNib:(NSWindowController *) aController
	{
	    [super windowControllerDidLoadNib:aController];

	    // implements something to initialize.
	}


WindowControllerをサブクラス化する場合
-----------------------------------------
NSDocumentのサブクラスでオーバーライドする関数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- \- (void)makeWindowControllers

	- ここで、サブクラス化した自前のWindowControllerを生成します。
	- 生成したWindowControllerをDocumentに追加します。(addWindowControllerを呼び出す。)
		- このタイミングで、DocumentのWindowController管理変数に生成したWindowControllerが追加され、WindowControllerの「document」にもDocumentのインスタンスがSetされ関連づけが完了する。

 .. code-block:: objective-c

	- (void)makeWindowControllers {
	    mMyWindowController = [[[CKwvWindowController alloc]
	                             initWithWindowNibName:@"MyDocument"] autorelease];

	    // ここでWindowControllerとDocumentが関連づけられる.
	    [self addWindowController:mMyWindowController];
	}

NSWindowControllerのサブクラスでオーバーライドする関数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
サブクラス化したxrをしようする場合は、MyDocument.nibの「File's Owner」は作成したWindowControllerにします。
その場合は、nibが

- \- (void)windowDidLoad

 .. code-block:: objective-c

	- (void)windowDidLoad {
	    [super windowDidLoad];
	    
	    // Implement this method to handle any initialization after your window controller's window has been loaded from its nib file.
	}


Document Base Applicationで気をつけること
=============================================

Document Base Applicationを作っていると、まずApplication(NSApplicationのサブクラス)、myDocument(NSDocumentのサブクラス)とWindowControllerのサブクラスをどう協調させていけばいいかに悩みます。

そこで、まずはどういう順番で、どのクラスのどのメソッドが呼ばれるか調べてみました。
結果は以下の通りでした。

- Application - init
- Application - awakeFromNib
- MyDocument - init
- MyDocument - makeWindowControllers
- WindowController - init
- WindowController - awakeFromNib
- MyDocument - awakeFromNib
- Application - applicationDidFinishLaunching

あとは initとawakeFromNibの関係ですが、

initは、IBOutletではないインスタンスの初期化メソッド
awakeFromNibは、IBOutletとインターフェースビルダーでバインドしたオブジェクトがセットされた後呼び出され、outletの設定・初期化を行うためのメソッド
と、考えておけば良さそうです。
そう考えると、MyDocumnent.xibのFile's OwnerであるMyDocmentクラスが、xibの内部にある各オブジェクトの初期化が終わって、アウトレットとのバインドが終わるまでawakeFromNibが呼ばれない事に辻褄が合います。







NSViewController の注意点
==============================

.. warning::

	NSResponder を継承しているのに、デフォルトだとレスポンダチェーンに含まれません！！
	なんでやねん！！

そのままでは、TargetをFirst Responder に指定したアクションに応答してくれません。
なので、自分自身をレスポンダチェーンに追加してあげる必要があります。

NSViewController のサブクラスに以下のメソッドを追加します。

.. code-block:: objective-c
	:linenos:

	- (void)viewWasAddedToSuperView {
	    // NSViewControllerはデフォルトでは Responder Chain に含まれないので、自分を Responder Chain に追加する.
	    NSView *view = [self view];
	    NSResponder *next = [view nextResponder];
	    [view setNextResponder:self];
	    [self setNextResponder:next];
	}

このViewControllerが管理してるViewのNextREsponderとして自分自身をセットし、元々NextResponderとして設定されていたものを、ViewControllerのNextResponderとして設定します。


ViewとViewControllerが関連づけられた後で、このメソッドを呼び出してあげることで、NSViewControllerのサブクラスをレスポンダチェーンに追加する事ができます。




