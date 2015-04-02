==========================
Track オブジェクトの追加
==========================

このアプリケーションには、アプリケーションのロジックを含む２つのカスタムクラスがあります。Xcodeのテンプレートは「AppDelegate」クラスが提供され、nibファイルのインスタンスを作成してくれます。
そして、UI部品とapp delegateとの接続を作成したときに、「AppDelegate」クラスにコードを追加しました。app delefate は「Model-View-Controller」デザインパターンでいうと、Viewを更新したり、アプリケーションで使用する実際のデータを管理する「Model」オブジェクトを管理する「Controller」として働きます。
ということは、「Model」オブジェクトがトラックのボリュームを保持するように実装しなければならないことが分かるかと思います。
「Track」クラスを作成し、app delegateに「Track」のインスタンスを作成しなければなりません。
UI部品で値を変更されたときに、app delegate がトラックのボリュームを更新し、Viewを同期させるようにしましょう。

 	.. image:: images/adding_a_track_object/TrackMixMVC.png

----------


Trackクラスのヘッダファイルと実装ファイルを作成しよう
========================================================

まず最初にやることは、Trackクラスのヘッダファイルと実装ファイルを作成することです。
Onjective-CのrootクラスであるNSObjectを継承するようにしましょう。


新しいクラスのファイルを作成しよう
------------------------------------

1. XcodeのプロジェクトナビゲータのTrackMixフォルダを選択してください。
 	次のステップで新しいファイルを追加したとき、プロジェクトナビゲータの選択した位置の下にファイルが追加されます。

2. 以下の手順でObjective-Cのクラスを作成します。
 	- 「File > New > File」を選択する
 	- テンプレートダイアログで、OS X セクションのCocoaを選択してください。
 	- 「Objective-C class」テンプレートを選択して「Next」を選択してください。

 	.. image:: images/adding_a_track_object/28_createnewclass.png

3. 表示された画面で、クラス名を「Track」とします（慣例では、クラス名は最初の１文字を大文字で始めます）。新しいくらすは「NSObject」クラスのサブクラスとしたまま、「Next」ボタンをクリックしてください。

 	.. image:: images/adding_a_track_object/29_createnewclass2.png

4. 保存ダイアログで「Group」と「Traget」はそのままで「Create」をクリックしてください。

--------

これらのファイルはプロジェクトの「TrackMix」グループに配置されます。ファイルの中身を確認すると、インターフェースと関数定義が提供されているスタブクラスがあるかと思います。ここに音量を表す特性を追加して行きます。

---------

トラッククラスを実装する
==========================

トラックの音量はObjective-Cで定義されている「Property」を利用して実装します。
「Property」は変数の変数のインスタンスを実装するのに非常に便利です。

Volume Propertyを追加しよう
------------------------------

- Trackのヘッダファイル（Track.h）で「volume」という名前のpropetyの定義を追加しましょう。このヘッダファイルは以下のようになります。

 	.. code-block:: objective-c

 		#import <Foundation/Foundation.h>

		@interface Track : NSObject
		@property (assign) float volume;
		@end

アプリケーションをビルドするときに、コンパイラがproperty定義を見つけたら、volume Propertyのprivate変数のインスタンスとアクセッサ関数を作成してくれます。
_volumeインスタンス変数の値はTrackオブジェクトが生成されたときに自動的に0にセットされます。


Trackプロパティを追加しよう
=============================

音量を格納し、他の複数のUI部品で表示するための、Trackクラスのインスタンスをしようするために、app delegateクラスにTrack propertを追加します。

しかし、Trackクラスに何も宣言しないでpropertyを定義するとコンパイラがエラーを出力します。
Trackクラスのヘッダファイル（Track.h）をインポートすることもできますが、一般的には「@class」を使用することで、「Forward Declaration（先付け宣言）」することができます。
「Forward Declaration（先付け宣言）」は「Track」がどこかで定義されていることをコンパイラに約束し、チェックに掛かる無駄な時間を省きます。(こうすることで多重インクルードを避けることもできる。)
実装ファイルでヘッダファイルをインクルードしてください。

-------

app delegateに track プロパティを追加しよう
--------------------------------------------

1. 「AppDelegate」のinterface定義の前に、「Track」クラスの先付け宣言をapp delegateのヘッダファイルに追加してください。

 	.. code-block:: objective-c

 		@class Track;

