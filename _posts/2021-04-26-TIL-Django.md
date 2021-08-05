---
layout: post
title: "SQL Django ORM"
date: 2021-04-26
categories: TIL Django-orm Python SQL
---

![](https://images.velog.io/images/action2thefuture/post/28c970ec-c1f6-4d88-96ac-afa5dea86697/sql%EB%AC%B8.png)

**테이블 안에 특정한 row를 가져오기**

```sql
SELECT price, description FROM products;
```

```python
products.objects.values('price', 'description').distinct()
```

**테이블에서 해당 인덱스까지 슬라이싱**

```sql
SELECT * FROM products LIMIT 10;
```

```python
products.objects.all()[:10]
```

**Limit, Offset**

```sql
SELECT * FROM products LIMIT 2 OFFSET 3;
```

4번째 row부터 2개의 row를 출력

```python
products.objects.all()[4:6]
```

**Filter**

```sql
SELECT * FROM products WHERE id = 1;
```

```python
products.objects.filter(id=1)
```

**Filter by comparison operators**

```sql
SELECT * FROM products WHERE price > 5000;
SELECT * FROM products WHERE price >= 5000;
SELECT * FROM products WHERE price < 5000;
SELECT * FROM products WHERE price <= 5000;
SELECT * FROM products WHERE price != 5000;
```

```python
products.objects.filter(price__gt=18)
products.objects.filter(price__gte=18)
products.objects.filter(price__lt=18)
products.objects.filter(price__lte=18)
products.objects.exclude(price=18)
```

**Between**

```sql
SELECT * FROM products WHERE price BETWEEN 3000 AND 5000;
```

```python
products.objects.filter(price__range=(3000, 5000))
```

**LIKE operator**

해당 문자열이 있는지 확인

```sql
SELECT * FROM products WHERE korean_name like '%A%';
SELECT * FROM products WHERE korean_name like binary '%A%';
SELECT * FROM products WHERE korean_name like 'A%';
SELECT * FROM products WHERE korean_name like binary 'A%';
SELECT * FROM products WHERE korean_name like '%A';
SELECT * FROM products WHERE korean_name like binary '%A';
```

```python
products.objects.filter(korean_name__icontains='A')
products.objects.filter(korean_name__contains='A')
products.objects.filter(korean_name__istartswith='A')
products.objects.filter(korean_name__startswith='A')
products.objects.filter(korean_name__iendswith='A')
products.objects.filter(korean_name__endswith='A')
```

i-swith : 대소문자 구별하지 않음

**IN operator**

```sql
SELECT * FROM products WHERE id in (1, 2);
```

```python
products.objects.filter(id__in=[1, 2])
```

**AND**

```sql
SELECT * FROM products WHERE id = 1 AND price > 3000;
```

```python
products.objects.filter(id = 1, age__gt=3000)
```

**OR**

```sql
SELECT * FROM products WHERE id = 1 OR price > 3000;
```

```python
from django.db.models import Q
products.objects.filter(Q(id = 1) | Q(age__gt=3000))
```

**NOT**

```sql
SELECT * FROM products WHERE NOT id = 1;
```

```python
products.objects.exclude(id=1)
```

**NULL**

```sql
SELECT * FROM products WHERE price is NULL;
SELECT * FROM products WHERE price is NOT NULL;
```

```python
products.objects.filter(price__isnull=True)
products.objects.filter(price__isnull=False)
```

```python
# Alternate approach
products.objects.filter(price=None)
products.objects.exclude(price=None)
```

**ORDER BY Keyword**

```sql
SELECT * FROM products ORDER by price;
# price를 오름차순
SELECT * FROM products ORDER bY price DESC;

# price를 내림차순
```

```python
products.objects.order_by('price')
products.objects.order_by('-price')
```

**Insert**

```sql
INSERT INTO products VALUES ('커피', 'coffee', 5000);
```

```python
products.objects.create(korean_name='커피', english_name='coffee', price=5000)
```

**Update**

```sql
UPDATE products SET price = price * 1.5;
```

```python
from django.db.models import F

products.objects.update(price=F('price')*1.5)
```

**Delete all rows**

```sql
DELETE FROM products;
```

```python
products.objects.all().delete()
```

**Delete specific rows**

```sql
DELETE FROM products WHERE price < 6000;
```

```python
products.objects.filter(price__lt=10).delete()
```

**Aggregation**

- MAX

```sql
SELECT MIN(price) FROM products;
```

```python
from django.db.models import Min

products.objects.all().aggregate(Min('price'))
```

- MIN

```sql
SELECT MAX(price) FROM products;
```

```python
from django.db.models import Max

producsts.objects.all().aggregate(Max('age'))
```

- AVG

```sql
SELECT AVG(price) FROM products;
```

```python
from django.db.models import Avg
products.objects.all().aggregate(Avg('price'))
```

- SUM

```sql
SELECT SUM(price) FROM products;
```

```python
from django.db.models import Sum
products.objects.all().aggregate(Sum('price'))
```

- COUNT

```sql
SELECT COUNT(*) FROM products;
```

```python
products.objects.count()
```

**GROUP**

```sql
select price, count('price') as count from products group by price
```

```python
products.objects.values('price').annotate(count=Count('price'))
```

- HAVING

```sql
SELECT price, count('price') as count FROM products group by price having count >  0;
```

```python
products.objects.annotate(count=Count('price'))
.values('price', 'count')
.filter(count__gt=0)
```

👇 **예시**

![](https://images.velog.io/images/action2thefuture/post/c8d49b4b-7374-4128-b70c-4238b3283485/query%20set.png)

**JOIN**

```python
models.py
class Products(models.Model):
    name = models.CharField(max_length=100)

class Categories(models.Model):
    products = models.ForeignKey(Products, on_delete=models.CASCADE)
```

- 가져오기

```sql
SELECT name
FROM Categories
LEFT JOIN Products
ON Categories.products_id = Products.id
WHERE Products.id=1;
```

```python
categories = Categories.objects.select_related('products').get(id=1)
categories.products.name
```

- 특정 products id를 가진 카테고리 가져오기

```sql
SELECT *
FROM Categories
WHERE Categories.products_id = 1;
```

```python
products = Products.objects.prefetch_related('categories_set').get(id=1)
categories = products.categories_set.all()
```
