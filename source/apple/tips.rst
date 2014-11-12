========
TIPS
========

目次
=======

共通
----------
- :ref:`ディレクトリから指定した拡張子のファイルのみを抽出したい<get_specified_ext_files>`
- :ref:`指定したパスがディレクトリかどうかチェックしたい<check_is_directory>`
- :ref:`アプリケーションの設定を保存したい<save_app_settings>`
- :ref:`ユーザーデフォルトの値を削除したい<delete_userdefaults>`
- :ref:`文字列の先頭・末尾を確認したい<check_prefix_suffix>`
- :ref:`並列処理を行いたい<parallel_process>`

Cocoa
----------
- :ref:`ドラッグ＆ドロップで、特定のファイルのみドロップ可能にしたい<filer_dropfile>`
- :ref:`子Viewが親Viewのドラッグ＆ドロップを横取りしてしまうのを回避したい<ignore_subview_dragevent>`
- :ref:`ウィンドウを閉じるときにアプリケーションを一緒に終了したい<finish_app_with_close_close>`

iOS
-----


-----

共通
========
.. _get_specified_ext_files:

ディレクトリから指定した拡張子のファイルのみを抽出する
---------------------------------------------------------

例)オーディファイルを抽出する

.. code-block:: objective-c
	:linenos:

	NSArray *extensions = [NSArray arrayWithObjects:@"wav", @"mp3", @"aif", @"flac", @"ogg", nil];
	NSArray *dirContents = [[NSFileManager defaultManager] contentsOfDirectoryAtPath:documentsDirectoryPath error:nil];
	NSArray *files = [dirContents filteredArrayUsingPredicate:[NSPredicate predicateWithFormat:@"pathExtension IN %@", extensions]];

------

.. _check_is_directory:

指定したパスがディレクトリかどうかチェックする
------------------------------------------------

指定したパスにファイルが存在するかチェックする以下の２つのメソッドのうち後者を利用し、
引数の「isDirectory」を確認することで、指定したパスがディレクトリであるかを確認できます。

.. code-block:: objective-c

	-(BOOL)fileExistsAtPath:(NSString *)path;
	-(BOOL)fileExistsAtPath:(NSString *)path isDirectory:(BOOL *)isDirectory;


- 引数
 - path        : チェックするパス
 - isDirectory : チェックしたパスがディレクトリかどうかが設定される。

- 戻り値
	- YES : 存在する、NO : 存在しない

例）指定したパスがディレクトリかをチェックする関数を作成

.. code-block:: objective-c
	:linenos:

	- BOOL isDirectory:(NSString*)path {
	    BOOL isDirectory = NO;
	    [[NSFileManager defaultManager] fileExistsAtPath:path isDirectory:&isDirectory];
	    if (!isDirectory) {
	    	return NO;
	    }
	    return YES;
	}

------

.. _save_app_settings:

アプリケーションの設定を保存する
-----------------------------------
アプリケーション実行中に設定した項目を保存しておき、次回の起動時にその設定を反映させたい場合があります。
Cocoa / iOS では、これらの機能を実現する機能が予め提供されており、**ユーザーでフォルト** と呼ばれています。

この、ユーザーデフォルトにアクセスするためのインタフェースを提供するのが、**NSUserDefaults** です。
これを利用する事で、設定の保存／読込を用意に行う事ができます。

**＜メソッド一覧＞**

- 保存

 .. code-block:: objective-c

	- (void)setInteger:(NSInteger)value forKey:(NSString *)defaultName;
	- (void)setFloat:(float)value forKey:(NSString *)defaultName;
	- (void)setDouble:(double)value forKey:(NSString *)defaultName;
	- (void)setBool:(BOOL)value forKey:(NSString *)defaultName;
	- (void)setURL:(NSURL *)url forKey:(NSString *)defaultName NS_AVAILABLE(10_6, 4_0);
	- (void)setObject:(id)value forKey:(NSString *)defaultName;

- 読込

 .. code-block:: objective-c

	- (NSInteger)integerForKey:(NSString *)defaultName;
	- (float)floatForKey:(NSString *)defaultName;
	- (double)doubleForKey:(NSString *)defaultName;
	- (BOOL)boolForKey:(NSString *)defaultName;
	- (NSURL *)URLForKey:(NSString *)defaultName NS_AVAILABLE(10_6, 4_0);
	- (id)objectForKey:(NSString *)defaultName;

**＜使用例>**

- 設定の保存

 .. code-block:: objective-c
	:linenos:

	- (void)saveAppSettings {
	    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
	     
	    [defaults setObject:hoge forKey:@"hogeKey"];
	    [defaults setObject:moge forKey:@"mogeKey"];
	    [defaults setInteger:value forKey:@"value"];
	    [defaults setObject:imageData forKey:@"image"];
	     
	    [defaults synchronize]; // 設定内容をファイルに反映.
	}


- 設定の読込

 .. code-block:: objective-c
	:linenos:

	- (void)loadAppSettings {
	    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
	     
	    NSString* hoge = [defaults objectForKey:@"hogeKey"];
	    MyClass* moge = [defaults objectForKey:@"mogeKey"];
	    NSInteger value = [defaults integerForKey:@"value"];
	    NSData* imageData = [defaults objectForKey:@"image"];
	}

