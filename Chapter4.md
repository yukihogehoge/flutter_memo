# Chapter4のコード解説
## リスト4-1
```dart
class Widget4_1 extends StatefulWidget {
  const Widget4_1({super.key});

  @override
  State<Widget4_1> createState() => _Widget4_1State();
}

class _Widget4_1State extends State<Widget4_1> {
  static var _message = 'ok';
  static var _stars = '⭐︎⭐︎⭐︎⭐︎⭐︎';
  static var _star = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        // Text() => 単一のスタイルで文字列を表示するウィジェット
        title: Text('My App'),
        // leadingでAppBarタイトルの先頭にwidgetを配置。BackButtonは戻るボタン。
        leading: BackButton(color: Colors.white),
        // actions => titleWidgetの後路に並ぶ、widgetのリストを受け取るプロパティ
        // <Widget>というように型を明示的に指定すると、型安全の保証がなされ、読みやすくもなる
        actions: <Widget>[
          // IconButtonウィジェットのiconプロパティにIconsウィジェットを渡している
          // Iconsアイコン一覧が入っているクラスで、androidはその中に定義された定数(static const IconData)
          IconButton(
            icon: Icon(Icons.android),
            // tooltip => 長押しすると出てくる説明文
            tooltip: 'add star...',
            // 自作関数の参照を渡す。（iconPressedA()と書くと関数の呼び出しをして即時実行されてしまうので注意）
            onPressed: iconPressedA,
          ),
          IconButton(
            icon: Icon(Icons.favorite),
            tooltip: 'subtract star...', // 差し引く
            onPressed: iconPressedB,
          ),
        ],
        // PreferredSize => 子ウィジェットに「望ましいサイズ（特に高さ）」を明示的に指定するためのウィジェット
        // appBarやbottomNavigationBarなど、高さが必要な場所で使う
        bottom: PreferredSize(
          preferredSize: const Size.fromHeight(30.0),
          child: Center(
            child: Text(
              _stars,
              style: TextStyle(fontSize: 22.0, color: Colors.white),
            ),
          ),
        ),
      ),

      body: Center(
        child: Text(_message, style: const TextStyle(fontSize: 28.0)),
      ),
    );
  }

  void iconPressedA() {
    _message = 'tap "android".';
    _star++;
    update();
  }

  void iconPressedB() {
    _message = 'tap "favorite".';
    _star--;
    update();
  }

  void update() {
    // 三項演算子を使用。偽の時にさらに条件分岐するようなネスト構造になっている
    _star = _star < 0
        ? 0
        : _star > 5
        ? 5
        : _star;
    setState(() {
      // substring(開始位置, 終了位置) => 文字列を部分的に抽出
      _stars = '★★★★★☆☆☆☆☆'.substring(5 - _star, 5 - _star + 5);
      _message = _message + '[$_star]';
    });
  }
}
```
## リスト4_2
```dart
class Widget4_2 extends StatefulWidget {
  // 親クラスにある key をそのまま名前付き引数として受け取り、直接渡す。
  const Widget4_2({super.key});

  @override
  _Widget4_2State createState() => _Widget4_2State();
}

class _Widget4_2State extends State<Widget4_2> {
  static var _message = 'ok!';
  static var _index = 1;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My App')),
      body: Center(
        child: Text(_message, style: const TextStyle(fontSize: 28.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _index,
        backgroundColor: Colors.lightBlueAccent,
        items: [
          BottomNavigationBarItem(
            label: 'Android',
            icon: const Icon(Icons.android, color: Colors.black, size: 50),
          ),

          BottomNavigationBarItem(
            label: 'Favorite',
            icon: const Icon(Icons.favorite, color: Colors.red, size: 50),
          ),

          BottomNavigationBarItem(
            label: 'Home',
            icon: const Icon(Icons.home, color: Colors.white, size: 50),
          ),
        ],
        // 一般的なボタン類と違い、イベントが用意されていないのでBottomNavigationBar側で用意する。
        // ボタン類との違いとして、クリックした項目のインデックス番号が引数(int型)として与えられる。
        onTap: tapBottomIcon,
      ),
    );
  }

  void tapBottomIcon(int value) {
    var items = ['Android', 'Favorite', 'Home'];
    setState(() {
      _index = value;
      _message = 'you  tapped: "' + items[_index] + '".';
    });
  }
}
```
## リスト4_3
```dart
class Widget4_3 extends StatefulWidget {
  Widget4_3({super.key});
  @override
  _Widget4_3State createState() => _Widget4_3State();
}

class _Widget4_3State extends State<Widget4_3> {
  static var _message = 'ok!';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My App')),
      body: Column(
        children: <Widget>[
          Text(_message, style: TextStyle(fontSize: 32.0)),
          ListView(
            shrinkWrap: true, // 追加された項目に応じて大きさを自動調整。
            // 【注意】Columnの中で使用する場合はfalseとすると高さが定まらなくなるのでエラーが出る。
            padding: const EdgeInsets.all(20.0),

            children: <Widget>[
              // リストに複数のテキストを表示
              Text('First item', style: TextStyle(fontSize: 24.0)),
              Text('Second item', style: TextStyle(fontSize: 24.0)),
              Text('Third item', style: TextStyle(fontSize: 24.0)),
              ListTile(
                leading: Icon(Icons.favorite, color: Colors.black45, size: 50),
                title: Text('Favorite', style: TextStyle(fontSize: 24.0)),
                selected: true,
                onTap: tapListTile, //=> クリックされた際に関数を実行する
                // onLongPress: LongPressListTile, => 長押しされた際に関数を実行する
              ),
            ],
          ),
        ],
      ),
    );
  }

  void tapListTile() {
    setState(() {
      _message = 'you tapped!';
    });
  }
}
```
## リスト4_4
```dart
class Widget4_4 extends StatefulWidget {
  Widget4_4({super.key});
  @override
  _Widget4_4State createState() => _Widget4_4State();
}

class _Widget4_4State extends State<Widget4_4> {
  static var _message = 'ok!';
  static var _index = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My App')),
      body: Column(
        children: <Widget>[
          Text(_message, style: TextStyle(fontSize: 32.0)),
          ListView(
            shrinkWrap: true, // 追加された項目に応じて大きさを自動調整
            // 【注意】Columnの中で使用する場合はfalseとすると高さが定まらなくなるのでエラーが出る
            padding: const EdgeInsets.all(20.0),
            children: <Widget>[
              // ListTileは表示領域を超えるとエラーになる。スクロール表示はできない
              ListTile(
                leading: const Icon(Icons.android, size: 32), // アイコンインスタンスの作成
                title: Text(
                  'first item',
                  style: TextStyle(fontSize: 28.0),
                ), // タイトルにtextウィジェットを設定
                selected: _index == 1, // _indexとListTileに割り当てた番号が一致したら選択状態とする
                onTap: () {
                  // クリックされた時の処理
                  _index = 1; // 番号の割り当て
                  tapTile(); // tapTileメソッドの呼び出し
                },
              ),
              ListTile(
                leading: const Icon(Icons.favorite, size: 32),
                title: Text('second item', style: TextStyle(fontSize: 28.0)),
                selected: _index == 2,
                onTap: () {
                  _index = 2;
                  tapTile();
                },
              ),
              ListTile(
                leading: const Icon(Icons.home, size: 32),
                title: Text('third item', style: TextStyle(fontSize: 28.0)),
                selected: _index == 3,
                onTap: () {
                  _index = 3;
                  tapTile();
                },
              ),
            ],
          ),
        ],
      ),
    );
  }

  void tapTile() {
    setState(() {
      _message = 'you tapped: No, $_index.';
    });
  }
}
```
## リスト4_5
```dart
class Widget4_5 extends StatefulWidget {
  Widget4_5({super.key});
  @override
  _Widget4_5State createState() => _Widget4_5State();
}

class _Widget4_5State extends State<Widget4_5> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My App')),
      // スクロール表示用のコンテナ
      body: SingleChildScrollView(
        child: Column(
          // Column のchildrenで埋まった領域に対する残りの領域を縦方向に最小化するプロパティ
          mainAxisSize: MainAxisSize.min,
          // childrenのWidgetの上下に均等にスペースを配置する設定
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: <Widget>[
            Container(
              color: Colors.blue,
              height: 120.0,
              child: const Center(
                child: Text('One', style: TextStyle(fontSize: 32.0)),
              ),
            ),
            Container(
              color: Colors.white,
              height: 120.0,
              child: const Center(
                child: Text('Two', style: TextStyle(fontSize: 32.0)),
              ),
            ),
            Container(
              color: Colors.blue,
              height: 120.0,
              child: const Center(
                child: Text('Three', style: TextStyle(fontSize: 32.0)),
              ),
            ),
            Container(
              color: Colors.white,
              height: 120.0,
              child: const Center(
                child: Text('Four', style: TextStyle(fontSize: 32.0)),
              ),
            ),
            Container(
              color: Colors.blue,
              height: 120.0,
              child: const Center(
                child: Text('Five', style: TextStyle(fontSize: 32.0)),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
## リスト4_6
```dart
// １つ目のスクリーン
class FirstScreen4_6 extends StatelessWidget {
  @override
  // BuildContext context => 現在のウィジェットがどこにあるか、親・祖先などの情報を持つオブジェクト
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Home')),
      // Center() => 子ウィジェットを親ウィジェットの中央に配置するためのウィジェット
      body: Center(
        child: Text('Home Screen', style: TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        // 現在選択されているインデックスの指定。本来は、開かれているタブにハイライトをつけるためにHomeの"0"を指定すべき
        currentIndex: 1,
        // ナビゲーションバーにアイテムを追加
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'Home',
            icon: Icon(Icons.home, size: 32),
          ),
          const BottomNavigationBarItem(
            label: 'next',
            icon: Icon(Icons.navigate_next, size: 32),
          ),
        ],
        onTap: (int value) {
          if (value == 1) {
            // Navigator => 画面表示を切り替える機能を提供（pushは保管して表示の切り替え、popは最後に保管していた表示に戻る）
            Navigator.push(
              // どこから画面を開くかを示す。contextは最初のbuild引数
              context,
              // 新しい画面として SecondScreen4_6() を表示するためのルートを作成。
              // builder に渡した関数が新しい画面のウィジェットを返す。
              MaterialPageRoute(builder: (context) => SecondScreen4_6()),
            );
          }
        },
      ),
    );
  }
}

