# Django

## プロジェクト生成
TBD

## コンポーネント
* View関数
  * Httpリクエスト/レスポンスを授受する
  * `django.http.HttpResponse`
* テンプレートエンジン
  * `django.template.response.TemplateResponse`
  * HTMLライクな書式で `{{変数名}}` で値渡しができる

### views.py
```python
from django.http import HttpResponse
from django.template.response import TemplateResponse


def index(request):
    return TemplateResponse(request, 'foo/index.html', {'title': 'ハローDjango'})
```

### テンプレート (foo/index.html)
```html
<html>
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
</head>
<body>
    <h1>{{title}}</h1>
</body>
</html>
```
