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

```python
import unittest
from unittest import mock

from expires import get_expires_at


class TestExpiresAt(unittest.TestCase):
    @mock.patch('expires.time')
    def test__get_default(self, m):
        m.return_value = 1470620400
        actual_expired_time = get_expires_at()
        self.assertEqual(actual_expired_time, 1470624000)

    @mock.patch('expires.time')
    def test__get(self, m):
        m.return_value = 1470620400
        actual_expired_time = get_expires_at(7200)
        self.assertEqual(actual_expired_time, 1470627600)
    
    @mock.patch('expires.time', return_value=1470620401)
    def test__get1(self, _):
        actual_expired_time = get_expires_at(7200)
        self.assertEqual(actual_expired_time, 1470627601)
    
    def test__get2(self):
        with mock.patch('expires.time') as m:
            m.return_value = 1470620402
            actual_expired_time = get_expires_at(7200)
            self.assertEqual(actual_expired_time, 1470627602)
```
