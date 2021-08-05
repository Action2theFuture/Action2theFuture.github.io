---
layout: post
title: "Django C.R.U.D"
date: 2021-05-05
categories: TIL CRUD Django
---

![](https://images.velog.io/images/action2thefuture/post/b31ea212-9511-48bc-9563-80469fd650cc/%EC%9E%A5%EA%B3%A0.jpg)

# C.R.U.D

## Model 작성

```python
#models.py
from django.models import Model

class Model(models.Model):
  id = models.BigAutoField(primary_key=True)
  name = models.CharField(max_length=30)
  age = models.IntegerField()

  def __str__(self):
     return self.name

  class Meta:
     db_table = "Model"
```

### M2M

```python
#models.py
from django.models import Model

class Models(models.Model):
  id = models.BigAutoField(primary_key=True)
  name = models.CharField(max_length=30)
  age = models.IntegerField()
  clothes = models.ManyToManyField('Model', through="Models_Clothes", verbose_name="clothes", related_name="models")

  def __str__(self):
     return self.name

  class Meta:
    db_table = "models"

class Models_Clothes(models.Model):
  id =models.BigAutoField(primary_key=True)
  models = ForeignKey("Models", on_delete=models.CASCADE, verbose_name = "models")
  clothes = ForeignKey("Clothes", on_delete=models.CASCADE, verbose_name = "clothes")

class Clothes(models.Model):
  id = models.BigAutoField(primary_key=True)
  name = models.CharField(max_length=30)
  color = models.CharField(max_length=30)

  def __str__(self):
     return self.name

 class Meta:
   db_table = "clothes"
```

**models.ManyToManyField()**

## Create / Update

```python
#view.py
import json
from django.http import JsonResponse
from django.views import View

class ModelView(View):
  def post(self, request):
    data = json.loads(request.body)
    models.objects.create(name=data['name'],age=data['age'])
    return JsonResponse({'MESSAGE':'SUCCESS'}, status = 201)
```

## Read

```python
#view.py
import json
from django.http import JsonResponse
from django.views import View

class ModelView(View):
  def get(self, request):
    models = Models.objects.all()
    models_result = []
    for model in models:
      models_result.append(
        {
          "name":model.name,
          "age":model.age,
        }
       )
    return JsonResponse({'models_result':models_result}, status=200)
```

## Delete

```python
#view.py
import json
from django.http import JsonResponse
from django.views import View

class ModelView(View):
  def delete(self, request):
    data = json.loads(request.body)
    model= models.object.get(name=data['name'])
    model.delete()
    return JsonResponse({'MESSAGE':'SUCCESS'}, status = 201)
```

### Request, Json

- `request.body`는 bytes형태로 저장되어 있다
- json형식으로 보내지기 때문에 python 객체로 바꿔주는 `json Module`을 import를 하여서 python으로 사용가능할 수 있게 해준다
  - Serialization - json
  - Deserialization - python 객체

## Templates

```
#view.py
from django.template import loader
from django.http import HttpResponse
from django.models import Model
from django.views import View

class ModelView(View):
   def templates(request):
     context = {
          'name':name,
     }
     template = loader.get_template('models/template.html')
     return HttpResponse(template.render(context, request))
```

### django.shortcuts에서 제공하는 render()

```
#view.py
from django.template import loader
from django.shortcuts import render
from django.models import Model
from django.views import View

class ModelView(View):
   def templates(request):
     context = {
          'name':name,
     }
     return render(request, 'models/template.html', context)
```

**render(request objects,templates 이름,context(딕셔너리형 객체))**

## Form

```python
#forms.py
from django.forms import ModelForm

class Form(ModelForm):
    class Meta:
        model = Products
        fields=['name', 'age']
```
