# スクレイピング

### Webコンテンツ取得
* ライブラリ`Requests`を使用
```python
url = "https://hogehoge.hoge/fugafuga.html"
response = requests.get(url)
response.encoding = response.apparent_encoding # レスポンスを適切な文字エンコーディングする

print(response.text)
```

## HTML解析(BeatifulSoup)
### 基本
* https://www.crummy.com/software/BeautifulSoup/bs4/doc/
* html.parser

```python
import requests
from bs4 import BeautifulSoup

# URLからHTMLを取得します
url = "https://docs.pyq.jp/_static/assets/scraping/parse1.html"
response = requests.get(url)
response.encoding = response.apparent_encoding

soup = BeautifulSoup(response.text, 'html.parser')

# ulタグで囲まれた部分を抽出します
ul_tag = soup.find('ul')

# ulタグの中のaタグを抽出します
for a_tag in ul_tag.find_all('a'):
    
    # aタグのテキストを取得
    text = a_tag.text
    # aタグのhref属性を取得
    link_url = a_tag['href']
    # 表示します
    print('{}: {}'.format(text, link_url))

```

### CSSセレクタを利用する

```python
import requests
from bs4 import BeautifulSoup

# URLからHTMLを取得します
url = "https://docs.pyq.jp/_static/assets/scraping/item-list.html"
response = requests.get(url)
response.encoding = response.apparent_encoding

bs = BeautifulSoup(response.text, 'html.parser')

# div.item-list で 囲まれた部分を抽出します
item_list = bs.find('div', class_='item-list')
# div.item で囲まれた部分を抽出
for item in item_list.find_all('div', class_='item'):
    # 商品名を抽出
    item_name = item.find('a', class_='item-name').text.strip()
    # 価格を抽出
    item_price = item.find('span', class_='item-price').text.strip()
    print('商品名: {} 価格: {}'.format(item_name, item_price))
```

### CSV解析(csvモジュール)

### XML解析(XXX)


### Excel解析(XXX)

# Scrapy
* https://doc.scrapy.org/en/latest/intro/tutorial.html
## 要素
* `Spider`

## 実行
```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = 'quotes-%s.html' % page
        with open(filename, 'wb') as f:
            f.write(response.body)
        self.log('Saved file %s' % filename)
```

### コマンド
`scrapy crawl quotes`

## 留意事項
### ディレイ
* 複数URLをクロールする際のアクセス間隔の設定（デフォルト値は0秒）。これによりクロール先へ負荷をかけないようにする。
* https://doc.scrapy.org/en/latest/topics/settings.html#download-delay
