# **📎 Anchor**

**Anchor의 특징**

-   a 태그를 사용하며, 하나의 문서에서 다른 문서로 연결하기 위해 사용한다.
-   태그를 서로 중첩해서 사용할 수 없다.

</br>
 
**Anchor 속성 및 사용법**

-   **href**  
    하이퍼링크를 클릭했을 때 이동할 문서의 URL이나 문서의 책갈피를 지정한다.
-   **target**  
    하이퍼링크를 클릭했을 때 현재 윈도우 또는 새로운 윈도우에서 이동할지 지정한다. _(default는 \_self)_

``` html
<a href="http://www.naver.com">네이버</a>
<a href="http://www.google.com" target="_self">구글</a>
<a href="http://www.daum.com" target="_blank">다음</a>
<!--target 속성은 이 외에도 _parent, _top도 존재, 하지만 잘 사용x-->
```

</br>

**같은 페이지 안에서 이동**

같은 페이지 안에서도 특정 요소 클릭 시 그 위치로 이동하는 것이 가능하다.

![image](https://user-images.githubusercontent.com/59721896/190880681-5b6eca13-fb5c-4318-9e76-51093d5c6741.png)
👉 처음 페이지 로드

</br>

![image](https://user-images.githubusercontent.com/59721896/190880683-e47bfb52-d894-4425-ade1-59b67194b89a.png)
👉 목차에서 내용3 클릭 시 이동 화면

</br>

``` html
<body>
	<h3>목차</h3>
	<ul>
		<li><a href="#content1">내용1</a></li>
		<li><a href="#content2">내용2</a></li>
		<li><a href="#content3">내용3</a></li>
	</ul>
	
	<h3 id="content1">[내용1]</h3>
	<p>긴 내용 ...</p>
	<h3 id="content2">[내용2]</h3>
	<p>긴 내용 ...</p>
	<h3 id="content3">[내용3]</h3>
	<p>긴 내용 ...</p>
</body>
```
