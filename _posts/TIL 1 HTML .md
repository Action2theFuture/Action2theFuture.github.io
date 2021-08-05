---
layout: post
title:  "TIL 1 | HTML 기초 💬"
date:   2021-03-11 21:03:36 +0530
categories: TIL HTML
---

## HTML(HyperText Markup Language)
---
**웹페이지를 위한 마크업언어(MarkUp Language)**

>참고 웹사이트 <br>https://www.advancedwebranking.com/html/#basic-elements-metadata>
https://developer.mozilla.org/ko/docs/Web/HTML

### HTML 작성
HTML은 웹 페이지 콘텐츠 안의 꺾쇠 괄호에 둘러싸인 "태그"로 되어있는 HTML 요소 형태로 작성한다.

### HTML 기본 구성

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
</body>
</html>
```

- `<head>` : 문서의 머리를 나타내는 태그입니다
`<body>`와 다르게 문서의 내용이 나타나지 않지만 데이터를 정의하는 태그들이 들어갑니다
- `<body>` : 문서의 내용을 나타내는 태그입니다
대부분의 태그가 `<body>`태그에 들어갑니다.
- `<Meta>` : 데이터를 설명하는 데이터를 지정하는 태그입니다
대부분의 페이지는 UTF-8로 지정되어 있습니다
- `<title>` : 제목을 지정하는 태그입니다
HTML문서의 제목을 지정합니다



### `<HEAD>`에 들어가는 대표적인 태그
- `<title>`
- `<meta>`
- `<link>` : 외부 문서를 연결시키는 태그입니다
CSS문서를 연결하거나 웹 문서를 연결시킵니다
- `<style>` : 웹 문서의 스타일을 정해주는 태그입니다
속성으로도 사용가능합니다
   - ```<body style="font-size:20px">```
   
### 자주 사용하는 HTML 태그
- `<div>` : 순수한 컨테이너를 지정하는 태그입니다
Class나 Id를 지정하면 CSS와 연동하여 사용됩니다
- `<span>` : `<div>`랑 비슷하지만 `display`속성이 inline이라는 차이점이 있습니다
>`<div>display block</div>div는 block요소를 가집니다`<br><div>display block</div>div는 block요소를 가집니다
`<span>display inline</span>span은 inline요소를 가집니다`<br><span>display inline</span>span은 inline요소를 가집니다
- `<p>`: 문단을 지정하는 태그입니다
- `<a>`: 하이퍼링크를 만들어주는 태그입니다
- `<script>`: client-side scripts(`JS`, `VBS`)를 불러오는 태그입니다
- `<br>`: 줄바꿈을 해주는 태그입니다
- `<input>`: 사용자의 데이터를 받을 수 있는 형식을 만들어주는 태그입니다
- `<form>`: 사용자의 데이터를 보낼 수 있는 `form` 문서의 양식을 나타내는 태그입니다
- `<nav>`: 현재 페이지 또는 다른 페이지를 이동하기 위한 링크를 만들어주는 태그입니다

### `<form>`
---
1.`<form>`의 속성
- action : 보낼 데이터 양식의 위치를 정해줍니다
- action-charset : 데이터를 보낼 문자 인코딩을 정해줍니다
- method : 양식을 제출할 때 사용할 HTTP method를 정해줍니다
  - post : 양식 데이터를 요청 본문으로 전송합니다 
  - get : 양식 데이터를 action `URL`과 `?` 구분자 뒤에 이어 붙여서 전송합니다
- target : 받은 데이터를 응답할 위치를 정해줍니다
- name : form의 이름을 정해줍니다

2.`<form>`의 요소
- `<input>` : 대화형 컨트롤을 생성합니다
`input`태그 내의 `type`을 지정함에 따라 다양한 유형을 가질 수 있다
- `<label>` : 사용자 인터페이스 항목의 설명을 나타냅니다

>`<label>`태그와 연동한 `<input>` 
<label>Click here <input type = "checkbox"></label><br>
>`<label>`태그와 연동하지 않은`<input>`
Click here <input type = "checkbox">

---

-  `<button>` , `<textarea>` , `<select>`, `<option>`, `<fieldset>`
  
<button>button</button><br>

<textarea>textarea</textarea>

<select>
 <option>select1</option>
 <option>select2</option>
 <option>select3</option>
</select>
><fieldset>fieldset</fieldset>
><checkbox><checkbox>


### `<input>`의 유형
  
---
  
```HTML
  <input type="type">
```


 - `button`, `checkbox`, `color`, `date`, `file`, `email`, `number`, `range`, `time`, `search`, `submit`
  
| type | example | purpose
|:----------:|:----------|:----------|
| **`button`** | <input type="button" value="button"> | 푸쉬 버튼
| **`checkbox`** | <input type="checkbox"> | 선택/해제하는 값을 갖는다
| **`color`** | <input type="color"> | 색을 지정해준다
| **`date`** | <input type="date"> | 날짜를 지정하고 달력을 열어준다
| **`file`** | <input type="file"> | 파일을 지정할 수 있다
| **`email`** | <input type="email" value="email@abc.co.kr"> | 이메일을 편집하는 것을 도와준다
| **`number`** | <input type="number" value ="0"> | 숫자를 입력할 수 있다
| **`range`** | <input type="range"> | 값이 가려진 숫자를 입력한다 
| **`time`** | <input type="time"> |  시간대가 없는 시간을 입력한다
| **`search`** | <input type="search" value="search"> |  검색문자열을 입력한다
| **`submit`** | <input type="submit" value="submit"> | 양식을 전송하는 버튼
<br>

---

### 쓰면서 느낀점 ❕❔
처음으로 velog로 기술블로그를 작성하니 쓰면서 모르는 부분을 배워가고 아는 부분도 부족한 게 무엇인지 알 수가 있었다 
시작이 반이라는 말이 있듯이 꾸준히 조금씩 쓰다보면 달라지는 나의 모습이 보여진다


쓰면서 임시저장을 안 해서 3번정도 다시 써야했다 
중간 중간에 저장버튼을 누르는 것을 잊지 말아야겠다
 ~~노트북이 온전하게 있어서 다행이다~~




