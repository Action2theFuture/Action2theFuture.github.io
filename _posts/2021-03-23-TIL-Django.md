---
layout: post
title: "Django 기초 💬"
date: 2021-03-23
categories: TIL Django Python
---

![](https://images.velog.io/images/action2thefuture/post/902d3ca2-5b97-4d0b-a689-711fcfd65fd9/%EC%9E%A5%EA%B3%A0.jpg)

# Python's Framework

[Django 공식문서](https://docs.djangoproject.com/ko/3.1/)

# Django 시작 ✨

---

## Django 설치🎈

```python
$ python -m pip install Django
```

### 설치 확인

```
$ python -m django --version
```

### 가상환경

각 프로젝트의 환경설정에 대해 독립을 시키기 위해 가상환경을 설치한다

```
pip install virtualenv
```

**👇zsh: command not found: 오류시**

**환경변수 설정**

```python
code ~/.zshrc
export PATH=/프로그램 경로:$PATH
```

**가상환경 만들기**

```
$ virtualenv myenv
```

## django 구조

---

![](https://images.velog.io/images/action2thefuture/post/6f7c8398-78de-4fac-810f-20c5e0fda8e5/django.jpg)

- **Model** 데이터 저장
- **View** 데이터를 보여줌
- **Control, Template** 사용자의 입력과 이벤트에 반응하여 Model과 View 업데이트

## 프로젝트 시작 🏃‍♂️🏃‍♀️

---

```python
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

```
$ python manage.py `명령어`
```

**📣 명령어**

- startapp 앱 생성
- runserver 서버 실행
- createsuperuser 관리자 생성
- makemigrations app app의 모델 변경 사항 체크
- migrate 변경 사항을 DB에 반영
- shell 쉘을 통해 데이터를 확인
- collectstatic static 파일을 한 곳에 모음

**settings.py**
프로젝트의 환경 및 구성을 저장

- DeBug 디버그 모드(기본으로 True로 설정)
- INSTALLED.APPS pip로 설치한 앱 또는 본인이 만든 앱을 추가
- MIDDELWARE.CLASSES Request와 Response 사이의 주요기능 레이어
- TEMPLATES djang template 관련 설정, 실제 view(html, 변수)
- DATABESE 데이터 베이스 엔진의 연결설정
  개발 서버에서는 python만으로 충분히 작동이 가능하다
- STATIC_URL 정적 파일의 URL(CSS,JS,image,etc)

## App 만들기 🔨

```
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

### view 작성

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
#include를 사용하여 url을 가져와 손쉽게 관리할 수 있게 되었다
    path('admin/', admin.site.urls),
]
```

👇html 파일을 view.py로 한번에 올리는 방법도 있다

`view.py`

```python
from django.shortcuts import render

def index(request):
    name = "name"
    return render(request, 'myapp/templates/index.html', {
        'name': name,
    }
```

#### DataBase 생성

```python
$ python manage.py makemigrate
```

### 관리자 만들기

```python
$ python manage.py createsuperuser
```

**😁초기 화면**

![](https://images.velog.io/images/action2thefuture/post/99056392-cb09-4fb7-9370-c58bf99251ab/%EC%98%88%EC%8B%9C%2017.png)

**🔗관리자 권한 page**

![](https://images.velog.io/images/action2thefuture/post/e7727316-bedb-468f-bb8f-e50dea330e66/%EC%98%88%EC%8B%9C%2018.png)

- 관리자 권한으로 사용자 권한을 설정할 수 있고
- 객체를 삭제, 수정, 추가를 할 수가 있다

### MODEL 만들기

`myapp/models.py`

```python
from django.db import models

class Model(models.Model):
  name = models.CharField(max_length=50) #글자 수를 정의할 때 사용
  title = models.CharField(max_length=50)
  contents = models.TextField() #글자 수가 제한이 없을 때 사용
  url = models.URLField() #url을 등록할 때 사용
  email = models.EmailField() #email을 등록할 때 사용
  cdate = models.DateTimeField(auto_now_add=True) #날짜와 시간을 정의 할 때 사용

```

[MODEL 참조](https://docs.djangoproject.com/en/2.0/ref/models/fields/#field-types)

**관리자 page로 app 변경**

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

템플릿 시스템을 이용하여 정적인 HTML을 동적인 Python의 언어로 사용가능하게 해줄 수 있다

#### App 등록

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

#### Model의 DB 활성화

```python
$ python manage.py makemigrations myapp
```

변경사항 DB에 저장

```python
$ python manage.py migrate
```

## 개발 서버 동작

```
$ python manage.py runserver
```

**명령어 뒤에 원하는 포트 번호를 적어 사용할 수 있다**

```
$ python manage.py runserver 8080
```