// ２つ目のスクリーン
class SecondScreen4_6 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Next")),
      body: Center(
        child: const Text('Next Screen', style: TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'prev',
            icon: Icon(Icons.navigate_before, size: 32),
          ),
          const BottomNavigationBarItem(
            label: '?',
            icon: Icon(Icons.android, size: 32),
          ),
        ],
        onTap: (int value) {
          // 最後に保管したcontextを表示する
          if (value == 0) Navigator.pop(context);
        },
      ),
    );
  }
}
```
## リスト4_7
```dart
class FirstScreen4_7 extends StatefulWidget {
  const FirstScreen4_7({super.key}); // コンストラクタ

  @override
  _FirstScreen4_7State createState() => _FirstScreen4_7State();
}

class _FirstScreen4_7State extends State<FirstScreen4_7> {
  // TextEditingController => TextFieldやTextFormFieldの状態を管理するためのコントローラー（正体はクラスであり、インスタンス化して使用している）
  // テキストの変更を監視し、特定のアクションを実行したり、プログラムからテキストを変更したりすることができる
  static final _controller =
      TextEditingController(); // TextEditingController(text: '初期値')というように初期値を入れることができる。
  // 入力値を入れる変数
  static var _input = '';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Column(
        children: <Widget>[
          const Text('Home Screen', style: TextStyle(fontSize: 32.0)),
          // Padding() => 子ウィジェットの周囲に余白を追加するためのウィジェット
          Padding(
            padding: const EdgeInsets.all(20.0), // 余白指定
            child: TextField(
              controller: _controller,
              style: const TextStyle(fontSize: 28.0),
              onChanged: changeField,
            ),
          ),
        ],
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(label: 'Home', icon: Icon(Icons.home)),
          const BottomNavigationBarItem(
            label: 'next',
            icon: Icon(Icons.navigate_next),
          ),
        ],
        onTap: (int value) {
          if (value == 1) {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen4_7(_input)),
            );
          }
        },
      ),
    );
  }

  void changeField(String val) => _input = val;
}

