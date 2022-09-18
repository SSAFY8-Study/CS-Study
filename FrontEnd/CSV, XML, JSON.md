# **📎 CSV (Comma Separated Values)**

**CSV**

-   각 항목을 comma로 구분해 데이터를 표현한다.
-   XML과 JSON에 비해 문장이 짧으므로, 많은 양의 데이터 전송 시 유리하다.
-   각각의 데이터가 어떤 내용인지 파악하기 어렵다.  
    👉 _서버와 클라이언트가 '완벽히 데이터 구조를 공유할 경우에만' 가장 빠를 수 있음_

</br>

**CSV 구조 예시**

``` html
<!--jsp 파일-->
<%@ page language="java" contentType="text/plain; charset=UTF-8" pageEncoding="UTF-8"%>
1,김설희,A,25
2,홍설희,B,26
3,박설희,C,28
```

</br>
</br>

# **📎 XML (eXtensible Markup Language)**

**XML**

-   tag로 data를 표현한다.  
    👉 tag를 보면 각 data가 무엇을 의미하는지 파악할 수 있다.
-   tag에 사용자 정의 속성을 넣을 수 있으므로 복잡한 data 전달이 가능하다.
-   tag를 포함하기 때문에 용량이 커진다는 단점이 존재한다.

</br>

**XML 구조 예시**

``` html
<!--studentsXML.jsp 파일-->
<?xml version="1.0" encoding="UTF-8"?>
<%@ page language="java" contentType="text/xml; charset=UTF-8" pageEncoding="UTF-8"%>
<students>
    <student>
        <id>1</id>
        <name>김설희</name>
        <class>A</class>
        <age>25</age>
    </student>
    <student>
        <id>2</id>
        <name>홍설희</name>
        <class>B</class>
        <age>26</age>
    </student>
    <student>
        <id>3</id>
        <name>박설희</name>
        <class>C</class>
        <age>28</age>
    </student>
</students>
```

</br>

**XML 형식의 데이터 사용 예시 구현**

