# JavaScript Element

## 객체 생성

|함수명| 설명|
|--|--|
|createElement(tagName)|element node를 생성한다.|
|createTextNode(text)|text node를 생성한다.|
|appendChild(node)|객체에 node를 child로 추가한다.|
|setAttribute(name)|객체의 속성을 지정한다.|
|getAttribute(name)|객체의 속성값을 가져온다.|
|innerHTML| 문자열을 HTML 태그로 삽입한다.|
|innerText| 문자열을 text node로 삽입한다.|

<br>

## 객체 생성 예제

```javascript
window.onload = function(){
  //변수를 선언하고 element node와 text node 생성
  var title = document.createElement('h2');
  var msg = document.createTextNode('Hello SSAFY !!!');
  
  //text node를 element node에 추가
  title.appendChild(msg);
  document.body.appendChild(title);
```
<br>

```javascript
window.onload = function() {
  var profile = document.createElement('img');
  profile.src = 'profile.png';
  profile.width = 150;
  profile.height = 200;
  
  document,body.appendChild(profile);
};//가장 간단한 방법이지만 웹 표준이나 웹 브라우저가 지원하는 태그의 속성 만 사용이 가능하다.

window.onload = function() {
  var profile = document.createElement('img');
  profile.setAttribute('src', 'profile.png');
  profile.setAttribute('width',150);
  profile.setAttribute('height', 200);
  
  profile.setAttribute('data-content','내사진');//이런 웹 브라우저가 지원하지 않는 태그의 속성도 가능하다
  
  document,body.appendChild(profile);
};
```

<br>

```javascript
window.onload = function() {
  var html = document.getElementById('divHtml');
  var text = document.getElementById('divText');
  
  html.innerHTML = '<h2>Hello SSAFY!!!</h2>'; //Hello SSAFY!!!가 화면에 나옴
  text.innerText = '<h2>Hello SSAFY!!!</h2>'; //<h2>Hello SSAFY!!!</h2>가 화면에 나옴
};
```
<br>

## 객체 가져오기

|함수명|설명|
|--|--|
|getElementById(id)| 태그의 id 속성과 일치하는 element <b>객체</b> 가져오기|
|getElementsByClassName(classname)| 태그의 class 속성이 classname과 일치하는 element <b>배열</b> 가져오기|
|getElementsByTagName(tagname)| 태그이름이 tagname과 일치하는 element <b>배열</b> 가져오기|
|getElementsByName(name)| 태그의 name 속성이 name과 일치하는 element <b>배열</b> 가져오기|
|querySelector(selector)| selector에 일치하는 첫번째 element <b>객체</b> 가져오기|
|querySelectorAll(selector)| selector에 일치하는 모든 element <b>배열</b> 가져오기|

<br>

## getElementById(id)

```javascript
<script type="text/javascript">
    window.onload = function() {
        var msg = document.getElementById('header');

        msg.innerHTML = '안녕!!!</h2>';
    }
</script>
<body>
    <h2 id="header">Hello!!!</h2>
</body>
```
![image](https://user-images.githubusercontent.com/64126100/190870151-07f0c6af-c642-4402-be78-d559ddc4c5ff.png)

<br>

## getElementsByClassName(classname)

```javascript
<script type="text/javascript">
    window.onload = function() {
        var color = ['orange', 'blue', 'purple'];
        var TEXT = document.getElementsByClassName('text');

        for(var i=0;i<TEXT.length;i++){
            TEXT[i].style.background = color[i];
        }
    }
</script>

<body>
    <h2 class="text">Hello 3th!!!</h2>
    <h2 class="text">Hello 4th!!!</h2>
    <h2 class="text">Hello 5th!!!</h2>
</body>
```
![image](https://user-images.githubusercontent.com/64126100/190870105-b324886e-1fd5-4cae-8bdb-77d806df7928.png)

<br>

## getElementByTagName(tagname)

```javascript
<script type="text/javascript">
    window.onload = function() {
        var color = ['orange', 'blue', 'purple'];
        var TEXT = document.getElementsByTagName('h2');

        for(var i=0;i<TEXT.length;i++){
            TEXT[i].style.background = color[i];
        }
    }
</script>

<body>
    <h2>Hello 3th!!!</h2>
    <h2>Hello 4th!!!</h2>
    <h2>Hello 5th!!!</h2>
</body>
```
![image](https://user-images.githubusercontent.com/64126100/190870105-b324886e-1fd5-4cae-8bdb-77d806df7928.png)

<br>

## querySelector(selector)

```javascript
<script type="text/javascript">
    window.onload = function() {
        var msg = document.querySelector('#header');

        msg.innerHTML = '안녕!!!</h2>';
    }
</script>
<body>
    <h2 id="header">Hello!!!</h2>
</body>
```

![image](https://user-images.githubusercontent.com/64126100/190870151-07f0c6af-c642-4402-be78-d559ddc4c5ff.png)

<br>

## querySelectorAll(selector)

```javascript
<script type="text/javascript">
    window.onload = function() {
        var color = ['orange', 'blue', 'purple'];
        var TEXT = document.querySelectorAll('.ssafy');

        for(var i=0;i<TEXT.length;i++){
            TEXT[i].style.background = color[i];
        }
    }
</script>

<body>
    <h2 class="ssafy">Hello 3th!!!</h2>
    <h2 class="ssafy">Hello 4th!!!</h2>
    <h2 class="ssafy">Hello 5th!!!</h2>
</body>
```
![image](https://user-images.githubusercontent.com/64126100/190870105-b324886e-1fd5-4cae-8bdb-77d806df7928.png)




