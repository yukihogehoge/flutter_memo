# Chapter2-3
## リスト2_2〜2_4
```dart
class Widget2_2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // scaffoldは建築の「足場」を指す
    // MaterialAppのhomeにScaffoldクラスのインスタンスを指定することで、一般的なデザインのアプリが作成できる。
    return Scaffold(
      // 上部に表示されるアプリバーで、titleを指定する。childは指定しない。
      appBar: AppBar(
        title: Text('Hello, Flutter!'),
        backgroundColor: Colors.purple,
      ),
      // body: メインコンテンツの領域
      body: Text(
        'Hello, Flutter world!!',
        style: TextStyle(fontSize: 32.0),
      ),
    );
  }
}
```
### Scaffoldの主な引数一覧
- appBar: 上部に表示されるアプリバー
- body: メインコンテンツの領域
- floatingActionButton: 右下に表示されるFABボタン
- drawer: 左側のナビゲーションメニュー（引き出し）　などなど

```dart
class Widget2_3 extends StatefulWidget {
  final String title;
  final String message;
  // ウィジェットを作成する最初に呼び出されるもので、親のキーと必須（required）の引数がインスタンス時に生成される
  const Widget2_3({super.key, required this.title, required this.message});

  @override
  // createStateメソッドをオーバーライド
  // Widget2_3ウィジェットに対応するStateオブジェクトを返す
  State<Widget2_3> createState() => _Widget2_3State();
}

// Stateを継承したクラス
class _Widget2_3State extends State<Widget2_3> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // widget.title => 対応するウィジェットの変数titleを参照する
      appBar: AppBar(title: Text(widget.title)),
      body: Text(
        widget.message,
        style: TextStyle(fontSize: 32.0),
      ),
    );
  }
}
```

