==================
コードのレビュー
==================

もしもアプリケーションの動作に問題があったら、この章に載せてあるコードとあなたのコードを見比べて、actionやoutletの接続を再確認してみてください。

コードとコンパイラの警告
==============================

ここまでに書いたコードは警告なしにコンパイルできるはずです。もしも警告が出されているのであれば、それらの警告はエラーと同じくらいのつもりで扱った方が良いでしょう。
Objective-Cは柔軟な言語なので、コンパイラから受け取ることがあるのはほとんど警告かもしれません。

コードリスト
==============

このセクションではAppDelegateとTrackクラスのインターフェースファイルと実装ファイルを載せてあります。
これらのリストにはXcodeのテンプレートで追加されていたメソッドやコメントは表示していません。


Interfaceファイル:AppDelegate.h
-----------------------------------

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
	- (void)updateUserInterface;

	@end


実装ファイル:AppDelegate.m
------------------------------

.. code-block:: objective-c

	#import "AppDelegate.h"
	#import "Track.h"

	@implementation AppDelegate

	@synthesize textField = _textField;
	@synthesize slider = _slider;

	- (void)applicationDidFinishLaunching:(NSNotification *)aNotification
	{
	    Track *aTrack = [[Track alloc] init];
	    [self setTrack:aTrack];
	    [self updateUserInterface];
	}

	- (IBAction)mute:(id)sender {
	    [self.track setVolume:0.0];
	    [self updateUserInterface];
	}

	- (IBAction)takeFloatValueForVolumeFrom:(id)sender {
	    float newValue = [sender floatValue];
	    [self.track setVolume:newValue];
	    [self updateUserInterface];
	}

	- (void)updateUserInterface {
	    float volume = [self.track volume];
	    [self.textField setFloatValue:volume];
	    [self.slider setFloatValue:volume];
	}

	@end


Interfaceファイル:Track.h
-----------------------------------

.. code-block:: objective-c

	#import <Foundation/Foundation.h>

	@interface Track : NSObject
	@property (assign) float volume;

	@end


実装ファイル:Track.m
-----------------------

.. code-block:: objective-c

	#import "Track.h"

	@implementation Track

	@end
