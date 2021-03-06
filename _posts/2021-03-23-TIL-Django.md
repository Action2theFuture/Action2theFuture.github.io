---
layout: post
title: "Django ๊ธฐ์ด ๐ฌ"
date: 2021-03-23
categories: TIL Django Python
---

![](https://images.velog.io/images/action2thefuture/post/902d3ca2-5b97-4d0b-a689-711fcfd65fd9/%EC%9E%A5%EA%B3%A0.jpg)

# Python's Framework

[Django ๊ณต์๋ฌธ์](https://docs.djangoproject.com/ko/3.1/)

# Django ์์ โจ

---

## Django ์ค์น๐

```bash
$ python -m pip install Django
```

### ์ค์น ํ์ธ

```bash
$ python -m django --version
```

### ๊ฐ์ํ๊ฒฝ

๊ฐ ํ๋ก์ ํธ์ ํ๊ฒฝ์ค์ ์ ๋ํด ๋๋ฆฝ์ ์ํค๊ธฐ ์ํด ๊ฐ์ํ๊ฒฝ์ ์ค์นํ๋ค

```bash
pip install virtualenv
```

**๐zsh: command not found: ์ค๋ฅ์**

**ํ๊ฒฝ๋ณ์ ์ค์ **

```bash
code ~/.zshrc
export PATH=/ํ๋ก๊ทธ๋จ ๊ฒฝ๋ก:$PATH
```

**๊ฐ์ํ๊ฒฝ ๋ง๋ค๊ธฐ**

```bash
$ virtualenv myenv
```

## django ๊ตฌ์กฐ

---

![](https://images.velog.io/images/action2thefuture/post/6f7c8398-78de-4fac-810f-20c5e0fda8e5/django.jpg)

- **Model** ๋ฐ์ดํฐ ์ ์ฅ
- **View** ๋ฐ์ดํฐ๋ฅผ ๋ณด์ฌ์ค
- **Control, Template** ์ฌ์ฉ์์ ์๋ ฅ๊ณผ ์ด๋ฒคํธ์ ๋ฐ์ํ์ฌ Model๊ณผ View ์๋ฐ์ดํธ

## ํ๋ก์ ํธ ์์ ๐โโ๏ธ๐โโ๏ธ

---

```bash
$ django-admin startproject mysite
```

![](https://images.velog.io/images/action2thefuture/post/7477e548-9f32-4c7a-9f7b-e8775af10029/%EC%98%88%EC%8B%9C%2015.png)

```
myenv/
  mysite/
      manage.py
      mysite/
          __init__.py
          settings.py
          urls.py
          asgi.py
          wsgi.py
```

**manage.py**

```bash
$ python manage.py `๋ช๋ น์ด`
```

**๐ฃ ๋ช๋ น์ด**

- startapp ์ฑ ์์ฑ
- runserver ์๋ฒ ์คํ
- createsuperuser ๊ด๋ฆฌ์ ์์ฑ
- makemigrations app app์ ๋ชจ๋ธ ๋ณ๊ฒฝ ์ฌํญ ์ฒดํฌ
- migrate ๋ณ๊ฒฝ ์ฌํญ์ DB์ ๋ฐ์
- shell ์์ ํตํด ๋ฐ์ดํฐ๋ฅผ ํ์ธ
- collectstatic static ํ์ผ์ ํ ๊ณณ์ ๋ชจ์

**settings.py**
ํ๋ก์ ํธ์ ํ๊ฒฝ ๋ฐ ๊ตฌ์ฑ์ ์ ์ฅ

- DeBug ๋๋ฒ๊ทธ ๋ชจ๋(๊ธฐ๋ณธ์ผ๋ก True๋ก ์ค์ )
- INSTALLED.APPS pip๋ก ์ค์นํ ์ฑ ๋๋ ๋ณธ์ธ์ด ๋ง๋  ์ฑ์ ์ถ๊ฐ
- MIDDELWARE.CLASSES Request์ Response ์ฌ์ด์ ์ฃผ์๊ธฐ๋ฅ ๋ ์ด์ด
- TEMPLATES djang template ๊ด๋ จ ์ค์ , ์ค์  view(html, ๋ณ์)
- DATABESE ๋ฐ์ดํฐ ๋ฒ ์ด์ค ์์ง์ ์ฐ๊ฒฐ์ค์ 
  ๊ฐ๋ฐ ์๋ฒ์์๋ python๋ง์ผ๋ก ์ถฉ๋ถํ ์๋์ด ๊ฐ๋ฅํ๋ค
- STATIC_URL ์ ์  ํ์ผ์ URL(CSS,JS,image,etc)

## App ๋ง๋ค๊ธฐ ๐จ

```bash
$ python manage.py startapp myapp
```

![](https://images.velog.io/images/action2thefuture/post/c76fa8e3-b6d3-4bf3-b59c-3db5f62a2d4e/%EC%98%88%EC%8B%9C%2016.png)

```
myenv/
  mysite/
      manage.py
      mysite/
          __init__.py
          settings.py
          urls.py
          asgi.py
          wsgi.py
  myapp/
      __init__.py
      admin.py
      apps.py
      migrations/
          __init__.py
      models.py
      tests.py
      views.py
```

### view ์์ฑ

`myapp/view.py`

```python
from django.http import HttpResponse

def index(request):
  return HttpResponse("Hello Django")
```

`myapp/urls.py`

```python
from django.urls import path

from . import views

urlpatterns = [
	# /myapp/
    path('', views.index, name='index'),
]
```

`mysite/urls.py`

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('myapp/', include('myapp.urls')),
#include๋ฅผ ์ฌ์ฉํ์ฌ url์ ๊ฐ์ ธ์ ์์ฝ๊ฒ ๊ด๋ฆฌํ  ์ ์๊ฒ ๋์๋ค
    path('admin/', admin.site.urls),
]
```

๐html ํ์ผ์ view.py๋ก ํ๋ฒ์ ์ฌ๋ฆฌ๋ ๋ฐฉ๋ฒ๋ ์๋ค

`view.py`

```python
from django.shortcuts import render

def index(request):
    name = "name"
    return render(request, 'myapp/templates/index.html', {
        'name': name,
    }
```

#### DataBase ์์ฑ

```bash
$ python manage.py makemigrate
```

### ๊ด๋ฆฌ์ ๋ง๋ค๊ธฐ

```bash
$ python manage.py createsuperuser
```

**๐์ด๊ธฐ ํ๋ฉด**

![](https://images.velog.io/images/action2thefuture/post/99056392-cb09-4fb7-9370-c58bf99251ab/%EC%98%88%EC%8B%9C%2017.png)

**๐๊ด๋ฆฌ์ ๊ถํ page**

![](https://images.velog.io/images/action2thefuture/post/e7727316-bedb-468f-bb8f-e50dea330e66/%EC%98%88%EC%8B%9C%2018.png)

- ๊ด๋ฆฌ์ ๊ถํ์ผ๋ก ์ฌ์ฉ์ ๊ถํ์ ์ค์ ํ  ์ ์๊ณ 
- ๊ฐ์ฒด๋ฅผ ์ญ์ , ์์ , ์ถ๊ฐ๋ฅผ ํ  ์๊ฐ ์๋ค

### MODEL ๋ง๋ค๊ธฐ

`myapp/models.py`

```python
from django.db import models

class Model(models.Model):
  name = models.CharField(max_length=50) #๊ธ์ ์๋ฅผ ์ ์ํ  ๋ ์ฌ์ฉ
  title = models.CharField(max_length=50)
  contents = models.TextField() #๊ธ์ ์๊ฐ ์ ํ์ด ์์ ๋ ์ฌ์ฉ
  url = models.URLField() #url์ ๋ฑ๋กํ  ๋ ์ฌ์ฉ
  email = models.EmailField() #email์ ๋ฑ๋กํ  ๋ ์ฌ์ฉ
  cdate = models.DateTimeField(auto_now_add=True) #๋ ์ง์ ์๊ฐ์ ์ ์ ํ  ๋ ์ฌ์ฉ

```

[MODEL ์ฐธ์กฐ](https://docs.djangoproject.com/en/2.0/ref/models/fields/#field-types)

**๊ด๋ฆฌ์ page๋ก app ๋ณ๊ฒฝ**

`myapp/admin.py`

```python
from django.contrib import admin
from .models import Model
# Register your models here.
admin.site.register(Model)
```

### Template System

`myapp/Templates/index.html`

```HTML
{% for Model in Model_list %}
<li>
  <a href="/view">{{ Model.title }}</a> | {{ Model.name }}
</li>
{% endfor %}
```

ํํ๋ฆฟ ์์คํ์ ์ด์ฉํ์ฌ ์ ์ ์ธ HTML์ ๋์ ์ธ Python์ ์ธ์ด๋ก ์ฌ์ฉ๊ฐ๋ฅํ๊ฒ ํด์ค ์ ์๋ค

#### App ๋ฑ๋ก

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp.apps.MyappConfig',
]
```

#### Model์ DB ํ์ฑํ

```bash
$ python manage.py makemigrations myapp
```

๋ณ๊ฒฝ์ฌํญ DB์ ์ ์ฅ

```bash
$ python manage.py migrate
```

## ๊ฐ๋ฐ ์๋ฒ ๋์

```bash
$ python manage.py runserver
```

**๋ช๋ น์ด ๋ค์ ์ํ๋ ํฌํธ ๋ฒํธ๋ฅผ ์ ์ด ์ฌ์ฉํ  ์ ์๋ค**

```bash
$ python manage.py runserver 8080
```
