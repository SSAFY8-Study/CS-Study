# **๐ id**

**input ํ๊ทธ id ์์ฑ ์ฌ์ฉ ํ์**

``` html
<input type="text" id="id">
```

</br>

**JavaScript์์ id ์ฌ์ฉ ๋ฐฉ๋ฒ**

-   document.all.id.value
-   id.value
-   document.getElementById("ํผ\_id").value

</br>

**id ์์ฑ ํน์ง**

-   page ์์์ ์ค๋ณต ์ฌ์ฉ ๋ถ๊ฐํ๋ฉฐ ์ฃผ๋ก JavaScript์์ ์ฌ์ฉํ๊ธฐ ์ํด ์ง์ ํ๋ค.
-   document.getElementById(id)๋ฅผ ํตํด์ ํด๋น Element์ Object๋ฅผ ๊ฐ์ ธ์จ๋ค.
-   id๋ก ์ค์ ๋ ๊ฐ์ ํ๋ผ๋ฏธํฐ๋ก์ ์๋ฒ๋ก ๋ณด๋ผ ์ ์๊ธฐ ๋๋ฌธ์ ์๋ฒ์์ ์ ๊ทผ์ด ๋ถ๊ฐํ๋ค.

</br>
</br>

# **๐ name**

**input ํ๊ทธ name ์ฌ์ฉ ํ์**

``` html
<input type="text" name="name">
```

</br>

**JavaScript์์ name ์ฌ์ฉ ๋ฐฉ๋ฒ**

-   document.ํผ\_๊ฐ์ฒด๋ช.ํผ\_์์๋ช.value
-   document.getElementsByName("name")

</br>

**name ์์ฑ ํน์ง**

-   page ์์ญ์์ ์ค๋ณต ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.  
    ๐ ๊ฐ์ name์ด ์ฌ๋ฌ ๊ฐ์ผ ๋, ๋ฐฐ์ด๋ก ๊ฐ์ ๊ฐ์ ธ์ฌ ์ ์๋ค.
-   action์ ํด๋นํ๋ ํ์ด์ง์ ์ ๋ฌํ  ์ ์๋ ํ๋ผ๋ฏธํฐ๋ก ์ฌ์ฉ๋๋ค.  
    ๐ GET/POST ๋ฐฉ์์ผ๋ก ์ ๋ฌํ๊ณ  ์ถ์ ํ๊ทธ์ ์ฌ์ฉํ๋ค. (input, radio, checkbox ๋ฑ)
-   ํ๊ทธ์ name ๊ฐ์ key๋ก ํด์ value๋ฅผ ์ ์กํ๋ค.  
    ๐ request์ ๊ฐ์ด ์ ๋ฌ๋  ๋ Map์ฒ๋ผ, key์ value ์์ ํ์์ผ๋ก ๋ฐ์ดํฐ๊ฐ ์ ์ฅ๋๋ค.
-   ์๋ฒ ๋จ์์ request.getParameter(parameterName)์ผ๋ก ๊ฐ์ ๊ฐ์ ธ์ฌ ์ ์๋ค.

</br>
</br>

# **๐ id์ name์ ์ฌ์ฉ**

-   ํ๋ฉด์ ๊ตฌ์ฑํ๋ ๊ฒ์ ์ ์ผํ๊ฒ ์๋ณํ์ฌ ๋ฐ๋ก ์ ๊ทผํ  ๋๋ id ์ฌ์ฉ,  
    ๊ทธ๋ฃน์ผ๋ก ๊ณตํต๋ ๊ฒ๋ค์ ํจ๊ป ์ ๊ทผํ๊ณ  ์ถ์ ๋๋ name ์ฌ์ฉ
-   ๊ณ ์ ํ ์๋ณ์ด ๋ชฉ์ ์ด๋ผ๋ฉด id ์ฌ์ฉ,  
    form control ์์์ value๋ฅผ ์๋ฒ๋ก ์ ์กํ๋ ๊ฒ์ด ๋ชฉ์ ์ผ ๋๋ name ์ฌ์ฉ

</br>
</br>

์ฐธ๊ณ 

-   [https://velog.io/@dongeranguk/input-%ED%83%9C%EA%B7%B8-id%EC%99%80-name%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@dongeranguk/input-%ED%83%9C%EA%B7%B8-id%EC%99%80-name%EC%9D%98-%EC%B0%A8%EC%9D%B4)
-   [https://jhost.tistory.com/54](https://jhost.tistory.com/54)
