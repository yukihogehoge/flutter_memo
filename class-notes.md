# Flutterの概要
## Flutterとは？
- googleによって開発されたマルチプラットフォーム開発が可能なフレームワーク
- マテリアルデザインのコンポーネントを標準で用意しているので、初心者でも綺麗なUIのアプリが作成できる
## Dartとは？
- Flutterで使用するコンパイル型言語
- JavaScriptの問題点を改善した代替言語、Reactの書き方に似ている
- Null Safety: 基本null使用禁止とし、使用する場合は「int? a = null」といったように記述する。これにより、コンパイル時にエラーとして出てくるため実装時にnullエラーとして落ちることがなくなる。
## プロジェクトの作成
### コマンドプロンプトからの作成
コマンドプロンプト（ターミナル）に以下のコマンドを入れる
```
flutter create <<プロジェクトの名前>>
cd <<プロジェクトの名前>> //ディレクトリの移動
open iOS/Runner.xcworkspace //iosの場合のみ
flutter run
```
### vscodeからの作成
1. コマンド パレットを開く（F1、Ctrl+Shift+P、**Shift+Cmd+P**）
1. 「flutter new」と入力し、[Flutter: New Project] コマンドを選択
1. `Application`を選択し、プロジェクトを作成するフォルダを選択する。
1. ホームディレクトリ直下のworkspace内に保存。  
練習→sandbox/experiment 宿題→assignment プロジェクト→project
1. プロジェクトの名前を入力
【以下は補足】
-  `pubspec.yaml`で、現在のバージョン、依存関係、同梱するアセットなど、アプリの基本情報を指定
- `analysis_options.yaml`でFlutter がコードを解析する際の厳格さを指定  
→[Flutterのドキュメント](https://codelabs.developers.google.com/codelabs/flutter-codelab-first?hl=ja#2)を参照

## chapter1
### 環境構築で使えるコマンド
- `flutter doctor` flutter開発に必要なツール類をチェックし、開発の準備が整っているか判定してくれる
- `flutter create <プロジェクト名>` flutterプロジェクトを作成する

## chapter2
### プロジェクト構成
- libフォルダにmain.dartが格納されている

- 名前付き引数による関数（後から復習）

- ウィジェット: 部品
- ウィジェットツリー: 構造

```dart
void main() {
  runApp(ウィジェット);
}
```

- buildメソッド: Stateless/fulWidgetが生成されるときに呼び出される。return内でどんなWidgetかを指定する。  
- `class MaterialApp extends StatefulWidget`: このように、MaterialAppはStatefulWidgetを継承したクラスであり、titleに文字列、homeにウィジェットといった値をコンストラクタで受け取ることができる
- setState: ステートの更新があったことをステートクラスに知らせて画面を更新する
- `class _MyHomePageState extends State<MyHomePage> {略}`: ステートクラスの定義
- `Column()`: 受け取れるウィジェットはchildrenだけ！

### TextStyle
テキストのスタイルを指定するために用意されているクラス
- `fontSize`: 文字のサイズ
- `fontFamily`: 文字フォント
- `fontWeight`: 文字の太さ
  - `fontWeight: FontWeight.nomal`: 普通
  - `fontWeight: FontWeight.bold`: 太字
  >【補足】数値の場合、100から900までの9段階で定義。  
  boldやnormalは、これらの数値に対する別名（エイリアス）である。  
  FontWeight.normal: FontWeight.w400 と同じで、これが基準の太さ。  
  FontWeight.bold: FontWeight.w700 と同じ。

### Color
色を指定するクラス（2^24色分表現できる）  
`Color (255, 255, 3, 4)`: 一つ目の引数Aは透過度を指定できる

### Center
childで指定したWidgetを上下中央揃えで表示する
```dart
Center(
  child: Text("Hello, world!")
)
```
### Container
Centerよりも、より細かく位置の調整をする場合に使用する
- EdgeInsets: 周囲の余白幅を設定するためのクラス
- Alignment: 配置場所を設定するためのクラス
```dart
Container(
  child:
  Text(略),
  padding: const EdgeInsets.all(10.0),  // 全方位に10だけ余白
  alignment: Alignment.bottomCenter, // 中央下
)
```

### Column
複数のウィジェットを縦に並べて表示する
- `mainAxisAlignment: MainAxisAlignment.start`: 上下の位置（画面の一番上）
- `crossAxisAlignment: CrossAxisAlignment.center`: 文字の揃え位置（中央揃え）

## chapter3
### カスケード記法
メソッド呼び出し時に..で繋げることで、元のオブジェクトを参照することができる。  
例: `print((sample..add(4)).num)`でsampleオブジェクトが持つnumフィールドを出力できる。

### 様々な入力
- TextField: 自由に文字を入力させたい時
- Checkbox, Switch: 要素に該当するかどうかをチェックさせたい時
- Radio, Dropdown(PopupMenuButton): 複数の要素から1つだけ選ばせたい時
- Slider: 特定の値の範囲で数値を入力させたい時

### 3項演算子
<値> ? <値=trueの時の値> : <値=falseの時の値>
```dart
void main() {
  int a = 10;
  print(a < 10 ? "ok" : "ng");
}
```

### null許容

