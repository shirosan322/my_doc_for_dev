==================================
Objective-Cのコードを書きましょう
==================================

もしもこれまでに、OS X か iOSのプログラミングを行ったことがなければ、初歩的なプログラミング言語であるObjective-Cに慣れておく必要があります。
Objective-Cは難しい言語ではありませんし、一度しばらく勉強すれば、すばらしい言語であることにお気づきになるでしょう。
Objective-C言語は、洗練されたオブジェクト指向プログラミングを可能にします。
Objective-Cはクラスやメソッドを定義する構文を提供することで、ANSI Cプログラミング言語を拡張しています。また、クラスやインターフェースを拡張することを促進します。

もし、あなたがANSI-Cに詳しければ、これから示す情報はObjective-Cの基本的な構文を理解するの手助けになるでしょう。
また、他のオブジェクト指向言語でプログラミングをしたことがあれば、「カプセル化」「継承」「多様性」といったオブジェクト指向の伝統的なコンセプトの多くがObjective-Cにも登場することが分かるかと思います。
もしも、ANCI-Cをよく知らないのであれば、この記事を読む前に少なくともC言語の概要くらいは読んでおいた方が良いかもしれません。

Objective-Cは「The Objective-C Programming Language」の中で完全に説明されています。

---------

Objective-CはC言語の拡張集合である
========================================

Objective-C言語は、オブジェクトのメソッドを呼び出すためのクラスとメソッドを定義し、動的にクラスを拡張し、特定の問題に対処するプログラミング·インタフェースを作成するためのに構文を指定します。
Cプログラミング言語のスーパーセットとして、Objective-Cは、基本的なC言語と同じ構文をサポートしています。
あなたは、プリミティブ型（int、floatなど）、構造体、関数、ポインタ、if...elseのような制御フロー構成など、使い慣れた要素のすべてを使うことが可能です。
また、「stdlib.h」や「stdio.h」で定義されているような、標準Cライブラリルーチンにもアクセスすることができます。

Objective-Cには、ANSI-Cに次のような構文と特徴が追加されています。

	- クラスの定義
	- クラスやインスタンスのメソッド
	- メソッド呼び出し（メッセージングと呼ばれている）
	- プロパティの宣言（およびそれらのアクセッサメソッドの自動合成）
	- 静的および動的型付け
	- ブロック - いつでも実行可能なコードのカプセル化されたかたまり。
	- プロと頃うやカテゴリのような基本的な言語への拡張

Objective-Cのこれらの側面がよく分からなくても、今は心配しないでください。
残りの記事を進めるにつれて、これらのことが分かってくるはずです。
もしも、あなたがオブジェクト指向の概念についてあまり詳しくなければ、最初のうちはオブジェクトを関連した関数を持った構造体だと考えることは、理解を深める上で最初のうちは良いかもしれません。この考え方は、特にランタイムの実装の観点から、あたらずとも遠からずというところです。

他のオブジェクト指向言語に見られる抽象化および機構の大部分を提供することに加えて、Objective-Cは、非常に動的な言語であり、その動的さは最大の利点です。
アプリケーションをビルドしたときではなく、実行中（つまりランタイム上にあるとき）に、その振る舞いを決定することを可能にしているという点で、動的であると言えます。
このように、Objective-Cの動的性は、コンパイルされ、リンクされたときに課される制約からプログラムを解放します。その代わりに、実行時、すなわちユーザーがコントロールできる状態にあるときに、シンボル解決のための責任の多くをシフトします。

-----------

クラスとオブジェクト
======================

他のほとんどのオブジェクト指向言語と同様に、Objective-C内のクラスは、データのカプセル化や、データを操作するアクションを定義するのをサポートしている。
オブジェクトは、クラスの実行時インスタンスです。
オブジェクトには、クラスで宣言されて変数のインスタンスやクラスのメソッドへのポインタのインメモリコピーが含まれています。
「アロケーション」と「初期化」と呼ばれる２ステップの手順でオブジェクトを作成します。

Objective-Cのクラスの特徴として、「interface」と「implementation」をいう２つの個別の部分を必要としています。
「interface」部は、クラスの宣言やクラスの公開インターフェースの定義が含まれています。
Cのコードど同じように、ソースコードの実装詳細からパブリック宣言を分離するために、ヘッダファイルとソースファイルを定義します。（もしも、プログラムのインターフェースの一部であるのであれば、実装ファイルにその他の宣言をすることもできますが、これはprivateであることを意味しています。）
これらのファイルは以下のテーブルに示すようなファイル拡張子を持っている。

