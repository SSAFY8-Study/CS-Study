# **๐ CSV (Comma Separated Values)**

**CSV**

-   ๊ฐ ํญ๋ชฉ์ comma๋ก ๊ตฌ๋ถํด ๋ฐ์ดํฐ๋ฅผ ํํํ๋ค.
-   XML๊ณผ JSON์ ๋นํด ๋ฌธ์ฅ์ด ์งง์ผ๋ฏ๋ก, ๋ง์ ์์ ๋ฐ์ดํฐ ์ ์ก ์ ์ ๋ฆฌํ๋ค.
-   ๊ฐ๊ฐ์ ๋ฐ์ดํฐ๊ฐ ์ด๋ค ๋ด์ฉ์ธ์ง ํ์ํ๊ธฐ ์ด๋ ต๋ค.  
    ๐ _์๋ฒ์ ํด๋ผ์ด์ธํธ๊ฐ '์๋ฒฝํ ๋ฐ์ดํฐ ๊ตฌ์กฐ๋ฅผ ๊ณต์ ํ  ๊ฒฝ์ฐ์๋ง' ๊ฐ์ฅ ๋น ๋ฅผ ์ ์์_

</br>

**CSV ๊ตฌ์กฐ ์์**

``` html
<!--jsp ํ์ผ-->
<%@ page language="java" contentType="text/plain; charset=UTF-8" pageEncoding="UTF-8"%>
1,๊น์คํฌ,A,25
2,ํ์คํฌ,B,26
3,๋ฐ์คํฌ,C,28
```

</br>
</br>

# **๐ XML (eXtensible Markup Language)**

**XML**

-   tag๋ก data๋ฅผ ํํํ๋ค.  
    ๐ tag๋ฅผ ๋ณด๋ฉด ๊ฐ data๊ฐ ๋ฌด์์ ์๋ฏธํ๋์ง ํ์ํ  ์ ์๋ค.
-   tag์ ์ฌ์ฉ์ ์ ์ ์์ฑ์ ๋ฃ์ ์ ์์ผ๋ฏ๋ก ๋ณต์กํ data ์ ๋ฌ์ด ๊ฐ๋ฅํ๋ค.
-   tag๋ฅผ ํฌํจํ๊ธฐ ๋๋ฌธ์ ์ฉ๋์ด ์ปค์ง๋ค๋ ๋จ์ ์ด ์กด์ฌํ๋ค.

</br>

**XML ๊ตฌ์กฐ ์์**

``` html
<!--studentsXML.jsp ํ์ผ-->
<?xml version="1.0" encoding="UTF-8"?>
<%@ page language="java" contentType="text/xml; charset=UTF-8" pageEncoding="UTF-8"%>
<students>
    <student>
        <id>1</id>
        <name>๊น์คํฌ</name>
        <class>A</class>
        <age>25</age>
    </student>
    <student>
        <id>2</id>
        <name>ํ์คํฌ</name>
        <class>B</class>
        <age>26</age>
    </student>
    <student>
        <id>3</id>
        <name>๋ฐ์คํฌ</name>
        <class>C</class>
        <age>28</age>
    </student>
</students>
```

</br>

**XML ํ์์ ๋ฐ์ดํฐ ์ฌ์ฉ ์์ ๊ตฌํ**