class SecondScreen4_7 extends StatelessWidget {
  final String _value;

  SecondScreen4_7(this._value);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Next")),
      body: Center(
        child: Text(
          'you typed: "$_value".',
          style: const TextStyle(fontSize: 32.0),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before),
          ),
          BottomNavigationBarItem(label: '?', icon: const Icon(Icons.android)),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
        },
      ),
    );
  }
}
```
### 関数を呼び出す時に（）をつけるかどうかについて
| シーン                 | 書き方     | 意味                  |
| ------------------- | ------- | ------------------- |
| 関数を「**実行**」したいとき    | `関数名()` | 今すぐその関数を呼び出す        |
| 関数を「**渡すだけ**」にしたいとき | `関数名`   | あとで呼び出してもらう（準備だけする） |

- changeField（カッコなし）→ この関数を**あとで使う**ために渡す
```dart
onChanged: changeField; // フィールドが変更、編集されると関数を実行するという意味
```
- changeField()（カッコあり）→ 今すぐ**その場で**実行する  
これは「ユーザーが何もしてないのに勝手に呼ばれる」というバグの元になる
```dart
onChanged: changeField(); // 関数がその場で実行されて、返り値（void）がonChangedに渡される（これはNG）
```

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',
      theme: ThemeData(
        useMaterial3: false,
        primarySwatch: Colors.teal,
        primaryColor: const Color(0xFF009688),
        canvasColor: const Color(0xFFfafafa),
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen4_8(),
        '/second': (context) => NextScreen4_8('Second'),
        '/third': (context) => NextScreen4_8('Third'),
      },
    );
  }
}

class HomeScreen4_8 extends StatelessWidget {
  const HomeScreen4_8({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: const Text('Home Screen', style: TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(label: 'Home', icon: const Icon(Icons.home)),
          BottomNavigationBarItem(
            label: 'Next',
            icon: const Icon(Icons.navigate_next),
          ),
        ],
        onTap: (int value) {
          if (value == 1) {
            Navigator.pushNamed(context, '/second');
          }
        },
      ),
    );
  }
}

class NextScreen4_8 extends StatelessWidget {
  final String _value;
  NextScreen4_8(this._value);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Next")),
      body: Center(
        child: Text('$_value Screen', style: const TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before),
          ),
          BottomNavigationBarItem(label: '?', icon: const Icon(Icons.android)),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
          if (value == 1) Navigator.pushNamed(context, '/third');
        },
      ),
    );
  }
}
