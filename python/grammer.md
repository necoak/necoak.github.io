# Python文法

# 文字列操作
### スライス
* インデックス
  * `s[n]` : nインデックス目の文字
  * 範囲外を指定した場合はIndexErrorがスローされる

* 文字列のスライス
  * 以下は0origin
  * 省略なしで書くと`文字列[位置a:位置b]`で、aインデックス目からbインデックス目までの部分文字列の抽出
  * `s[1:3] ` : 1インデックス目からから3インデックス目まで（含まず）の文字列
  * `s[:3]` : 3インデックス目まで（含まず）の文字列
  * `s[1:]` : 1インデックス目以後の文字列

* ステップ指定のスライス
  * 省略なしで書くと`文字列[位置a:位置b:ステップ]`で、aインデックス目からbインデックス目までのステップ文字ごとの部分文字列の抽出
  * `s[::2]` : 文字列全体を、0インデックス目、2インデックス目、4インデックス目...と部分文字列
  * `s[::-1]` : ステップのマイナス指定の場合は逆からの指定

### コンテナ操作(list, dict, set, tupple)
* インデックス操作
  * `lst[n]` : nインデックス目の要素
  * `lst[-n]` : 末尾n番目の要素 (`lst[-1]`で最後尾の要素)

### 演算子
* `+` : 結合
* `==`
`比較で==使っていいのは、いいな。Javaだと.equalsメソッドを使うもんな`

# 条件文
* if / elif / else 
  * switch case文はない

# 標準IO
* `input()`
* `print()`
  * `end=` : 末尾改行を他の文字列にしたい場合は、`print(x, end=' ')`のようにendパラメータを指定する
  * `sep=` : `print(1, 2, 3, sep='-)` を実行すると`1-2-3`となる

# キャスト(型変換)
* int
* 集合体
  * list
  * set

## 内包表記

* リスト、ジェネレータ式、集合、辞書のオブジェクトを生成する方法
```python
# [要素の式 for 変数 in イテレーティブ]
# examples
sq = [i**2 for i in range(10)] # 長さ10の平方数列
pt = [[x, y]
      for x in range(-1,2)
      for y in range(-1,2)
      if abs(x - y) == 1] #
```

# データタイプ
### タプル(tupple)
* 変更不可のオブジェクト（イミュータブル）
  * かっこで囲む
* アンパックにより複数変数に同時代入できる
```python
items = (1, 2, 3)
a, b, c = items
# -> a:1, b:2, c:3 に代入される
a, *b = items
# -> a:1, b:[2, 3] と*付変数は可変長で受け取れる
```

### 集合(set)
* 順序なし
* 同じものは1つだけ保持できる
* イミュータブルオブジェクトしか保持できない
```python

```

* 集合演算が使える
```python
s1 = {'a', 'b'}
s2 = {'b', 'c'}
s1.difference(s2) # 差集合 {'a'}
s1.intersection(s2) # 積集合 {'b'}
s1.symmetric_difference(s2) # 対称差 {'a', 'c'}
s1.union(s2) #和集合 {'a', 'b', 'c'}
```

### allとany


# 関数
### 標準形
```
def func(仮引数):
   処理
   return 値
```

### パラメータ指定とデフォルト引数
* パラメータ指定、つまり仮引数を指定lして関数実行すると、対象の仮引数に値を渡すことができる
* デフォルト引数を指定すると、引数を省略して関数実行することができる
```python
def func(arg1, arg2=2, arg3=3):
   print(arg1, arg2, arg3)

func(10, 20, 30)  # 10 20 30
func(10, 20)  # 10 20 3
func(arg1=10)  # 10 2 3
func(10, arg3=30)  # 10 2 30
func(arg3=300, arg1=100, arg2=200) # 100 200 300
```

### 可変長引数
* 仮引数に`*`をつけると、それ以降の引数をタプルとして受け取る可変長引数となる
* そのままその仮引数を関数内で使うとタプルになってしまうが、
  `*`をつけて使用するとアンパックして使用することができる（便利）
```python
def func(*args):  # ここを修正
    print(args)
    print(*args)


func('hello', 'world')
```

* ちなみにアンパック自体は、関数外でも使える(便利)
```python
tpl = ('a', 'b', 'c')
print(tpl)
print(*tpl)

lst = ['a', 'b', 'c']
print(lst)
print(*lst)
```

### 任意個数のキーワード引数
* 仮引数に`**`をつけると任意のキーワード引数を受け取れる。タプルではなく、特定の引数として受け取れる。
* `*args`と合わせて、任意個数引数の関数定義をしたい場合に利用することが多い

```python
def func(**kwargs):
    print(kwargs)

func(abc=1, xyz='xyz')

def func(*args, **kwargs):
    print(args, kwargs)

func(1, 2, 3, abc=1, xyz='xyz')
```

* キーワード引数は、さらに関数呼び出しする際のキーワード引数としてそのまま渡すことができる（便利）
* つまり、ラッパー関数を作るときに、そのまま引数を渡せてしまう。超便利
```python
# printのラッパー関数を定義
def print_with_log(*args, **kwargs):
    logger.info(...)  # ここでログを出力するなどかぶせる処理を実装
    print(*args, **kwargs) # 本来の処理を呼び出す。このとき、print関数に対しキーワード引数そのまま渡せる
```

* `func(*args, **kwargs`という意味
  * `*args` ... 引数がリスト展開されて渡される
  * サンプル
  ```python
  args = [1, 2, 3]
  kwargs = {'sep': '-', 'end': '.'}
  print(*args, **kwargs)  # print(1, 2, 3, sep='-', end='.') -> 1-2-3.
```

