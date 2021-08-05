---
layout: post
title: "Django Middleware"
date: 2021-05-07
categories: Request TIL Django middleware
---

# Django Middleware

![](https://images.velog.io/images/action2thefuture/post/f976fa4e-fd60-4a9e-b25b-3af9706644fe/django%20middleware.png)

**http요청이 들어오면 middleware를 거치고 view로 들어간 뒤 다시 middleware를 거치면서 http응답으로 들어온다**

미들웨어는 하나의 계층으로 이루어져서 순서대로 작동이 된다

- http 요청 - 위에서부터 아래로 적용이 된다
- http 응답 - 아래에서부터 위로 적용이 된다

Custom Middleware 구현

```python
#middleware.py
class JSONMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
        self.my_json_object = {
            "name" : "Doge",
            "age" : 5
        }

    def __call__(self, request):
        response = self.get_response(request)
        return response

    def process_template_response(self, _, response):
        response.context_data['my_json_object'] = self.my_json_object
        return response
```

- json을 보내주는 middleware를 간단하게 만들어보았다
  1. `JsonMiddelware` 이름의 class를 만들었다
  2. `my_json_object` 이름으로 딕셔너리를 만들었다
  3. `__call__` 함수를 이용하여 get_response를 리턴하였다
  4. `process_template_response` 함수에 my_json_object를 response에 넣어서 리턴하였다
     `process_template_response` 함수는 **middleware hook**
     (middleware에서 사용하는 특수 method)
- `get_response` 함수는 view나 middleware에서 호출하고 넘겨주기 위해 쓰이는 함수이다

```python
#setting.py
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'demo.middleware.JSONMiddleware',
    #추가된 middleware
]
```

setting.py안에 추가된 middleware를 넣어준다

```python
#view.py
from django.template.response import TemplateResponse
from django.http import HttpResponse

def index(request):
    context = {
        "name" : "neo"
    }
    return TemplateResponse(request, 'demo/index.html', context=context)
```

👇 **결과**
![](https://images.velog.io/images/action2thefuture/post/15613407-231f-4108-8eec-b27e0517da8f/json.png)

Django가 request로 여러 단계의 middleware를 지나가면서 여러가지 기능을 사용할 수 있도록 자동적으로 만들어주었다

````python

```python
#setting.py
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'corsheaders.middleware.CorsMiddleware',
]
````

## Request

Django는 request 및 response를 이용하여 시스템에 상태를 전달한다
`django.http`를 이용하여서 request와 response 객체를 불러올 수 있다

```python
#view.py
import json

from django.http     import JsonResponse, HttpResponse
from django.views    import View

class IndexView(View)
   def get(self, requset)
     data = {
        'coin' : 'doge',
        'price' : 600,
        'value' : 'trash',
       }
     return JsonResponse(data)

   def post(self, request)
     data = json.loads(request.body)
     return HttpResponse('SUCCESS')
```

Django에서 제공하는 HttpResponse로 많은 속성값을 사용할 수 있다

**1. HttpRequest.body**
바이트 문자열로 데이터를 처리할 때 사용한다 python에서 그대로 사용할 수 없으므로 json 모듈을 이용하여 파이썬이 읽을 수 있는 객체로 바꾸어서 사용이 가능하다
**2. HttpRequest.path**
해당 페이지의 경로를 확인이 가능하다
**3. HttpRequest.method**
get인지 post인지 http의 method를 문자열로 보여준다
**4. HttpRequest.POST**
딕셔너리 형태
**5. HttpRequest.GET**
딕셔너리 형태
**6. HttpReques.headers**
Http의 헤더를 대소문자를 구분하지 않고 딕셔너리같은 객체로 보내준다

[여러가지의 HttpRequest의 속성](https://docs.djangoproject.com/ko/3.2/ref/request-response/#django.http.HttpRequest.encoding)
