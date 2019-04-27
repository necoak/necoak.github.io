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