```dart
class Widget2_4 extends StatefulWidget {
  // 定数titleを宣言
  final String title;
  // 親のキーと必須の引数（title）を持つコンストラクタを作成することで、インスタンス生成時に必ずtitle引数を入れるようにする
  const Widget2_4({super.key, required this.title});

  @override
  // Widget2_4ウィジェットに対応するStateオブジェクトを返す
  State<Widget2_4> createState() => _Widget2_4State();
}

// Stateを継承したクラス
class _Widget2_4State extends State<Widget2_4> {
  String _message = 'Hello!';
  // メッセージを変更するメソッド
  void _setMessage() {
    // setState() => 状態変更をする
    setState(() {
      _message = 'タップしました！';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        // 状態変更前にはクラスに定義した_messageが表示される
        _message,
        style: TextStyle(fontSize: 32.0),
      ),
      floatingActionButton: FloatingActionButton(
        // ボタンが押されると_setMessageメソッドが実行される
        onPressed: _setMessage,
        // ウィジェットにマウスを重ねたとき（Webやデスクトップ）、または長押ししたとき（モバイル）」に表示される小さな説明テキスト
        tooltip: 'set message.',
        // FABの子要素としてこのアイコンを表示する
        child: Icon(Icons.star),
      ),
    );
  }
}
```
## リスト2_7〜3_1
```dart
import 'package:flutter/material.dart';

void main() {
  // 'new'は省略可能！！！
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Generated App',
      theme: new ThemeData(
        // Material 3が自動的に有効になっており、AppBarの背景色は ThemeData.primaryColor ではなく、
        // ColorScheme.surface や ColorScheme.primary などに従う。これを回避するためにfalseにする。
        useMaterial3: false,
        primarySwatch: Colors.teal, // 主要色はColorsクラスのプロパティを指定することで設定できる。
        primaryColor: const Color(0xFF009688),
        // accentColor: const Color(0xFF009688),
        canvasColor: const Color(0xFFfafafa),
      ),
      home: new Widget2_10(),
    );
  }
}

class Widget2_7 extends StatefulWidget {
  // nullも許容する
  Widget2_7({Key? key}) : super(key: key);
  @override
  _Widget2_7State createState() => new _Widget2_7State();
}

class _Widget2_7State extends State<Widget2_7> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Text(
        "Hello Flutter!",
        style: new TextStyle(
          fontSize: 32.0,
          // 定数にすることで同じインスタンス内で参照することができ、メモリの節約になる。
          // Colorはconstを使用するのを基本と考える。
          color: const Color(0xFF000000),
          fontWeight: FontWeight.w700,
          // fontFamily => フォントの種類（書体） の指定
          // Roboto => Googleが開発したサンセリフ体のフォントで、androidでのデフォルトフォント。読みやすく、モダンなデザインなのが特徴。
          fontFamily: "Roboto",
        ),
      ),
    );
  }
}

class Widget2_9 extends StatefulWidget {
  Widget2_9({Key? key}) : super(key: key);
  @override
  _Widget2_9State createState() => new _Widget2_9State();
}

class _Widget2_9State extends State<Widget2_9> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Center(
        // child: => Centerウィジェットに子要素を追加
        child: new Text(
          "Hello, Flutter!",
          style: new TextStyle(
            fontSize: 32.0,
            color: const Color(0xFF000000),
            fontWeight: FontWeight.w700,
            fontFamily: "Roboto",
          ),
        ),
      ),
    );
  }
}

class Widget2_10 extends StatefulWidget {
  Widget2_10({Key? key}) : super(key: key);
  @override
  _Widget2_10State createState() => new _Widget2_10State();
}

class _Widget2_10State extends State<Widget2_10> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Container(
        child: new Text(
          "Hello, Flutter!",
          style: new TextStyle(
            fontSize: 32.0,
            color: const Color(0xFF000000),
            fontWeight: FontWeight.w700,
            fontFamily: "Roboto",
          ),
        ),

        padding: const EdgeInsets.all(20.0), // 全方向を設定（値はdouble型にする）
        // padding: EdgeInsets.fromLTRB(10, 20, 40, 80), => 個別に設定（左、上、右、下）
        // padding: const EdgeInsets.only(top: 10, bottom: 20), => 余白を作りたい部分のみ設定（無記載部分は0になる）
        // padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 60), => 左右、上下それぞれ同じ値を設定
        alignment: Alignment.bottomCenter, // 中央下
      ),
    );
  }
}

class Widget2_12 extends StatefulWidget {
  Widget2_12({Key? key}) : super(key: key);
  @override
  _Widget2_12State createState() => new _Widget2_12State();
}

class _Widget2_12State extends State<Widget2_12> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Column(
        mainAxisAlignment:
            MainAxisAlignment.start, // columnウィジェットの配置場所をsizeの範囲内で指定
        mainAxisSize: MainAxisSize.max, //minは文字の範囲、maxは上から下まで
        crossAxisAlignment:
            CrossAxisAlignment.start, // column内のウィジェットの配置場所（どこ寄せかっぽい挙動になる）
        // children => 複数の子要素を指定
        children: <Widget>[
          new Text(
            "One",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w700,
              fontFamily: "Roboto",
            ),
          ),

          new Text(
            "Two",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w700,
              fontFamily: "Roboto",
            ),
          ),

          new Text(
            "Three",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w700,
              fontFamily: "Roboto",
            ),
          ),
        ],
      ),
    );
  }
}

class Widget2_13 extends StatefulWidget {
  Widget2_13({Key? key}) : super(key: key);
  @override
  _Widget2_13State createState() => new _Widget2_13State();
}

class _Widget2_13State extends State<Widget2_13> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Row(
        // columnと同じ
        mainAxisAlignment: MainAxisAlignment.center,
        mainAxisSize: MainAxisSize.max,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: <Widget>[
          new Text(
            "One",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w400,
              fontFamily: "Roboto",
            ),
          ),

          new Text(
            "Two",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w400,
              fontFamily: "Roboto",
            ),
          ),

          new Text(
            "Three",
            style: new TextStyle(
              fontSize: 32.0,
              color: const Color(0xFF000000),
              fontWeight: FontWeight.w400,
              fontFamily: "Roboto",
            ),
          ),
        ],
      ),
    );
  }
}

class Widget3_1 extends StatefulWidget {
  Widget3_1({Key? key}) : super(key: key);
  @override
  _Widget3_1State createState() => new _Widget3_1State();
}

class _Widget3_1State extends State<Widget3_1> {
  static var _message = 'ok!';
  static var _janken = <String>['グー', 'チョキ', 'パー'];

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text('App Name')),
      body: new Center(
        child: new Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            new Padding(
              child: new Text(
                _message,
                style: new TextStyle(
                  fontSize: 32.0,
                  color: const Color(0xFF000000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
              ),

              padding: const EdgeInsets.all(20.0),
            ),

            new TextButton(
              onPressed: buttonPressed,
              child: Padding(
                padding: EdgeInsetsGeometry.all(10.0),
                child: new Text(
                  "Push me!",
                  style: new TextStyle(
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto",
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void buttonPressed() {
    setState(() {
      // 同じオブジェクトに対してメソッドを連続して呼びたいときにカスケード記法'..'を使用する。
      // .shuffle()はlistの中身（要素の順序）を直接変更するメソッド。新しいリストを返すわけではないので、戻り値はvoidになる。
      // .add()や.sort()
      _message = (_janken..shuffle()).first;
    });
  }
}

```
