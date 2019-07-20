# 標準ライブラリ

## datetimeモジュール
* date : 年月日を扱う日付型
* time : 時分秒、マイクロ秒を扱う時刻型
* datetime : 日付時刻型
* timedelt : 日付、時刻の間隔を扱う

* 比較は算術演算子が使える
* 文字列変換は、f-stirngsで指定する
  * f'{dt:%Y/%m/%d}' 
    * %Y: 4桁年、

https://docs.python.org/ja/3/library/datetime.html#strftime-and-strptime-behavior

```python
# date
from datetime import date

date1 = date(2019, 6, 7)
print(str(date1)) # 2019-06-07
print(str(date1.weekday())) # 4: Thursday
print(str(date1.year)) # 2019
print(str(date1.month)) # 6
print(str(date1.day)) # 7
print(f'{date1:%Y/%m/%d}') # 2019/06/07

# time
from datetime import time

time1 = time(23, 45, 59)
print(str(time1))
print(str(time1.hour))
print(str(time1.minute))
print(str(time1.second))
print(f'{time1:%H:%M:%S}')
```

### tempfileモジュール
* 一時ファイルやディレクトリの作成
* https://docs.python.org/ja/3/library/tempfile.html

```python
import tempfile

with tempfile.TemporaryFile(mode='w') as f:
    print('hello tempfile, f)

with tempfile.NamedTemporaryFile(mode='w') as f:
    print('hello readable named tempfile', f)
```

### argparse
* コマンドライン引数
* argparseチュートリアル
  * https://docs.python.org/ja/3/howto/argparse.html#id1
* argparse API
  * https://docs.python.org/ja/3/library/argparse.html

```python
if __name__ == '__main__':
    parser = argparse.ArgumentParser(description='コマンドの説明文をかくことができます')
    parser.add_argument('length', type=int, help='生成するパスワード長')
    parser.add_argument('-c', '--complex', action='store_true',
                        help='文字数字だけでなく記号も含める場合指定')
    args = parser.parse_args()
    print(password_generator(args.length, args.complex))
```
* 使用の流れ
  * 1. ArgumentParserインスタンスを作り
  * 2. 引数をparserにaddし(parser.add_argument)
  * 3. パースする(parser.parse_args)

* オプション引数
* 

### docstring
TBD

### logging
* プログラムのログを出力するライブラリ
  * printfデバッグよりも出力レベルや出力先を変えられるので便利

```python
import logging

logging.basicConfig(level=logging.INFO)

def main():
    logging.info('main started.')

    try:
        zerodivede = 2 / 0
    except ZeroDivisionError as e:
        logging.error('error occured: %s', e)

    logging.info('main ended.')
```

* ロギング設定
  * `logging.basicConfig(...)`
     * level:  logging.CRITICAL, logging.ERROR, logging.WARN, logging.INFO, logging.DEBUG ..
     * handlers
       * loging.StreamHandler, logging.FileHandler
       * setLevel: 
       * setFormatter: 

* example
```python
import logging
stream_handler = logging.StreamHandler()
stream_handler.setLevel(logging.INFO)
stream_handler.setFormatter(logging.Formatter(
    '%(pathname)s:%(lineno)s %(asctime)s %(name)s %(levelname)s %(message)s'
    ))

file_handler = logging.FileHandler('./logs/script.log')
file_handler.setLevel(logging.ERROR)

logging.basicConfig(
    level=logging.INFO,
    handlers=[stream_handler, file_handler])
```

### string
* string.ascii_letters
* string.digits
* string.punctuation

### random
* random.shuffle()
* random.sample()

### io
* io.StringIO