---
layout: post
title: "BootStrap"
date: 2021-03-13 21:03:36 +0530
categories: TIL HTML CSS BootStrap
---

## BootStrap

---

**HTML, CSS, JS로 이루어진 FrameWork**

🧱 FrameWork : 재사용성을 극대화시킨 하나의 틀

### BootStrap 시작

[부트스트랩](https://getbootstrap.com/)

1.CDN을 이용

CSS

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/css/bootstrap.min.css"
  rel="stylesheet"
  integrity="sha384-BmbxuPwQa2lc/FVzBcNJ7UAyJxM6wuqIj61tLrc4wSX0szH/Ev+nYRRuWlolflfl"
  crossorigin="anonymous"
/>
```

JS

```html
<script
  src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/js/bootstrap.bundle.min.js"
  integrity="sha384-b5kHyXgcpbZJO/tY9Ul7kGkf1S0CWuKcCD38l8YkeH8z8QjE0GmW1gYU5S9FOnJ0"
  crossorigin="anonymous"
></script>
```

2.다운로드된 파일을 직접 적용

### BootStrap 적용

요소 안에 BootStrap에서 정한 Class를 넣으면 html의 code로 편리하게 작성이 가능하다

```html
<div class="container">...</div>
```

### 내장된 Grid System

기기나 ViewPort에 따라 12개의 열이 나누어지는 것을 가능하게 해준다

```html
8:4 비율로 나누어진다
<div class="row">
  <div class="col-md-8">.col-md-8</div>
  <div class="col-md-4">.col-md-4</div>
</div>

4:4:4 비율로 나누어진다
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4">.col-md-4</div>
</div>
```

`<div class="col-크기-숫자"></div>`

- 크기 : `xs` - 모바일 ,`sm` - 태블릿,`md` - 데스크탑, `lg` - 데스크탑
- 숫자 : 총 합이 12로 맞춰진다

### BootStrap Components

![](https://images.velog.io/images/action2thefuture/post/0e474a8f-740e-4821-a3c8-fb76f90ce84e/%EC%98%88%EC%8B%9C.png)

원하는 Component의 코드를 복사해서 사용할 수 있다

### 반응형 웹

<br>

👇 **최대화했을때**
![](https://images.velog.io/images/action2thefuture/post/53dc4b30-ece2-4c92-9061-0db29ef82dff/%EC%98%88%EC%8B%9C2.png)
👇 **일정크기이하로 줄일 때**
![](https://images.velog.io/images/action2thefuture/post/e4871fb9-6df2-40ac-9056-515f6974b3a3/%EC%98%88%EC%8B%9C3.png)

**Bootstrap이 자동적으로 반응형 웹으로 만들어준다
하지만, 원치 않을 시 반응형을 제거할 수 있다**

1.viewport `<meta>` 를 제거

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1, shrink-to-fit=no"
/>
```

2.해당 요소의 가로폭 지정

```html
.container { width: 1000px !important; }
```

3.그리드 레이아웃
.col-xs-\* 클래스로 변경
