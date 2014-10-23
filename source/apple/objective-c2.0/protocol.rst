=======================
プロトコル(Protocol)
=======================

プロトコル（Protocol）とは
============================

オブジェクトの役割や振る舞いを表すメソッドの集合のことをプロトコル（protocol）と呼びます。
「実現方法は全然違うけど、やりたいことは同じ」みたいなときに「やりたいこと」をメソッドとしてまとめて宣言しておいたものというイメージ。

.. Note::

	Javaにおけるインターフェースとう概念は、Objective-Cのプロトコルを取り入れたものです。

抽象クラスに似ていますが、プロトコルは **「メソッドもインスタンス変数も、何も実装しない宣言だけの抽象クラス」** と考えることができます。

プロトコルの宣言
=====================

.. code-block:: objective-c

	@protocol HogeProtocol // プロトコル名.
	// メソッドの宣言を書く.
	- (void)hoge;
	...
	@end

例） NSLockingプロトコルの定義.

.. code-block:: objective-c

	@protocol NSLocking
	- (void)lock;
	- (void)unlock;
	@end

プロトコルは通常ヘッダファイルとして記述しておき、それを必要とするクラス宣言の直前でインポートします。

プロトコルの採用
======================

あるプロトコルのメソッドを実装するクラスの宣言を行う場合、インターフェース部は次のように記述します。

.. code-block:: objective-c

	@interface クラス名 : スーパークラス名 <プロトコル名> {
	    インスタンス変数の宣言;
	      ...
	}
	メソッドの宣言;
	  ...
	@end

このように記述することで、プロトコルに含まれるメソッドはクラスの宣言の一部として記述されたのと同じことになるので、インターフェース部に改めてメソッドの宣言を記述する必要はありません。
そして、インターフェース部に宣言されたメソッド同様に実装部に、プロトコルに含まれるメソッドを実装する必要があります。

例）NSLockingプロトコルを採用している、NSLockクラス.

.. code-block:: objective-c

	@interface NSLock : NSObject <NSLocking> {
	@private
	    void *_priv;
	}
	- (BOOL)tryLock;
	- (BOOL)lockBeforeDate:(NSDate*)limit;
	@end


また、１つのクラスが複数のプロトコルを採用する場合もあります。この場合は、<>内に、カンマを区切って複数のプロトコルを記述します。

例）クラスAがプロトコルSとプロトコルTを採用する場合.

.. code-block:: objective-c

	@interface A : NSObject <S, T> {
	    ....
	@end

カテゴリに対してプロトコルを採用することもできます。

.. code-block:: objective-c

	@interface クラス名 (カテゴリ名) <プロトコル名>
	メソッドの宣言;
	  ...
	@end

必須機能とオプション機能の指定
=================================

Objective-C 2.0から、プロトコルに列挙されたメソッドのうちで必ず実装しなければならないものと、 **実装しなくてもよいものを指定できる** （オプション）ようになりました。

プロトコルで宣言している機能郡の中には、必ずしも実装しなくても良いというメソッドがあればオプションとして指定できます。
その場合、オプションのメソッドには「@optional」、必ず実装が必要なメソッドには「@required」というコンパイラ指示子用います。これらの指定がないメソッドは「@required」が指定されたのと同じで必ず実装しなければなりません。

例）アラーム

.. code-block:: objective-c

	@protocol Alarm
	- (void)setCurrentTime:(NSDate*)date;
	@property (assign) BOOL alarm;

	@optional
	@property (assign) BOOL snooze;
	- (void)pauseAlarm:(id)sender;

	@required
	- (void)setTimerAtHour:(int)h minute:(int)m;

	@end







