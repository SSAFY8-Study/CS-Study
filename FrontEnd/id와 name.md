# **📎 id**

**input 태그 id 속성 사용 형식**

``` html
<input type="text" id="id">
```

</br>

**JavaScript에서 id 사용 방법**

-   document.all.id.value
-   id.value
-   document.getElementById("폼\_id").value

</br>

**id 속성 특징**

-   page 안에서 중복 사용 불가하며 주로 JavaScript에서 사용하기 위해 지정한다.
-   document.getElementById(id)를 통해서 해당 Element의 Object를 가져온다.
-   id로 설정된 값은 파라미터로서 서버로 보낼 수 없기 때문에 서버에서 접근이 불가하다.

</br>
</br>

# **📎 name**

**input 태그 name 사용 형식**

``` html
<input type="text" name="name">
```

</br>

**JavaScript에서 name 사용 방법**

-   document.폼\_객체명.폼\_원소명.value
-   document.getElementsByName("name")

</br>

**name 속성 특징**

-   page 영역에서 중복 사용 가능하다.  
    👉 같은 name이 여러 개일 때, 배열로 값을 가져올 수 있다.
-   action에 해당하는 페이지에 전달할 수 있는 파라미터로 사용된다.  
    👉 GET/POST 방식으로 전달하고 싶은 태그에 사용한다. (input, radio, checkbox 등)
-   태그의 name 값을 key로 해서 value를 전송한다.  
    👉 request에 값이 전달될 때 Map처럼, key와 value 쌍의 형식으로 데이터가 저장된다.
-   서버 단에서 request.getParameter(parameterName)으로 값을 가져올 수 있다.

</br>
</br>

# **📎 id와 name의 사용**

-   화면을 구성하는 것을 유일하게 식별하여 따로 접근할 때는 id 사용,  
    그룹으로 공통된 것들을 함께 접근하고 싶을 때는 name 사용
-   고유한 식별이 목적이라면 id 사용,  
    form control 요소의 value를 서버로 전송하는 것이 목적일 때는 name 사용

</br>
</br>

참고

-   [https://velog.io/@dongeranguk/input-%ED%83%9C%EA%B7%B8-id%EC%99%80-name%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@dongeranguk/input-%ED%83%9C%EA%B7%B8-id%EC%99%80-name%EC%9D%98-%EC%B0%A8%EC%9D%B4)
-   [https://jhost.tistory.com/54](https://jhost.tistory.com/54)
