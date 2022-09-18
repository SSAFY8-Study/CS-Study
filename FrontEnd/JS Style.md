# JavaScript에서 style tag 속성 가져오기

<pre><code>
//getElementsByTagName을 사용해 style tag의 요소들을 배열로 받아올 수 있다
var str = document.getElementsByTagName("STYLE")[0];

//지정된 id의 style 속성에 접근할 수 있다
var str = document.getElementById("idName").style;
</code></pre>

<style>에 접근하여 요소들을 받아올 수 있다.


<br>
<br>

<pre><code>
//<style> 태그를 생성할 수 있다.
var ss = document.createElement("STYLE");
//style 속성 정의
var text = document.createTextNode("body {color:red;}");
//정의한 속성을 style 태그의 child로 추가
ss.appendChild(text);
//<head>의 child로 추가
document.head.appendChild(ss);

//id에 접근하여 style 속성을 생성할 수 있다.
document.getElementById("idName").style.color = "red";

//기존에 선언한 style 속성을 덮어쓸 수 있다.
document.getElementById("idName").style.cssText = 'color: blue; background-color: yellow';
  </code></pre>
  
script 태그 내에서 style 태그를 생성하고 속성을 정의할 수 있고 id를 활용해 속성에 접근하고 속성을 추가할 수 있다.

<br>
<br>

위를 활용하여 아래와 같은 예제를 작성할 수 있다.

```html
<head>
</head>
//버튼 클릭 시 색 변화
<button onclick="changeColor()">Click</button>

<script>
function changeColor() {
  var ss = document.createElement("STYLE");
  var text = document.createTextNode("body {color:red;}");
  ss.appendChild(text);
  document.head.appendChild(ss);
}
</script>
```
<br>
<br>
  
```html
<style>
div{
  width: 200px;
  height: 100px;
}
</style>

<script>
var divS = document.querySelector("div");

console.log(divS.style.width); //200px
console.log(divS.style.height); //100px
</script>
```


querySelector를 사용하여 특정 tag에 선언된 style 속성을 가져올 수 있다. 
