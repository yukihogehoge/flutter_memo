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
