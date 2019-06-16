# Pythonでのテスト

# 単体テストフレームワーク
* unittestモジュールを使う

* TestCase継承クラスでテストケースを実装。名称として接頭語に`Test`をつける慣習
* 該当モジュールの階層にtestsフォルダを切って、test_xxxx.pyというモジュール名で実装する慣習
* テストメソッドの接頭語として`test_`をつける
* テストメソッドの中でassertを行う
  * assertEqual / assertNotEqual
  * assertTrue / assertFalse

```python
import unittest


def add1(v):
    return v + 1


class TestAdd1(unittest.TestCase):
    def test_call(self):
        self.assertEqual(add1(1), 2)


def canDivideBy2(v):
    return ((v % 2) == 0)


class TestCanDivideBy2(unittest.TestCase):
    def test_call(self):
        self.assertTrue(canDivideBy2(4))
        self.assertFalse(canDivideBy2(5))
```

実行の仕方
```
> python -m unittest tests.test_foo
```

# Mock
* unittestモジュールに含まれるモックフレームワーク

```python
import unittest
from unittest import mock

def foo(user):
    return {'name': user.name, 'fullname': user.get_fullname()}

class TestFoo(unittest.TestCase):
    def test_call(self):
        dummy = mock.Mock()
        dummy.name = 'John' # 属性のセット
        dummy.get_fullname.return_value = 'John Smith' # 関数返り値のセット
        
        self.assertEqual(foo(dummy), {'name': 'John', 'fullname': 'John Smith'})
        dummy.get_fullname.assert_called_once()
```
## mock.patch
* 既存オブジェクトに対し置き換えしてテストすることができる
