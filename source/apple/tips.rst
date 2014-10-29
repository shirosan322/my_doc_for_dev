========
TIPS
========

目次
=======

- :ref:`ディレクトリから指定した拡張子のファイルのみを抽出したい<get_specified_ext_files>`
- :ref:`指定したパスがディレクトリかどうかチェックしたい<check_is_directory>`
- :ref:`子Viewが親Viewのドラッグ&ドロップを横取りしてしまうのを回避したい<ignore_subview_dragevent>`


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