.. list-table::
	:widths: 20, 80
	:header-rows: 1

	* - 拡張子
	  - ソース種別
	* - .h
	  - ヘッダファイル。クラス、型、関数等の宣言が含まれている。
	* - .m
	  - 実装ファイル。この拡張子のソースファイルはObjectice-CとCのコードの両方を含みます。これは単にソースファイルと呼ばれることもあります。
	* - .mm
	  - 実装ファイル。Objective-Cに加えて、C++のコードが含まれている場合です。Objective-CからC++のクラスか機能を参照しているときのみ、この拡張子を使用してください。


ソースコード中でヘッダファイルをインクルードする必要があるときは、ヘッダファイルかソースファイルの先頭業の一部として、インポート(#import)ディレクティブを指定します。
#importディレクティブはCの#includeディレクティブに似ていますが、同じファイルは必ず１度しか読み込まない点が異なります。
もしもフレーワークのヘッダファイルの一部か全体ををインポートしたければ、個別のヘッダファイルではなく、包括的なヘッダファイルをインポートしてください。
（架空の）Gizmoフレームワークのヘッダファイルをインポートするための構文は以下の通りです。

.. code-block:: objective-c

	#import <Gizmo/Gizmo.h>


以下の図は、NSObjectクラスを継承したMyClassという名前のクラスの宣言の構文です。
（親クラスは、他のあらゆるクラスが直接または間接的に継承しているものの１つです）
クラスの宣言は、「@interface」コンパイラディレクティブで始まり、「@end」ディレクティブで終わります。
後ろに続いているクラス名（転んで区切られている）が親クラスの名前です。Objective-Cでは親クラスを１つだけ持つことができます。

	.. image:: images/class_decl_2x.png
		:scale: 50


「@interface」と「@end」ディレクティブの間にプロパティとメソッドの宣言を記述します。
これらの宣言は、クラスのパブリックインターフェースを形成します。
（プロパティについては「:ref:`Declared_Properties_and_Accessor_Methods`」で説明します。）
セミコロンは各プロパティとメソッドの宣言の終わりを示します。
クラスが、パブリックインターフェースに関連づけられたカスタム関数、またはデータ型を持っている場合は、@interface...@endブロックの外側に宣言を記述します。

クラスの実装のための構文も似ています。
「@implementation」コンパイラディレクティブ（クラス名が後に続きます）で始まり、「@end」ディレクティブで終わります。
メソッドの実装は、これらのディレクティブの間に記述します。（関数の実装は@implementation...@endブロックの外側に実装する必要があります。）
実装ファイルでは、コードの最初の行の一つとして、対となるインターフェイスファイルを常にインポートする必要があります。

.. code-block:: objective-c

	#import "MyClass.h"
	@implementation MyClass

	- (id)initWithString:(NSString *)aName
	{
	    // code goes here
	}

	+ (MyClass *)myClassWithString:(NSString *)aName
	{
	    // code goes here
	}
	@end

Objective-Cは、オブジェクトを含む変数の動的な型付けをサポートしていますが、静的型付けもサポートしています。
静的に型付けされた変数は、変数の型宣言内のクラス名が含まれています。
動的に片付けされた変数は、オブジェクトの代わりに「id」を使用します。
特定の状況において、動的に型付けされた変数が使用されているのに気づくでしょう。

たとえば、（含まれるオブジェクトの正確な種類は不明でもよい）配列のようなコレクションオブジェクトには、動的型付けされた変数を使用するかもしれません。
このような変数は、すばらしい柔軟性を提供し、Objective-Cプログラムの動的性をより大きくしています。

この例では、静的および動的型付けされた変数宣言の例を示します。

.. code-block:: objective-c

	MyClass *myObject1;  // Static typing
	id       myObject2;  // Dynamic typing


宣言のアスタリスク（*）に注目してください。Objective-Cでは、オブジェクト参照は常にポインタである必要があります。
もしもこの要件が何を意味しているか分からなくても心配しないでください。Objective-Cのプログラミングを始られるようになるのに、ポインタのエキスパートになる必要はありません。
ここでは、静的型付けのオブジェクトの宣言には、変数名の前に*を置くことだけ覚えておいてください。「id」型はポインタを示します。

-----------------


メソッドとメッセージング
===========================

もしも、あなたがオブジェクト指向プログラミングが初めての経験であれば、メソッドを特定のオブジェクトにスコープされている関数と考えることは、役立つかもしれません。
オブジェクトにメッセージを送ることで、オブジェクトのメソッドを呼び出します。
Objective-Cには、「インスタンスメソッド」と「クラスメソッド」の２種類があります。

	- 「インスタンスメソッド」は、その実行がクラスの特定のインスタンスにスコープされるメソッドです。言い換えると、インスタンスメソッドを読み出す前に、必ずクラスのインスタンスを生成する必要があります。インスタンスメソッドはメソッドの中で最も一般的なタイプのものです。

	- 「クラスメソッド」は、その実行がメソッドのクラスにスコープされているメソッドです。これは、メッセージを受信するためのオブジェクトのインスタンスは必要ありません。

メソッドの宣言は、メソッドタイプ識別子、戻り値の型、シグネチャーキーワード、パラメータの型と名前の情報で構成されています。
これは、「insertObject:atIndex:」インスタンスメソッドの宣言です。

	.. image:: images/method_decl_2x.png
		:scale: 50

インスタンスメソッドの宣言はマイナス記号（-）の後に続けて行い、クラスメソッドの対応する記号はプラス記号（+）です。
クラスメソッドについては、後ほど「:ref:`ClassMethod`」で解説します。

メソッドの実際の名前（insertObject:atIndex:）は、コロン（:）を含む、すべてのシグネチャーキーワードを連結したものです。
コロンはパラメータの存在を宣言しています。上の例では、メソッドは２つのパラメータがあることを示しています。
もしも、メソッドにパラメータがなければ、最初の（そして唯一の）シグネチャーキーワードのあとのコロンを省略します。

メソッドを呼び出したいときは、メソッドを実装しているオブジェクトにメッセージを送ることでこれを行います−−−オブジェクトのメッセージングともいう。
（一般的に「メッセージの送信」は「メソッドの呼び出し」と同義語として使われていますが、Objective-Cのランタイムは実際に送信を行っています。）
メッセージは、メソッド名とメソッドが必要としているパラメータ情報です。
オブジェクトに送るすべてのメッセージは、動的に送信されます。このようにしてObjective-Cクラスの多態性が容易になっています。
（多態性とは、同じメッセージに応答するオブジェクトの型の違いの能力について言っている。）
呼び出されたメソッドはメッセージを受信するオブジェクトのクラスの親クラスで実装されているときもあります。

メッセージを送信するために、ランタイムはMessage Expressionが必要です。
「Message Expression」は、メッセージ自身（必要なパラメータも含む）を括弧（[]）で囲ます。メッセージを受信するオブジェクトは一番左の括弧のすぐ内側にあります。
たとえば、myArray変数で保持されたオブジェクトに「insertObject:atIndex:」メッセージをオブジェクトに送るには、次のような構文を使います。

	.. code-block:: objective-c

		[myArray insertObject:anObject atIndex:0];

一時的な結果を格納するためのローカル変数をたくさん宣言することを避けるために、Objective-Cはメッセージ式をネストさせます。
ネストされた各メッセージ式から返された値は、パラメータとして使われたり、別のメッセージの受信オブジェクトとして使用されます。
例えば、前の例で使用されているいずれかの変数を値を取得するメッセージで置き換えることもできます。
もし、配列オブジェクトにアクセスしたり、配列にオブジェクトを追加するようなメソッドを持った「myAppObject」という名前の別のオブジェクトを持っていたとします。そうすると、先程の例は次のように書くこともできます。

	.. code-block:: objective-c

		[[myAppObject theArray] insertObject:[myAppObject objectToInsert] atIndex:0];

Objective-Cは、アクセッサメソッドを呼び出すのにドット構文も提供しています。
「アクセッサメソッド」はオブジェクトの状態を設定したり取得したりしますが、これはカプセルかの鍵となるもので、すべてのオブジェクトにおいて重要な特徴です。
オブジェクトは状態を隠したりカプセル化したりし、これらの状態にアクセスするためのインターフェースをすべてのインスタンスに共通して提供します。
ドット表記構文を使用することで、先程の例を次のように書くこともできます。

	.. code-block:: objective-c

		[myAppObject.theArray insertObject:myAppObject.objectToInsert atIndex:0];

割当にもドット表記構文を使用することができます。

	.. code-block:: objective-c

		myAppObject.theArray = aNewArray;

これは単純に「[myAppObject setTheArray:aNewArray];」を別の方法で書いたものです。
ドット表記で書かれた動的型付けされたオブジェクトへの参照は使用できません。

「Your First Mac App」で、変数に代入するのにドット表記を使用していました。


.. _ClassMethod:

クラスメソッド
-----------------

上記の例では、クラスインスタンスにメッセージを送りましたが、クラス自身にメッセージを送ることも可能です（クラスはランタイムによって生成されたClass型のオブジェクトです）。
クラスにメッセージを送るとき、指定したメソッドはインスタンスメソッドではなく、クラスメソッドとして定義されていなければなりません。
クラスメソッドはC++の静的クラスメソッドに似た機能です。

多くの場合、クラスの新しいインスタンスを生成するためのFactoryメソッドか、クラスに関連づけられたいくつかの情報にアクセスするために使用します。
クラスメソッドの宣言の構文は、〜〜メソッドタイプ識別子にマイナス記号の代わりにプラス記号（+）を使用すること以外は同じです

次の例では、クラスのファクトリメソッドとしてクラスメソッドを使用する方法を示しています。
この場合、「array」メソッドは、「NSMutableArray」によって継承されている「NSArray」クラスの、クラスの新しいインスタンスの割当と初期化をして返すクラスメソッドです。

	.. code-block:: objective-c

		NSMutableArray *myArray = nil;  // nil is essentially the same as NULL

		// Create a new array and assign it to the myArray variable.
		myArray = [NSMutableArray array];

-------

.. _Declared_Properties_and_Accessor_Methods:

プロパティの宣言とアクセッサメソッド
======================================

一般的な意味で、プロパティはオブジェクトによってカプセル化された、または保存されたデータです。
これは、名前や色いったような属性の１つか、複数の他のオブジェクトとの関係のいずれかである。 
オブジェクトのクラスはそのオブジェクトを使用するユーザーがカプセル化されたプロパティの値を設定したり取得したりすることができるインターフェースを定義しています。
これらの操作を実行するメソッドを「アクセッサメソッド」と呼びます。

２種類のアクセッサメソッドがあり、これらは命名規則に準拠する必要があります。
プロパティの値を取得する「getter」アクセッサメソッドは、同じ名前のプロパティを持っています。
プロパティに新しい値を設定する「setter」メソッドは、プロパティ名の最初の文字が大文字にした「setPropertyName」といった形式になっています。
適切に命名されたアクセッサメソッドは、プロパティの名前を通して直接オブジェクトのプロパティにアクセスするメカニズムである、key-valueコーディング（KVC）を含む、「Cocoa」や「Cocoa Touch Framework」の技術的に重要な要素の一つです。

Objective-Cは、アクセッサメソッドの宣言と実装の表記を便利にするものとしてプロパティ宣言を提供しています。「Your First Mac App」ではvolumeのプロパティを宣言しました。

	.. code-block:: objective-c

		@property (assign) float volume;

プロパティを宣言することで、クラス内にあるそれぞれのプロパティの「getter」「setter」メソッドを実装しなくてもよくなります。
その代わり、プロパティ宣言を使用したい動作を指定します。
コンパイラは、その宣言に基づいて実際の「getter」「setter」メソッドを生成、または統合することができます。
プロパティ宣言は書かなければならない多くの定型的なコードを減らしてくれ、結果として、あなたのコードがよりクリーンでエラーの発生を減らすことができます。

クラスのインターフェースには、メソッドの宣言とともにプロパティの宣言も含まれています。
パブリックプロパティはクラスのヘッダファイルに宣言し、クラス拡張のプライベートプロパティはソースファイルに宣言します。
（クラスの拡張については「:ref:`Protocols_and_Categories`」でサンプルとともに簡単に説明するので、そちらを参照してください。）
DelegateやViewControllerのようなコントローラオブジェクトのプロパティは通常privateであるはずです。

基本的なプロパティの宣言では、「@property」コンパイラディレクティブを使用し、プロパティの型情報と名前が続きます。
プロパティに、アクセッサがどのようの動作するかを定義するカスタムオプションを設定することもできます。たとえば、プロパティが弱参照かどうか、read-onlyかどうか等。
オプションは「@property」ディレクティブに続く括弧の中に記述します。

以下のコードは、いくつかのプロパティ宣言を示しています。

	.. code-block:: objective-c

		@property (copy) MyModelObject *theObject;  // Copy the object during assignment.
		@property (readonly) NSView *rootView;      // Declare only a getter method.
		@property (weak) id delegate;               // Declare delegate as a weak reference

コンパイラは宣言されたプロパティを自動的に統合します。プロパティを合成する中で、コンパイラはアクセッサメソッドだけでなく、プロパティを「返す」privateインスタンス変数も作成します。
このインスタンス変数は、プロパティと同じ名前を持っていますが、接頭辞としてアンダースコア（_）があります。
あなたのアプリケーションは、初期化と解放のときだけ、（プロパティの代わりに）インスタンス変数に直接アクセスすることができます。

もしも、インスタンス変数に別の名前をつけたい場合は、自動合成をバイパスして明示的にプロパティを合成することができます。
指定した名前のインスタンス変数と一緒にアクセッサメソッドを生成するようにコンパイラに依頼するために、「@synthesize」コンパイラディレクティブを使用してください。
例えば次のような感じです。

	.. code-block:: objective-c

		@synthesize enabled = _isEnabled;

ちなみに、プロパティを宣言するときにアクセッサメソッドにカスタム名を付けることもでき、通常、Boolean型のプロパティのgetterを作るには次のように書きます。

	.. code-block:: objective-c

		@property (assign, getter=isEnabled) BOOL enabled; // Assign new value, change name of getter method

---------

ブロック
==============

ブロックは色々なときに実行されうる処理の単位（コードのセグメント）をカプセルかしたオブジェクトです。
ブロックは本質的には、移植可能で匿名な関数で、メソッドや関数のパラメータとして渡したり、メソッドや関数から返すこともできます。
ブロック自体は、入力されたパラメータリスト持っており、宣言か推測された戻り値の型もあるかもしれません。
また、変数へのブロックを割り当てることができ、関数を呼び出すのと同じように呼び出すこともできます。

ブロックであることを示す高分譲のマーカとして、キャレット（^）が使用されます。
他にも、パラメータ、戻り値、ブロックの本体（実行されたコード）にも構文上の似たような規則があります。
以下の図で、ブロックを変数に割り当てるときの構文について詳しく説明します。

	.. image:: images/blocks.png

そして、ブロックはまるで関数であるかのように呼び出すことができます。

	.. code-block:: objective-c

		int result = myBlock(4); // result is 28

ブロックはローカルの辞書的なスコープを共有します。
このブロックの特性は便利です。というのも、もしもメソッドを実装し、そのメソッドwがブロックを定義している場合、ブロックはローカル変数とメソッドのパラメータ（スタック変数を含む）だけでなく、インスタンス変数を含む関数やグルーバル変数にもアクセスできます。
このアクセスは読み取り専用ですが、「__block」修飾子を使用して変数を宣言した場合は、ブロック内で変更することも可能です。
ブロックで囲まれたメソッドや関数が戻ってきた後でさえも、そして、ローカルスコープが破棄された後でさえも、ローカル変数はブロックへの参照がある限りブロックの一部として残ります。

メソッドや関数のパラメータと同じように、ブロックはコールバックとして機能することができます。
呼び出されると、メソッドまたは関数がいくつかの処理を実行し、追加の情報を要求したり、プログラム固有の動作を取得するために、適切な時に、ブロックを経由してコールバックすることができます。
ブロックは、関数呼び出しの時点で、呼び出し元にコールバックを提供することができます。
「contest」構造体に必要なデータをパッケージングする代わりに、ブロックは呼び出し元のメソッドや関数として、静的スコープからデータを取得することができます。

ブロックコードは別々のメソッドや関数として実装する必要がないので、実装したコードがシンプルで理解しやすくなるでしょう。

Objective-Cのフレームワークには、ブロックパラメータを持つメソッドが多くあります。
たとえば、「Foundation」フレームワークの「NSNotificationCenter」クラスはブロックパラメータを持った以下のメソッドを宣言しています。

	.. code-block:: objective-c

		- (id)addObserverForName:(NSString *)name object:(id)obj queue:(NSOperationQueue *)queue usingBlock:(void (^)(NSNotification *note))block

このメソッドは通知センター（Notification Center）にオブザーバーを追加しています。
（通知（Notification）については、「Streamline You App with Design」で議論しています。）
指定した名前の通知がポストされると、ブロックが呼び出され通知をハンドルします。

	.. code-block:: objective-c

		opQ = [[NSOperationQueue alloc] init];
		[[NSNotificationCenter defaultCenter] addObserverForName:@"CustomOperationCompleted"
					object:nil queue:opQ
				usingBlock:^(NSNotification *notif) {
		// handle the notification
		}];

--------------

.. _Protocols_and_Categories:

プロトコルとカテゴリ
======================

「Protocol」はあらゆるクラスで実装することができるメソッドを宣言します。
それは、たとえプロトコルを実装したクラスが共通の親クラスを持っていないときでさ実装できてしまいます。
プロトコルメソッドは、あらゆる特定のクラスから独立して動作を定義します。
プロトコルは、単に他のクラスが実装する責任があるインターフェースを定義します。
プロトコルメソッドを実装しているときは、そのクラスはプロトコルに「準拠している」と言われる。

実用的な観点から、プロトコルはメソッドのリストを定義しますが。
これは、特定のクラスのインスタンスであることが、必要でないオブジェクトの間で成り立ちます。
この契約は、これらのオブジェクト間の通信を可能にします。
あるオブジェクトは、自分が遭遇したものであることや、イベントについてついて何か質問したいということを、他のオブジェクトに伝えたい。

「UIApplication」クラスはアプリケーションの必要としている動作を実装します。
アプリケーションの現在の状態について通知を受けるために、「UIApplication」をサブクラス化することを強制する代わりに、「UIApplication」クラスは
アサインされているデリゲートオブジェクトの特定のメソッドを呼び出すことで、これらの通知を配信します。
「UIApplicationDelegate」プロトコルのメソッドを実装しているオブジェクトは、これらの通知を受け取り、適切な応答を提供することができます。

継承しているクラスの名前の後に山括弧（<...>）を書き、その中にプロトコルの名前を入れておくことで、プロトコルに準拠または採用しているクラスであることを指定します。

「Your First Mac App」で、「NSApplicationDelegate」プロトコルの採用は以下のように指定されていました。(AppDelegate.h)

	.. code-block:: objective-c

		@interface TrackMixAppDelegate : NSObject <NSApplicationDelegate>

実装するプロトコルメソッドを宣言する必要はありません。

親クラスを持っていないこととインスタンス変数を定義していない（プロパティは宣言できます。）ことを除けば、プロトコルの宣言はクラスのインターフェースの宣言と似ています。
以下の例では1つのメソッドを含むプロトコルの宣言を記載しています。

	.. code-block:: objective-c

		@protocol MyProtocol
		- (void)myProtocolMethod;
		@end

多くのデリゲートプロトコルにとって、プロトコルを採用するということは、プロトコルによって定義されたメソッドを実装するという簡単なことです。
プロトコルには、プロトコルをサポートしていることを明示的に要求するものや、必須メソッドとオプションメソッドの両方を指定するこができるものもあります。

Objective-Cフレームワークのヘッダファイルを探すときは、次の例に似たような行が見つかるでしょう。

	.. code-block:: objective-c

		@interface NSDate (NSDateCreation)

この行はカテゴリの宣言で、カテゴリの名前を括弧で囲むことが構文規則となっています。
カテゴリは、サブクラス化をすること無くクラスのインターフェースを拡張できるようにする、Objective-C言語の特徴の１つです。
カテゴリ内のメソッドは（あなたのプログラムの範囲内で）クラス型の一部となり、すべてのクラスのサブクラスに継承されています。
カテゴリで定義されたメソッドを呼び出すことで、クラス（またはそのサブクラス）のあらゆるインスタンスにメッセージを送ることができます。

ヘッダファイル内で関連したメソッドのグループ化の手段としてカテゴリを使用することができます。
異なるヘッダファイルに異なるカテゴリを置くことさえできます。
フレームワークはそのヘッダファイルにおいて、明確にするためにこのテクニックを使用しています。

また、実装ファイル（.m）にプライベートプロパティとプライベートメソッドを宣言するためのクラス拡張と知られている匿名のカテゴリを使用することもできます。
クラス拡張は括弧内のテキストが無い以外はカテゴリと似ています。
例えば、以下の例は典型的あなクラス拡張の例です。

	.. code-block:: objective-c

		@interface TrackMixAppDelegate ()
		@property (weak) IBOutlet NSWindow *window;
		@property (assign) IBOutlet NSTextField *nameField;
		@property (strong) MyDataObject *data;
		@end

---------


型の定義とストラテジのコーディング
=====================================

Objective-Cは、特別な目的で予約されているため変数のなめとして使用すべきでない用語がいくつかあります。
これらの用語のうち、アットマーク（@）の接頭語が着いている用語はコンパイラディレクティブです。（たとえば、@interfaceや@end）
他の予約語には型や、型を伴うリテラルが定義されています。
Objective-Cは、ANSI-Cでは気づかなかった方やリテラルがたくさん定義されているます。
場合によっては、これらの型やリテラルはANSI-Cのそれと対応を変換してください。
次の表は、各型で許容されているリテラルを含む、いくつかの重要な事柄が示されています。

.. list-table:: 
	:widths: 20, 80
	:header-rows: 1

	* - 型
	  - 説明とリテラル
	* - id
	  - 動的なオブジェクト型。動的にも静的にもなオブジェクトのである反対のリテラルはnil。
	* - Class
	  - 動的なクラス型。負のリテラルはnilです。
	* - SEL
	  - セレクタのデータ型。このデータ型は、実行時にメソッドシグネチャを表します。反対のリテレラルはNULLです。
	* - BOOL
	  - ブール型。この型のリテラル値はYESとNOです。


多くの場合、これらの型やリテラルの定義はエラーチェックや制御フローコードで使用されます。
プログラムの制御フロー分では、どのような処理を行うかを決定するために、適切なリテラルをテストするこができます。

たとえば

	.. code-block:: objective-c

		NSDate *dateOfHire = [employee dateOfHire];
		if (dateOfHire != nil) {
			// handle this case
		}

このコードを書き換えるために、オブジェクトが雇用日を表すオブジェクトがnilでない（言い換えると、有効なオブジェクトである）場合は、ロギックは特定の方向へ進みます。
ここでは、同じ分岐を行うための簡単な書き方は次の通りです。

	.. code-block:: objective-c

		NSDate *dateOfHire = [employee dateOfHire];
		if (dateOfHire) {
			// handle this case
		}

（dateOfHireオブジェクトを参照する必要がないと仮定すると）これらのコードをさらに減らすことも可能です。

	.. code-block:: objective-c

		if ([employee dateOfHire]) {
			// handle this case
		}

同じようにしてBoolean値も処理します。
例えば次の例では、「isEqual:」メソッドはBoolea値を返します。

	.. code-block:: objective-c

		BOOL equal = [objectA isEqual:objectB];
		if (equal == YES) {
			// handle this case
		}

nilの有無をテストするコードと同じようにしてこのコードも短くすることができます。

Objective-Cでは、悪影響を与えること無く、nilにメッセージを送ることができます。
メソッドがオブジェクトを返すことになっている場合にランタイムがnilを返す場合を除いて、全く影響ありません。
nilに送ったメッセージからの戻り値は、返されたものの型がオブジェクトである限りは問題なく動作することが保証されています。

Objetive-Cの予約語に「self」と「super」という重要な２つがあります。
1つ目の「self」はメッセージの実装内で、現在のオブジェクトを参照するのに使用することができるローカル変数です。
これは、C++でいう「this」に相当します。

メッセージ式のレシーバーのときだけ、予約語を「slef」を「super」で置き換えることが可能です。
もしも自分自身にメッセージを送るなら、ランタイムは現在のオブジェクトのクラスのメソッドの実装を探します。
そこでメソッドを見つけられなかったら、スーパクラス（等々）のメソッドの実装を探しに行きます。
「super」にメッセージを送るのであれば、ランタイムは最初に、スーパークラスのメソッドの実装を探します。

「self」「super」両方の主な使用方法として、メッセージの送信を行う必要があります。
呼び出すメソッドが「self」のクラスで実装されてるときは「self」にメッセージを送信します。
例えば、

	.. code-block:: objective-c

		[self doSomeWork];

「self」は、宣言したプロパティと合成されたアクセッサを呼び出すために、ドット表記で使用することもできる。

	.. code-block:: objective-c

		NSString *theName = self.name;

多くの場合、スーパクラスから継承されたメソッドのオーバーライド（再実装）で、スーパクラスにメッセージを送ります。
この場合、呼び出されたメソッドはオーバーライドされたメソッドと同じシグネチャを持っています。