![image](https://user-images.githubusercontent.com/59721896/190883934-2744a1c0-3397-464a-a70f-ad38a3c2fe08.png)

-   addEventListenter를 사용하여 버튼 클릭 이벤트로 XML 데이터를 가져올 수 있도록 했다.
-   CSV와 XML을 모두 받아올 수 있는 response.text()를 이용해주었고,  
    받아온 데이터를 인자로 넘겨 makeList 메소드를 실행했다.
-   makeList에서는 내장 객체 DOMParser를 활용, 받아온 .data를 XML로 변환했다.
-   querySelector를 통해 id를 받아오고, 해당하는 id의 textContent를 가져와 출력했다.  
    _👉 여기서는 id, name, class, age가 각각 하나씩만 존재하기 때문에 그냥 querySelector도 괜찮지만_  
    _여러 개가 존재할 가능성도 있기 때문에 아래와 같이 사용하는 것이 더 정확하다._  
    _**querySelectorAll("id")\[0\]**_ 혹은 _**getElementsByTagName("id")\[0\]**_

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
    <h3>학생 정보</h3>
    <button id="listBtn">학생 정보 조회</button>
    <table style="display: none">
      <tr>
        <th>학번</th>
        <th>이름</th>
        <th>분반</th>
        <th>나이</th>
      </tr>
      <tbody id="studentinfo"></tbody>
    </table>
    <script>
      let btn = document.querySelector("#listBtn"); // == document.getElementById("listBtn");
      btn.addEventListener("click", function () {
        // studentsXml.jsp 비동기 호출
        fetch("studentsXml.jsp")
            .then((response) => response.text()) // response.text()는 CSV, XML 모두 받아올 수 있음
            .then((data) => makeList(data)) // makeList 호출
      });

      function makeList(data) {
        document.querySelector("table").setAttribute("style", "display: ;");
        let tbody = document.querySelector("#studentinfo");
        
        // XML parsing
        let parser = new DOMParser(); // DOMParset 내장 객체
        const xml = parser.parseFromString(data, "application/xml"); // 입력받은 데이터를 XML형식으로 바꿔라!
        
        initTable();
        let students = xml.querySelectorAll("student");
        students.forEach((student) => {
          let tr = document.createElement("tr");

          let idTd = document.createElement("td");
          // id가 여러개 있을 때를 대비하여 All로 받아온 뒤 인덱스로 접근
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

_(CSV와 같지만, CSV의 경우 XML 파싱 대신 '\\n'와 ','를 기준으로 데이터를 읽는다는 것이 차이점!!_

_거의 동일하기 때문에 CSV는 작성하지 않음)_

</br>
</br>

# **📎 JSON**

**JSON**

-   CSV와 XML의 단점을 극복했다.
-   JavaScript에서 사용하는 객체의 형식으로 data를 표현한다.
-   Ajax 사용 시 거의 표준으로 사용한다.

</br>

**JSON 구조 예시**

``` html
<!--studentsJSON.jsp 파일-->
<%@ page language="java" contentType="application/json; charset=UTF-8"
    pageEncoding="UTF-8"%>
[
 {
    "id" : "1",
    "name" : "김설희",
    "class" : "A",
    "grade" : 25
 },
 {
    "id" : "2",
    "name" : "홍설희",
    "class" : "B",
    "grade" : 26
 },
 {
    "id" : "3",
    "name" : "박설희",
    "class" : "C",
    "grade" : 28
 }
]
```

</br>

**JSON 특징**

-   데이터를 주고 받을 때 쓸 수 있는 가장 간단한 파일 포맷이다.
-   텍스트 기반으로 가볍다.
-   읽기 편하다.
-   Key와 Value 쌍으로 구성된다.
-   서버와 데이터를 주고 받을 때 직렬화, 역직렬화를 사용한다.
-   프로그램 언어나 플랫폼에 상관 없이 사용이 가능하다.

</br>

**직렬화(serialize)와 역직렬화(deserialize)**

직렬화

-   객체를 문자열로 변환하는 작업이다.
-   통신 할 때는 문자열로 직렬화 하여 주고 받는 것이 안전하다.
-   사용법 : JSON.stringify(JSON 형식의 객체)

역직렬화

-   문자열을 객체로 변환하는 작업이다.
-   서버로부터 받은 문자열은 객체로 역직렬화 하여 사용한다.
-   사용법 : JSON.parse(JSON 형식의 문자열)

</br>

**JSON 형식의 데이터 사용 예시 구현**

-   JSON의 경우 response.json()을 통해 데이터를 받아오면 훨씬 편리하다.
-   여기서는 student가 key : value 쌍 형식의 데이터를 가진 하나의 객체로서 들어오기 때문에  
    querySelector와 같은 메서드 대신, 바로 student.id, student.name과 같이 바로 값을 찾을 수 있다.

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
    <h3>SSAFY 분반</h3>
    <button id="listBtn">학생정보보기</button>
    <table style="display: none">
      <tr>
        <th>학번</th>
        <th>이름</th>
        <th>분반</th>
        <th>성적</th>
      </tr>
      <tbody id="studentinfo"></tbody>
    </table>
    <script>
      let btn = document.querySelector("#listBtn");
      btn.addEventListener("click", function () {
        // studentsJSON.jsp 비동기 호출
        fetch("studentsJSON.jsp")
            .then((response) => response.json()) // CSV, XML과의 차이점
            .then((data) => makeList(data))
      });

      function makeList(data) {
        document.querySelector("table").setAttribute("style", "display: ;");
        let tbody = document.querySelector("#studentinfo");
        initTable();
        data.forEach((student) => {
          let tr = document.createElement("tr");

          let idTd = document.createElement("td");
          idTd.appendChild(document.createTextNode(student.id)); // student가 하나의 JSON 객체이므로 key를 통해 바로 value를 받아올 수 있다.
          tr.appendChild(idTd);

          let nameTd = document.createElement("td");
          nameTd.appendChild(document.createTextNode(student.name));
          tr.appendChild(nameTd);

          let classTd = document.createElement("td");
          classTd.appendChild(document.createTextNode(student.["class"])); // [""]와 같은 형식으로도 가능
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

# **🌟 정리**

CSV는 comma로 구분하는 문자열, XML은 태그로 되어있는 데이터,

JSON은 JavaScript의 객체로 프로퍼티의 이름과 값으로 이루어진다.

</br>

CSV는 데이터 용량이 가장 작지만, 내용을 파악하기 어렵다는 단점이 있고,

XML은 태그를 사용하기 때문에 내용 파악과 복잡한 데이터 전달에 유리한 반면, 용량이 가장 크다는 단점이 있다.

JSON은 CSV와 XML의 단점을 모두 극복한 데이터 형식이다.

</br>

CSV와 XML은 모두 response.text()로 데이터를 받아온다는 공통점이 있지만,

CSV는 '\\n'와 \\,\\로 데이터를 구분하고, XML은 DOMParser을 사용하여 구분하여 사용한다는 차이가 존재한다.

JSON은 response.json()으로 받아온 뒤, JSON 객체의 키를 통해 바로 value를 찾을 수 있다.