-------

.. _delete_userdefaults:

ユーザーデフォルトの値を削除したい
-------------------------------------

開発中の場合、動作を確認するためにユーザーデフォルトの値を使用したくない場合があります。
そういった場合は、メニューやボタンを一時的に用意しユーザーデフォルトを削除するようにしたい場合があります。
そんなときは、以下のように記述しましょう。

.. code-block:: objective-c

	NSString* domainName = [[NSBundle mainBundle] bundleIdentifier];
	[[NSUserDefaults standardUserDefaults] removePersistentDomainForName:domainName];

------

.. _check_prefix_suffix:

文字列の先頭・末尾を確認する
================================

- 先頭を確認する（〜ではじまる）

　自分で作成したアプリケーション独自のファイルを書き出す場合に、ファイル名の先頭に特定の文字を設定する場合等があります。文字列に指定した接頭辞ががあるかどうかをチェックする場合は以下のようにします
。

.. code-block:: objective-c

	BOOL flag = [hogeStr hasPrefix:@"myapp_"];	// myapp_で始まる.


- 末尾を確認する（〜でおわる）

　ファイルのパスを自分で生成するとき等、文字列の末尾に"/"が含まれているかどうかを確認した場合等があります。その場合は、以下のようにします。

.. code-block:: objective-c

	BOOL flg = [hogeStr hasSuffix:@"/"];	// "/"で終わる.

--------

.. _parallel_process:

並列処理を行う
=====================





Cocoa
========
.. _filer_dropfile:

ドラッグ＆ドロップで、特定のファイルのみドロップ可能にする
----------------------------------------------------------------

NSDraggingDestinationプロトコルのoptionalメソッドである以下のメソッドを実装し、ここでドラッグしているファイルのパスを取得して、拡張子やディレクトリをチェックします。

 .. code-block:: objecitve-c

	- (NSDragOperation)draggingEntered:(id <NSDraggingInfo>)sender;

チェックした結果、ドラッグ＆ドロップ対象とするファイルでなかった場合は、**「NSDragOperationNone」** を返します。

例）拡張子が.wavのファイルのみドロップ可能にする

.. code-block:: objective-c
	:linenos:

	- (NSDragOperation)draggingEntered:(id <NSDraggingInfo>)sender {
	    NSString* urlString = nil;
	    
	    NSPasteboard *pboard = [sender draggingPasteboard];
	    NSArray *objs = [pboard pasteboardItems];
	    
	    for (id item in objs) {
	        NSArray* info = [item types];
	        for(NSString *type in info) {
	            if([[item types] containsObject:type]) {
	                urlString = [item stringForType:type];
	            }
	        }
	    }
	    
	    if (urlString != nil) {
	        NSString* ext = [urlString pathExtension];
	        if ([ext caseInsensitiveCompare:@"wav"] == NSOrderedSame) {
	            highlight = YES;               // ドロップエリアをハイライトする.
	            [self setNeedsDisplay: YES];   // 描画更新.
	            return NSDragOperationGeneric; // ドロップ可能.
	        }
	    }
	    return NSDragOperationNone; // ドロップ不可.
	}


------

.. _ignore_subview_dragevent:

子Viewが親Viewのドラッグ&ドロップを横取りしてしまうのを回避する
----------------------------------------------------------------

子ViewがもとからDrag & Dropイベント受けるようなView(NSImageView等)の場合、本来であれば親Viewにドロップしたくても、子Viewの範囲だけドロップ対象外となってしまう場合があります。
そういった場合は、以下のメソッドを呼び出し、子ViewがDrag & Dropを受けつけないように設定することがでこの問題を回避できます。

.. code-block:: objective-c

	- (void)unregisterDraggedTypes;

例）Drag & Drop 対象である「HogeView」の子ViewであるImageViewの部分にDropできない問題を解決する

.. code-block:: objective-c
	:linenos:

	@implementation HogeView {
	    IBOutlet NSImageView* imageView1;
	    IBOutlet NSImageView* imageView2;
	}

	- (void)awakeFromNib {
	    [super awakeFromNib];
	    [imageView1 unregisterDraggedTypes];
	    [imageView2 unregisterDraggedTypes];
	}
	...
	@end

-------

.. _finish_app_with_close_close:

ウィンドウを閉じるときにアプリケーションを一緒に終了する
---------------------------------------------------------

Macのアプリケーションでは、ウィンドウを閉じてもアプリケーションは終了していません。これがデフォルトの状態となっています。
ですが、シングルウィンドウのアプリケーション等、ウィンドウを閉じると同時にアプリケーションが終了してくれた方が都合が良い場合もあります。
そういった場合は、以下のデリゲートメソッドを実装します。

.. code-block:: objective-c

	- (BOOL)applicationShouldTerminateAfterLastWindowClosed:(NSApplication *)theApplication
	{
	    return YES;
	}

ここで、**YES** を返す事で、ウィンドウを閉じると同時にアプリケーションを終了させる事ができます。

-----






iOS
========

