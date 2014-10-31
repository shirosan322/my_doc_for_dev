========
TIPS
========

目次
=======

- :ref:`ディレクトリから指定した拡張子のファイルのみを抽出したい<get_specified_ext_files>`
- :ref:`指定したパスがディレクトリかどうかチェックしたい<check_is_directory>`
- :ref:`ドラッグ＆ドロップで、特定のファイルのみドロップ可能にしたい<filer_dropfile>`
- :ref:`子Viewが親Viewのドラッグ＆ドロップを横取りしてしまうのを回避したい<ignore_subview_dragevent>`


-----

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






