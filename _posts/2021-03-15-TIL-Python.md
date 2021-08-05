---
layout: post
title: "Beautiful Soup"
date: 2021-03-11 21:03:36 +0530
categories: TIL Python WebScraping Beautifulsoup
---

**웹 크롤링(Web Crawling) / 웹 스크래핑(Web Scraping)**
HTML에서 원하는 데이터를 추출하기 위해 사용되는 패키지

## Beautiful Soup 시작

파이썬의 Package Manager인 PIP를 이용하여 Beautiful Soup을 설치한다

```python
>> pip install bs4


from bs4 import BeautifulSoup
```

사이트의 정보를 가져오기 위해선 **requests**가 필요하다

```python
>> pip install requests

import requests
```

## HTML Parsing

```python
import requests
from bs4 import BeautifulSoup

url = "https://python.flowdas.com/tutorial/index.html"

data = requests.get(url)
soup = BeautifulSoup(data.text, "html.parser")
```

requests로 해당 사이트의 요청이 성공하면(response 200) beautifulsoup으로 해당 사이트의 HTML을 parsing할 수 있다

## ✨Scraping

![](https://images.velog.io/images/action2thefuture/post/9c56b920-57b4-4e56-96fd-16ce09cbcfd9/%EC%98%88%EC%8B%9C%209.png)

> https://python.flowdas.com/tutorial/index.html

---

**개발자도구**로 해당 HTML의 구조를 확인해본다
![](https://images.velog.io/images/action2thefuture/post/084a3b79-e58b-4e74-a120-29bf4268f456/%EC%98%88%EC%8B%9C%2011.png)
간단하게 몇줄의 code로 사이트의 정보를 원하는 부분만 가져올 수 있다
![](https://images.velog.io/images/action2thefuture/post/586c35a1-5296-447a-abe8-0b717e86721f/%EC%98%88%EC%8B%9C%2010.png)

```python
import requests
from bs4 import BeautifulSoup

url = "https://python.flowdas.com/tutorial/index.html"

data = requests.get(url)
soup = BeautifulSoup(data.text, "html.parser")

title = soup.find("div", {"class":"toctree-wrapper compound"}).find_all("a")

for i in title:
  print(i.text)
```

☝위 예시는 `find()`와 `find_all()`로 찾아보았다

👇**CSS selector**를 이용하여 찾을 수 있는 `select_one()`과 `select()`으로 사용해 볼 수 있다
![](https://images.velog.io/images/action2thefuture/post/39d37a91-bc06-42c8-a761-1e22f6592a29/%EC%98%88%EC%8B%9C%2012.png)

```python
import requests
from bs4 import BeautifulSoup

url = "https://python.flowdas.com/tutorial/index.html"

data = requests.get(url)
soup = BeautifulSoup(data.text, "html.parser")

title = soup.select(".toctree-wrapper > ul > li  a")

for i in title:
  print(i.text)
```

**CSS selector**

- 자손 선택자
  선택자1 선택자2

선택자1 하위의 선택자2에 해당되는 모든 요소

- 자식 선택자
  선택자1 > 선택자2

선택자1 하위의 선택자2에 해당되는 직계 자식 요소