![image](https://user-images.githubusercontent.com/59721896/190883934-2744a1c0-3397-464a-a70f-ad38a3c2fe08.png)

-   addEventListenter๋ฅผ ์ฌ์ฉํ์ฌ ๋ฒํผ ํด๋ฆญ ์ด๋ฒคํธ๋ก XML ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ฌ ์ ์๋๋ก ํ๋ค.
-   CSV์ XML์ ๋ชจ๋ ๋ฐ์์ฌ ์ ์๋ response.text()๋ฅผ ์ด์ฉํด์ฃผ์๊ณ ,  
    ๋ฐ์์จ ๋ฐ์ดํฐ๋ฅผ ์ธ์๋ก ๋๊ฒจ makeList ๋ฉ์๋๋ฅผ ์คํํ๋ค.
-   makeList์์๋ ๋ด์ฅ ๊ฐ์ฒด DOMParser๋ฅผ ํ์ฉ, ๋ฐ์์จ .data๋ฅผ XML๋ก ๋ณํํ๋ค.
-   querySelector๋ฅผ ํตํด id๋ฅผ ๋ฐ์์ค๊ณ , ํด๋นํ๋ id์ textContent๋ฅผ ๊ฐ์ ธ์ ์ถ๋ ฅํ๋ค.  
    _๐ ์ฌ๊ธฐ์๋ id, name, class, age๊ฐ ๊ฐ๊ฐ ํ๋์ฉ๋ง ์กด์ฌํ๊ธฐ ๋๋ฌธ์ ๊ทธ๋ฅ querySelector๋ ๊ด์ฐฎ์ง๋ง_  
    _์ฌ๋ฌ ๊ฐ๊ฐ ์กด์ฌํ  ๊ฐ๋ฅ์ฑ๋ ์๊ธฐ ๋๋ฌธ์ ์๋์ ๊ฐ์ด ์ฌ์ฉํ๋ ๊ฒ์ด ๋ ์ ํํ๋ค._  
    _**querySelectorAll("id")\[0\]**_ ํน์ _**getElementsByTagName("id")\[0\]**_

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>XML</title>
    <style type="text/css">
      table {
        width: 300px;
        height: 100px;
      }
      th,
      td {
        text-align: center;
      }
      .first-view-bg {
        background-color: darkgreen;
      }
      .first-view-color {
        color: ivory;
      }
    </style>
  </head>
  <body>
    <h3>ํ์ ์ ๋ณด</h3>
    <button id="listBtn">ํ์ ์ ๋ณด ์กฐํ</button>
    <table style="display: none">
      <tr>
        <th>ํ๋ฒ</th>
        <th>์ด๋ฆ</th>
        <th>๋ถ๋ฐ</th>
        <th>๋์ด</th>
      </tr>
      <tbody id="studentinfo"></tbody>
    </table>
    <script>
      let btn = document.querySelector("#listBtn"); // == document.getElementById("listBtn");
      btn.addEventListener("click", function () {
        // studentsXml.jsp ๋น๋๊ธฐ ํธ์ถ
        fetch("studentsXml.jsp")
            .then((response) => response.text()) // response.text()๋ CSV, XML ๋ชจ๋ ๋ฐ์์ฌ ์ ์์
            .then((data) => makeList(data)) // makeList ํธ์ถ
      });

      function makeList(data) {
        document.querySelector("table").setAttribute("style", "display: ;");
        let tbody = document.querySelector("#studentinfo");
        
        // XML parsing
        let parser = new DOMParser(); // DOMParset ๋ด์ฅ ๊ฐ์ฒด
        const xml = parser.parseFromString(data, "application/xml"); // ์๋ ฅ๋ฐ์ ๋ฐ์ดํฐ๋ฅผ XMLํ์์ผ๋ก ๋ฐ๊ฟ๋ผ!
        
        initTable();
        let students = xml.querySelectorAll("student");
        students.forEach((student) => {
          let tr = document.createElement("tr");

          let idTd = document.createElement("td");
          // id๊ฐ ์ฌ๋ฌ๊ฐ ์์ ๋๋ฅผ ๋๋นํ์ฌ All๋ก ๋ฐ์์จ ๋ค ์ธ๋ฑ์ค๋ก ์ ๊ทผ
          // idTd.appendChild(document.createTextNode(student.querySelectorAll("id")[0].textContent));
          idTd.appendChild(document.createTextNode(student.getElementsByTagName("id")[0].textContent));
          tr.appendChild(idTd);

          let nameTd = document.createElement("td");
          nameTd.appendChild(document.createTextNode(student.querySelector("name").textContent));
          tr.appendChild(nameTd);

          let classTd = document.createElement("td");
          classTd.appendChild(document.createTextNode(student.querySelector("class").textContent));
          tr.appendChild(classTd);

          let gradeTd = document.createElement("td");
          gradeTd.appendChild(document.createTextNode(student.querySelector("age").textContent));
          tr.appendChild(gradeTd);

          tbody.appendChild(tr);
        });
        let first = document.querySelector("tr:first-child");
        first.className = "first-view-bg";
        first.classList.add("first-view-color");
        let odd = document.querySelectorAll("tr:nth-child(even)");
        odd.forEach(function (td) {
          td.setAttribute("style", "background: lightgray;");
        });
      }

      function initTable() {
        let tbody = document.querySelector("#studentinfo");
        let len = tbody.rows.length;
        for (let i = len - 1; i >= 0; i--) {
          tbody.deleteRow(i);
        }
      }
    </script>
  </body>
</html>
```

_(CSV์ ๊ฐ์ง๋ง, CSV์ ๊ฒฝ์ฐ XML ํ์ฑ ๋์  '\\n'์ ','๋ฅผ ๊ธฐ์ค์ผ๋ก ๋ฐ์ดํฐ๋ฅผ ์ฝ๋๋ค๋ ๊ฒ์ด ์ฐจ์ด์ !!_

_๊ฑฐ์ ๋์ผํ๊ธฐ ๋๋ฌธ์ CSV๋ ์์ฑํ์ง ์์)_

</br>
</br>

# **๐ JSON**

**JSON**

-   CSV์ XML์ ๋จ์ ์ ๊ทน๋ณตํ๋ค.
-   JavaScript์์ ์ฌ์ฉํ๋ ๊ฐ์ฒด์ ํ์์ผ๋ก data๋ฅผ ํํํ๋ค.
-   Ajax ์ฌ์ฉ ์ ๊ฑฐ์ ํ์ค์ผ๋ก ์ฌ์ฉํ๋ค.

</br>

**JSON ๊ตฌ์กฐ ์์**

``` html
<!--studentsJSON.jsp ํ์ผ-->
<%@ page language="java" contentType="application/json; charset=UTF-8"
    pageEncoding="UTF-8"%>
[
 {
    "id" : "1",
    "name" : "๊น์คํฌ",
    "class" : "A",
    "grade" : 25
 },
 {
    "id" : "2",
    "name" : "ํ์คํฌ",
    "class" : "B",
    "grade" : 26
 },
 {
    "id" : "3",
    "name" : "๋ฐ์คํฌ",
    "class" : "C",
    "grade" : 28
 }
]
```

</br>

**JSON ํน์ง**

-   ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ  ๋ฐ์ ๋ ์ธ ์ ์๋ ๊ฐ์ฅ ๊ฐ๋จํ ํ์ผ ํฌ๋งท์ด๋ค.
-   ํ์คํธ ๊ธฐ๋ฐ์ผ๋ก ๊ฐ๋ณ๋ค.
-   ์ฝ๊ธฐ ํธํ๋ค.
-   Key์ Value ์์ผ๋ก ๊ตฌ์ฑ๋๋ค.
-   ์๋ฒ์ ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ  ๋ฐ์ ๋ ์ง๋ ฌํ, ์ญ์ง๋ ฌํ๋ฅผ ์ฌ์ฉํ๋ค.
-   ํ๋ก๊ทธ๋จ ์ธ์ด๋ ํ๋ซํผ์ ์๊ด ์์ด ์ฌ์ฉ์ด ๊ฐ๋ฅํ๋ค.

</br>

**์ง๋ ฌํ(serialize)์ ์ญ์ง๋ ฌํ(deserialize)**

์ง๋ ฌํ

-   ๊ฐ์ฒด๋ฅผ ๋ฌธ์์ด๋ก ๋ณํํ๋ ์์์ด๋ค.
-   ํต์  ํ  ๋๋ ๋ฌธ์์ด๋ก ์ง๋ ฌํ ํ์ฌ ์ฃผ๊ณ  ๋ฐ๋ ๊ฒ์ด ์์ ํ๋ค.
-   ์ฌ์ฉ๋ฒ : JSON.stringify(JSON ํ์์ ๊ฐ์ฒด)

์ญ์ง๋ ฌํ

-   ๋ฌธ์์ด์ ๊ฐ์ฒด๋ก ๋ณํํ๋ ์์์ด๋ค.
-   ์๋ฒ๋ก๋ถํฐ ๋ฐ์ ๋ฌธ์์ด์ ๊ฐ์ฒด๋ก ์ญ์ง๋ ฌํ ํ์ฌ ์ฌ์ฉํ๋ค.
-   ์ฌ์ฉ๋ฒ : JSON.parse(JSON ํ์์ ๋ฌธ์์ด)

</br>

**JSON ํ์์ ๋ฐ์ดํฐ ์ฌ์ฉ ์์ ๊ตฌํ**

-   JSON์ ๊ฒฝ์ฐ response.json()์ ํตํด ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ฉด ํจ์ฌ ํธ๋ฆฌํ๋ค.
-   ์ฌ๊ธฐ์๋ student๊ฐ key : value ์ ํ์์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ง ํ๋์ ๊ฐ์ฒด๋ก์ ๋ค์ด์ค๊ธฐ ๋๋ฌธ์  
    querySelector์ ๊ฐ์ ๋ฉ์๋ ๋์ , ๋ฐ๋ก student.id, student.name๊ณผ ๊ฐ์ด ๋ฐ๋ก ๊ฐ์ ์ฐพ์ ์ ์๋ค.

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>JSON</title>
    <style type="text/css">
      table {
        width: 300px;
        height: 100px;
      }
      th,
      td {
        text-align: center;
      }
      .first-view-bg {
        background-color: blueviolet;
      }
      .first-view-color {
        color: ivory;
      }
    </style>
  </head>
  <body>
    <h3>SSAFY ๋ถ๋ฐ</h3>
    <button id="listBtn">ํ์์ ๋ณด๋ณด๊ธฐ</button>
    <table style="display: none">
      <tr>
        <th>ํ๋ฒ</th>
        <th>์ด๋ฆ</th>
        <th>๋ถ๋ฐ</th>
        <th>์ฑ์ </th>
      </tr>
      <tbody id="studentinfo"></tbody>
    </table>
    <script>
      let btn = document.querySelector("#listBtn");
      btn.addEventListener("click", function () {
        // studentsJSON.jsp ๋น๋๊ธฐ ํธ์ถ
        fetch("studentsJSON.jsp")
            .then((response) => response.json()) // CSV, XML๊ณผ์ ์ฐจ์ด์ 
            .then((data) => makeList(data))
      });

      function makeList(data) {
        document.querySelector("table").setAttribute("style", "display: ;");
        let tbody = document.querySelector("#studentinfo");
        initTable();
        data.forEach((student) => {
          let tr = document.createElement("tr");

          let idTd = document.createElement("td");
          idTd.appendChild(document.createTextNode(student.id)); // student๊ฐ ํ๋์ JSON ๊ฐ์ฒด์ด๋ฏ๋ก key๋ฅผ ํตํด ๋ฐ๋ก value๋ฅผ ๋ฐ์์ฌ ์ ์๋ค.
          tr.appendChild(idTd);

          let nameTd = document.createElement("td");
          nameTd.appendChild(document.createTextNode(student.name));
          tr.appendChild(nameTd);

          let classTd = document.createElement("td");
          classTd.appendChild(document.createTextNode(student.["class"])); // [""]์ ๊ฐ์ ํ์์ผ๋ก๋ ๊ฐ๋ฅ
          tr.appendChild(classTd);

          let gradeTd = document.createElement("td");
          gradeTd.appendChild(document.createTextNode(student.grade));
          tr.appendChild(gradeTd);

          tbody.appendChild(tr);
        });
        let first = document.querySelector("tr:first-child");
        first.className = "first-view-bg";
        first.classList.add("first-view-color");
        let odd = document.querySelectorAll("tr:nth-child(even)");
        odd.forEach(function (td) {
          td.setAttribute("style", "background: lightgray;");
        });
      }

      function initTable() {
        let tbody = document.querySelector("#studentinfo");
        let len = tbody.rows.length;
        for (let i = len - 1; i >= 0; i--) {
          tbody.deleteRow(i);
        }
      }
    </script>
  </body>
</html>
```

</br>
</br>

# **๐ ์ ๋ฆฌ**

CSV๋ comma๋ก ๊ตฌ๋ถํ๋ ๋ฌธ์์ด, XML์ ํ๊ทธ๋ก ๋์ด์๋ ๋ฐ์ดํฐ,

JSON์ JavaScript์ ๊ฐ์ฒด๋ก ํ๋กํผํฐ์ ์ด๋ฆ๊ณผ ๊ฐ์ผ๋ก ์ด๋ฃจ์ด์ง๋ค.

</br>

CSV๋ ๋ฐ์ดํฐ ์ฉ๋์ด ๊ฐ์ฅ ์์ง๋ง, ๋ด์ฉ์ ํ์ํ๊ธฐ ์ด๋ ต๋ค๋ ๋จ์ ์ด ์๊ณ ,

XML์ ํ๊ทธ๋ฅผ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ ๋ด์ฉ ํ์๊ณผ ๋ณต์กํ ๋ฐ์ดํฐ ์ ๋ฌ์ ์ ๋ฆฌํ ๋ฐ๋ฉด, ์ฉ๋์ด ๊ฐ์ฅ ํฌ๋ค๋ ๋จ์ ์ด ์๋ค.

JSON์ CSV์ XML์ ๋จ์ ์ ๋ชจ๋ ๊ทน๋ณตํ ๋ฐ์ดํฐ ํ์์ด๋ค.

</br>

CSV์ XML์ ๋ชจ๋ response.text()๋ก ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์จ๋ค๋ ๊ณตํต์ ์ด ์์ง๋ง,

CSV๋ '\\n'์ \\,\\๋ก ๋ฐ์ดํฐ๋ฅผ ๊ตฌ๋ถํ๊ณ , XML์ DOMParser์ ์ฌ์ฉํ์ฌ ๊ตฌ๋ถํ์ฌ ์ฌ์ฉํ๋ค๋ ์ฐจ์ด๊ฐ ์กด์ฌํ๋ค.

JSON์ response.json()์ผ๋ก ๋ฐ์์จ ๋ค, JSON ๊ฐ์ฒด์ ํค๋ฅผ ํตํด ๋ฐ๋ก value๋ฅผ ์ฐพ์ ์ ์๋ค.