### 無名関数(ラムダ式)
```
lambda 引数: 式
```

### ドキュメンテーション文字列(docstring)
* docstringは、`help()`で表示される内容を記述する。javadocと同じような内容。
  * 書き方
    * 1行目に簡潔説明
    * 2行目は空行
    * 3行目以降に詳細な内容

```python
def add(a, b):
    """Add a and b.
    
    `add(a, b)` is same as `a + b`
    """
    return a + b
```

# 慣用句
## for
```python
for i in range(10):
   ....
```

## dict
```python
d = {}
for k, v in d:
   ...
```

## join
```python
' '.join
# a b c
print(' '.join(['a', 'b', 'c']))
```

# エラー
### 関数内のスコープ変数の割当てタイミング

* 下記実装では、グローバル変数を参照してprintするのかと思いきや、iという関数ローカル変数が先に作られ、変数アサインする前に参照したので、unboundエラーが出ている。
* 他の言語(例えばjs)だと、スコープという考え方から、ローカルを参照→なければグローバルとなるのだが、python(3系)はこの変数スコープの扱いが厳密になっているようだ
```python
i = 123  # グローバル変数
def func3():
    print(i)
    i = 0
    print(i)
```

実行結果
```
UnboundLocalError: local variable 'i' referenced before assignment
```

# 文字列フォーマット

## フォーマット
* `f-strings` : 
* `str.format` : `{}`

### f-strings
* `f'{式:フォーマット}'`
```python
print(f'{1 / 3:.2}') # '0.33
print(f'{dt:%Y-%m-%d %H:%M:%S}') # '2019-06-07 23:45:59'
```

### str.format
```python
str.format：'{:.2}'.format(1 / 3)
```

### %演算子
* 最近のpython3ではあまりつかわない。Cのprintf書式と同じ
```python
'%.2f' % (1 / 3)
```

## 文字列の整列（左寄せ右寄せセンタリング、パディング）
* ljust
* rjust
* center
* zfill

```python
v = -12.3
print(str(v).ljust(7, '0'))  # -12.300
print(str(v).rjust(7, '0'))  # 00-12.3
print(str(v).center(7, '0')) # 0-12.30
print(str(v).zfill(7))       # -0012.3
```

## ファイル入出力
```python
# ファイルの書き込み
with open('sample.txt','w', encoding='utf-8') as fp:
    fp.write('今日の天気は')

# ファイルの追記
with open('sample.txt','a', encoding='utf-8') as fp:
    fp.write('晴れです\n')
    fp.write('午後からは曇りになります\n')

# ファイルの読み込み
with open('sample.txt', encoding='utf-8') as fp:
    s = fp.read()

print(s)
```

* 読み込み関数
  * read
  * readline
  * redlines


## jsonモジュール
* 標準ライブラリにjsonモジュールがありそれを使う
  * dump(データ構造) : 変換(データ構造 -> json文字列)
  * dump(データ構造, ファイルオブジェクト) : 変換してファイル保存(データ構造 -> json文字列)
  * loads(json文字列) : 変換(json文字列 -> データ構造)
  * loads(ファイルオブジェクト) : ファイルに書かれたjson文字列を読み込んで変換(json -> データ構造)

### pickleモジュール
* データのシリアライズ・デシリアライズ
  * dumps(データ構造) : 変換(データ構造->bytes)
  * dump(データ構造, ファイルオブジェクト) : 
  * loads
  * load

# よくわからない
* ジェネレータ、ジェネレータ式

# よく使う
* strptime
datetime.datetime.strptime(date_str, '%Y/%m/%d %H:%M')
* 末尾改行削除
  * rstrip
  ```python
  with open('sample.txt)
  ```

# csvから読み込む
```python
csv_vals = []
with open('test.csv', 'r', encoding='utf-8') as fp:
    for row in fp:
        ss = row.rstrip().split(',') # 本当はカンマ区切りをもうちょっとちゃんと扱わないと
        csv_kvs.append(ss)
```

* csvライブラリを使う
```python
import csv

with open('input.csv', 'r') as fp:
    reader = csv.reader(fp)
    header = next(reader)  # ヘッダーを読み飛ばしたい時
    for row in reader:
        print(row)# row 要素のリストとなる
```

* pandasライブラリを使う
ToDo


# Collection
## Set

### 操作
* add
* remove
* discard : removeと同じ挙動だが、対称要素がなくてもエラー発出しない
* clear: 保持する要素をすべてからにする
* pop: 要素を１つだけ取り出す

### 集合演算
 * `|` : 和集合
 * `-` : 差集合
 * `&` : 積集合
 * `^` : 対称差 ... `A△B = (A−B)∪(B−A)`
    * ```python
        subset1 = {1, 2, 3}
        subset2 = {3, 4, 5}
        symmetricdifference = subset1 ^ subset2 # {1, 2, 4, 5}
      ```

## リスト操作便利関数
* enumerate
  * シーケンスとカウントのタプルを返す関数
    ```python
enumerate(['a', 'b', 'c']) # [(0, 'a'), (1, 'b'), (2, 'c')]
    ```

* zip
  * 引数に指定した複数のリスト要素のタプルを作る
  * 複数のリストで長さが合わない場合、一番短いものに合わせられる

## リスト内包表記
* basic
  * `[i **2 for i in range(1, 10)]`


# 関数
## デコレータ
* 関数の前に`@`をつけて書くものをデコレータという
* デコレータをつけることにより、その関数

* `@classmethod`
* `@staticmethod`
* `@property`
* `@functools.lru_cache()`
* `@app.route(path)`