2. 最後の「@property」定義と「@end」の間に「track」プロパティを追加してください。

 	.. code-block:: objective-c

 		@property (strong) Track *track;


	このpropertyは、「weak」属性ではなく「strong」属性であることを明記し、Trackオブジェクトがapp delegateのものであることを表しています。
 	app delegateが参照している限り、Trackオブジェクトは消滅しません。
 	以前に作成したoutletのプロパティ定義は、対応するUI部品がapp delegateではなくWindowが持っているView階層の中に含まれていたので、「weak」属性を使用しました。
 	WindowとViewの階層はapp delegateと独立してなくなるばこともあります。

---------

 .. Note::

 	**Tip:** Objective-Cは大文字・小文字を区別します。「Track」はクラスを指し、「track」は「Track」クラスのpropertyを指します。Cocoaでのよくあるプログラミングのエラーとして、変数名のスペルミスがあり、大文字と小文字が違っているということがよくあります（たとえば、"tableView"の代わりに"tableview"と書いているような場合）。
 	このチュートリアルでは、変数名をより注意深くみてもらえるようにするために、あえて「Track」と「track」を使用しています。


AppDelegateクラスのインタフェースファイル（AppDelegate.h）が以下のようになっていることを確認してください。（コメントは載せていません。また、プロパティや関数の定義順は気にしなくても構いません。）

.. code-block:: objective-c

	#import <Cocoa/Cocoa.h>

	@class Track;

	@interface AppDelegate : NSObject <NSApplicationDelegate>

	@property (assign) IBOutlet NSWindow *window;
	@property (weak) IBOutlet NSTextField *textField;
	@property (weak) IBOutlet NSSlider *slider;
	@property (strong) Track *track;

	- (IBAction)mute:(id)sender;
	- (IBAction)takeFloatValueForVolumeFrom:(id)sender;

	@end

-------

Trackインスタンスの作成
==========================

「AppDelegate」クラスに「track」プロパティを追加しましたが、Trackクラスのインスタンスに値を設定する必要があります。


Trackクラスのインスタンスを作成しよう
----------------------------------------

1. app delegateの実装ファイル（AppDelegate.m）で、「@implementation」の前に以下のコードを追加して、「Track.h」をインポートしてください。

 	.. code-block:: objective-c

 		#import "Track.h"

 	しかし、Trackを参照したときコンパイルエラーが発生するでしょう。

2. 「applicationDidFinishLaunching:」メソッドに以下のコードを追加して「Track」のインスタンスを生成してください。

 	.. code-block:: objective-c

 		Track *aTrack = [[Track alloc] init];
		[self setTrack:aTrack];

---------

これらの２行のコードは以下のようなことを行っています。

 - Trackクラスのインスタンスのメモリを確保している
 - Trackクラスのインスタンスを使用する準備として、初期化している
 - アクセッサメソッドを使用して、trackプロパティにあtらしいtrackをセットしている
 	setTrack:を定義したりコードを書く必要はありません。「track」として定義されたプロパティのアクセッサをコンパイラが自動生成します。

Objetive-Cはドット表記にも対応しています。ですので `[self setTrack:aTrack];` を以下のように置き換えることも可能です。

	.. code-block:: objective-c

		self.track = aTrack;


ドット表記は、元々の実装のアクセッサメソッド(setTrack:)と同じように働きます。内部関数を使用するとき等は特に、アクセッサメソッドとしてコンパクトな構文となります。

.. Note::

	**Memory management:** いくつかのオブジェクトを持っていますが、これらを明示的に解放していません。
	ですが、心配ありません。ARCを使用しているのでメモリリークは発生しません。
	Automatic Reference Counting（ARC）は、コンパイル時にメモリ管理用のコードを自動的に挿入するCocoa命名規則の特徴です。Xcodeにプロジェクトを作成した時点でARCはデフォルトで有効になっています。

---------

アプリケーションのテスト
==========================

アプリケーションのテストを行います。

アプリケーションをテストしよう
---------------------------------

- プロジェクトをコンパイルして実行してください（Build > Buid and Runを選択するか、XcodeツールバーのRunボタンを押してください。）

おそらくエラーなしにコンパイルができ、以前と同じユーザーインターフェースが表示されているはずです。残念ながら、ユーザーインターフェースは以前と同じように動作するでしょう。
Trackオブジェクトを持っていますが、app delegateはTrackの生成以外には何も行っていません。
実装を完了させるには、もう少しやらないと行けないこがあります。

----------

要約
======

複数のUI部品で表示されている音量を各のするために「Track」という名前のモデルクラスを実装しました。app delegate内では、Trackオブジェクトのpropertyを定義しました。
プロパティのアクセッサメソッドが自動的に同期されました。




