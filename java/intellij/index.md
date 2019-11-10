# IntellJ IDEA の使い方メモ

### 留意点(Eclipseとの違い)
* ファイルは自動で保存される
  * 回避方法: TBW
* 自動ビルドは標準で無効になっている
  * 有効化方法: TBW
* ワークスペース、パースペクティブがない
* キーマップ

## ショートカット

| 操作 | IJショートカット | (参考:Eclipse) |
|---|---|---|
| コード補完 | Ctrl + Space | Ctrl+Space |
| QuickFix | Alt + Enter | Ctrl + 1  / Ctrl + 2 |
| コマンド検索 | Shift 2回押し | Ctrl + 3 |
|  |  |  |
|  |  |  |

## エディタショートカット

| 操作 | ショートカット |
|---|---|
| 取り消し(Undo) | Ctrl + Z |
| やり直し(Redo) | Ctrl + Shift + Z |
| 検索(Find) | Ctrl + F |
| 置換(Replace) | Ctrl + R |
| 行/選択範囲の複製(Duplicate) | Ctrl + D |
| プロジェクト内検索 | Ctrl + Shift + F |
| プロジェクト内置換 | Ctrl + Shift + R |

### ファイルを作る
* `Alt + 1` でツールウィンドウへフォーカスを当て、作成したいパスへ移動
* `Alt + Insert`で新規ファイル作成

### リアルタイムプレビュー(HTML)
* LiveEditを用いる

* 準備:
  * IntelliJ で LiveEcitプラグインをインストールする
  * Chromeには、JetBrains IDE Supportエクステンションをインストールする
* 使い方
  * 対象ファイルを右クリック→Debug

### 便利機能
* インテンションアクション
  * Alt + Enter

* Postfix Completion
  * 評価式を書いたあとに「.XXX」と書くと、式になってくれる
    * "aaa".log → cosole.log("aaa")
    * arg1 > arg2.if → if(arg1 > arg2)
    * arg3.var → var arg3 = arg;

* Expand Selection
  * Ctrl + W
  * 構文に従って選択範囲を広げることができる
  * 逆向きは Ctrl + Shift + W

* コードフォーマット
  * Ctrl + Alt + L
  * 対象ファイルをフォーマットする
  * Preferences 

* リネームリファクタリング
  * Shift + F6

## Java

Inspection
Ctrl + F1 : 警告の内容を表示
→ Alt + Enter インテンショナクションで警告を解消、もしくは手で解消