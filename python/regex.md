# 正規表現@Python

* reモジュール
    * https://docs.python.org/ja/3/library/re.html

### Specific Characters

```
.  : 改行以外の任意の一文字
^  : 文字列先頭
$  : 文字列の末尾

```

### Special Sequence 
バックスラッシュで始まる特殊シーケンス
```
\d : 任意の数字
\D : \d以外
\s : 任意の空白文字
\S : \s以外
\w : 任意のUnicode文字
\W : \w以外
\A : 文字列の先頭
\Z : 文字列の末尾
```

### Escape Sequence

```
\t : タブ
\n : 改行
```

### Meta Character
* `\s` : バックスラッシュと小文字のs。文字列リテラルで表現するには..?
   * 方法1: バックスラッシュをエスケープする : `'\\s'`
   * 方法2: raw文字列を使う : `r'\w'`

## 操作
* match : 先頭からマッチするか
* search : 途中でマッチするか
* split : 区切り文字をパターンで分割
* sub : パターンを別文字で置換
* findall : すべてのパターンを列挙リスト化

### re.match(パターン, 対象文字列)
Todo
キャプチャ
()で囲まれたパターンに一致した文字列を記録して、あとでとりだせるようにする
* `(\\d+)円$` 



* re.search(パターン, 対象文字列)

## その他
### コンパイル
* 何度も正規表現マッチさせる場合、コンパイルしたほうが実行が効率的になる
```python
# result = re.match(pattern, string) と同等
prog = re.compile(pattern)
result = prog.match(string)
```

### r文字列
* raw文字列。エスケープシーケンスが利用できない
```python
r'abc'
```

### 量指定子
* 出現回数を指定してマッチさせることができる
  * `{出現回数}`
```python
re.match('^\d{3}-\d{4}$') # nnn-nnn : zipcode
```
* 0回または1回の出現
  * `?`
```python

```
### split

# 熟語
## 「、」で分割
