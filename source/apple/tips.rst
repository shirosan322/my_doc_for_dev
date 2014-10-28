========
TIPS
========

目次
=======

- :ref:`ディレクトリから指定した拡張子のファイルのみを抽出したい<get_specified_ext_files>`


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


