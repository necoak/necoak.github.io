# Pythonでのテスト

# 単体テスト
* unittestモジュールを使う

* TestCase継承クラスでテストケースを実装。名称として接頭語に`Test`をつける慣習
* テストメソッドの接頭語として`test_`をつける
* テストメソッドの中でassertを行う
  * assertEqual / assertNotEqual
  * assertTrue / assertFalse