# **📎 Form**

**Form의 개념 및 역할**

-   사용자로부터 데이터를 입력받아 서버에서 처리하기 위하여 사용
-   사용자의 요청에 따라 서버는 HTML form을 전달
-   사용자는 HTML form에 적절한 데이터 입력 후 서버로 전송함 (submit)
-   서버는 사용자의 요청 분석 후 데이터를 등록하거나, 원하는 데이터를 조회하여 결과를 반환함

👉 Form은 **_데이터를 받고, 보낼 수 있는 양식_**

</br>

**Form 작성**

``` html
<form [속성="속성값"]> form control </form>
```

</br>
</br>

# **📎 form control 요소**

**form control이란?**

-   사용자가 입력하는 control 요소들은 모두 <form> 태그의 하위에 위치해야만 서버로 전송된다.
-   각 control 요소마다 텍스트 입력, 버튼 클릭 등 다양한 형식으로 입력받을 수 있다.

| **tag** | **설명** |
| --- | --- |
| **form** | 사용자에게 입력 받을 항목을 정의, form tag 내부에 여러 개의 control 요소를 포함 |
| **inpuT** | 텍스트 box, 체크 box, 라디오 버튼 등 사용자가 데이터를 입력할 수 있도록 함 |
| **textare** | 여러 줄의 문자를 입력할 수 있도록 함 |
| **button** | 버튼을 표시 |
| **select** | select box(dropdown, combobox)를 표시 |
| **optgroup** | select box의 각 항목들을 그룹화 |
| **label** | 마우스를 이용하여 input tag 항목 선택 시 편리함을 제공, for 속성을 이용하여 다른 control 요소와 텍스를 연결시켜서 더 편리하게 선택할 수 있도록 함 |
| **fieldset** | 입력 항목들을 그룹화 |
| **legend** | fieldset tag의 제목을 지정 |

_👉 <form> 태그는 입력받을 요소들을 담는 하나의 양식을 의미, 나머지 태그들은 그 양식을 구성하는 입력 도구!_

</br>
</br>

# **📎 데이터 전송을 위한 속성**

**form에서 서버로 데이터를 보낼 때 필요한 속성들**

-   사용자가 입력한 자료들을 어떤 방식으로 서버로 전달할 것인지 결정
-   서버에서 어떤 프로그램을 이용해 처리할 것인지 결정

| **속성** | **설명** |
| --- | --- |
| **method** | 사용자가 입력한 내용을 서버 쪽 프로그램으로 어떻게 넘겨줄지 지정함 |
| 속성값 | **GET** 주소 표시줄에 사용자가 입력한 내용이 표시되며, 전송 내용 길이 제한이 있음 |
|| **POST** 전송 내용 길이에 제한이 없으며, 사용자가 입력한 내용이 표시되지 않음 |
| **name** | form의 이름을 지정. 한 문서 안에 여러 개의 <form> 태그가 있을 경우, 구분자로 사용함 |
| **action** | <form> 태그 안의 내용들을 처리해 줄 서버상의 프로그램을 지정함 (URL) |
| **target** | <action> 태그에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정함 |
| **autocomplete** | 자동완성 기능으로, 기본값은 on |

</br>

**GET과 POST 차이점**

-   GET은 HTTP 메시지의 header 영역에 담아 전송하기 때문에  
    전송 길이 제한(256~204bytes)이 있고, 주소에 데이터가 노출된다.
-   POST는 HTTP 메시지의 body 영역에 담아 전송하기 때문에 내부적으로 IO가 일어난다.  
    따라서 전송 내용의 길이에 제한이 없고, 사용자가 입력한 정보가 주소에 표시되지 않는다.

</br>

**언제 GET or POST를 사용해야 할까?**

-   **POST**  
    페이지 단위의 많은 양의 데이터 전송, 혹은 보안이 필요한 정보를 전송할 때
-   **GET**  
    짧은 양의 데이터, 혹은 노출되어도 상관없는 정보를 전송할 때  
    _(GET의 길이 제한을 초과하는 데이터 전송이 불가한 것은 아니지만, 짤려서 전송됨)_

</br>

**page 이동 시 GET과 POST 구분 방법**

[ page 이동의 세 가지 방법 ]

1.  주소 표시줄 입력
2.  a태그를 이용한 link 이동
3.  form을 이용한 이동 (GET, POST 방식)

여기서 1, 2번 및 3번의 GET 방식 전송은 모두 GET이고, 유일하게 3번의 form을 이용한 POST 방식 전송만이 POST이다.

**_👉 POST라고 명시하지 않으면 모두 GET이라고 생각하면 된다._**

</br>
</br>

# **📎 Form 작성 예시**

**form 예시 페이지 및 코드**

![image](https://user-images.githubusercontent.com/59721896/190871640-9c9174a8-c530-4269-a69a-75c037e9350c.png)

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>회원가입</title>
  </head>
  <body>
    <h1>회원가입</h1>
    <form method="POST" action="register.jsp">
	    <fieldset>
	      <legend>사용자 정보</legend>
	      	<label for="id">아이디 </label>
	      		<input type="text" placeholder="필수 입력" id="id" required/></br>
	        <label for="password">비밀번호 </label>
	        	<input type="password" placeholder="필수 입력" id="pass" required/></br>
	        <label>성별 </label>
	        	남<input type="radio" name="sex"/>
	        	여<input type="radio" name="sex"/></br>
	        <label>관심분야 </label>
	        	<input type="checkbox" name="sub"/>영화 
	        	<input type="checkbox" name="sub"/>음악 
	        	<input type="checkbox" name="sub"/>미술 </br>
	        <label>상태메시지</label></br>
	        <textarea cols="30" rows="5"></textarea></br>
	        <input type="submit" value="등록">
            <input type="reset" value="초기화">
	    </fieldset>
    </form>
  </body>
</html>
```

</br>
</br>

# **📎 Form 이벤트**

**이벤트란?**

-   웹 페이지에서 여러 상호작용이 있을 때마다 발생
-   마우스 클릭 혹은 키보드를 눌렀을 때와 같이 다양한 종류의 이벤트 존재  
    _(웹 페이지 로딩, 페이지 스크롤, 브라우저 창 크기 조절, 마우스 클릭, Form submit 등)_
-   JavaScript를 사용하여 DOM에서 발생하는 이벤트 감지, 이벤트에 대응하는 여러 작업 수행
-   이벤트는 일반적으로 함수와 연결, 이벤트 발생 시 함수 실행 (**이벤트 핸들러** 혹은 **이벤트 리스너**라고 부름)

</br>

**Form 이벤트**

-   form이 전송될 때는 submit 이벤트, 초기화할 때는 reset 이벤트 발생
-   submit과 reset은 이벤트 핸들러에서 취소할 수도 있음

| **이벤트** | **설명** |
| --- | --- |
| **onsubmit** | form이 전송될 때 발생 |
| **onreset** | 입력 form이 reset될 때 발생 |
| **oninput** | input 또는 textarea의 값이 변경되었을 때 발생 |
| **onchange** | select box, check box, radio button의 상태가 변경되었을 때 발생 |
| **onfocus(focusin)** | input과 같은 요소에 입력 포커스가 들어올 때 발생 |
| **onblur(focusout)** | input과 같은 요소 등에서 포커스가 다른 곳으로 이동할 때 발생 |
| **onselect** | input, textarea에 입력 값 중 일부가 마우스 등으로 선택될 때 발생 |

</br>

**Form 이벤트를 처리하는 이벤트 핸들러 구현**

1️⃣ 인라인 이벤트 핸들러 방식

``` html
<form method="POST" action="ok.html" onsubmit="javascript:event.preventDefault();alert('안녕');">
```

-   위에서 구현했던 예시의 form 태그 안에서 onsubmit 속성을 활용했다.
-   onsubmit 안에 JavaScript를 작성해주었다.

_**👉 event.preventDefault()**_

submit되는 순간 페이지가 리로드 되는 것을 막기 위한 메소드!

</br>

2️⃣ 이벤트 핸들러 프로퍼티 방식

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>회원가입</title>
  </head>
  <body>
    <h1>회원가입</h1>
    <form method="POST" action="ok.html" id="register">
	    <fieldset>
	      <legend>사용자 정보</legend>
	      	<label for="id" onsubmit="javascript:alert('id');">아이디 </label>
	      		<input type="text" placeholder="필수 입력" id="id" required/></br>
	        <label for="password">비밀번호 </label>
	        	<input type="password" placeholder="필수 입력" id="pass" required/></br>
	        <label>성별 </label>
	        	남<input type="radio" name="sex"/>
	        	여<input type="radio" name="sex"/></br>
	        <label>관심분야 </label>
	        	<input type="checkbox" name="sub"/>영화 
	        	<input type="checkbox" name="sub"/>음악 
	        	<input type="checkbox" name="sub"/>미술 </br>
	        <label>상태메시지</label></br>
	        <textarea cols="30" rows="5"></textarea></br>
	        <input type="submit" value="등록">
	        <input type="reset" value="초기화">
	    </fieldset>
    </form>
  </body>
  <script>
  	var f = document.getElementById("register")
  	f.onsubmit = function submitFunc() {
  		if(document.getElementById('id').value != "seolhee") {
  			alert("id를 'seolhee'라고 입력해주세요.");
  	  		return false;
  		}
  	}
  </script>
</html>
```

-   form에 id를 지정하고, HTML에서 id값을 통해 이벤트 대상이 될 DOM을 선택했다.
-   해당 DOM에 이벤트 핸들러(submitFunc())를 등록하고, onsubmit이 발생하면 함수가 실행되도록 했다.

</br>

3️⃣ addEventListener 메소드 방식

``` html
<script>
  	var f = document.getElementById("register")
  	function submitFunc1() {
  		if(document.getElementById('id').value != "seolhee") {
  			alert("id를 'seolhee'라고 입력해주세요.");
  	  		return false;
  		}
  	}
  	function submitFunc2() {
  		if(document.getElementById('id').value != "seolhee") {
  			alert("id를 'seolhee2'라고 입력해주세요.");
  	  		return false;
  		}
  	}
    	// document.addEventListener(이벤트, 메소드, 캡쳐링 여부)
  	f.addEventListener("submit", submitFunc1, false); // 마지막 인자값 생략 가능
  	f.addEventListener("submit", submitFunc2, false); // 마지막 인자값 생략 가능
  </script>
```

-   나머지는 위의 이벤트 핸들러 프로퍼티 방식과 같고, JavaScript 코드 부분만 변경했다.
-   addEventListener의 특성을 담기 위해 하나의 이벤트에 두 개의 이벤트 핸들러를 작성했다.
-   id를 통해 DOM을 선택하고, 이벤트 핸들러 메서드를 작성하여 해당 DOM에 각각 추가했다.

</br>

_✔️ 어떤 이벤트 핸들러를 사용해야 할까?_

| **이벤트 핸들러** | **장점** | **단점** |
| --- | --- | --- |
| **인라인 이벤트 핸들러** | 여러 개의 메소드 한 번에 호출 가능 | HTML 코드를 JavaScript가 침범 |
| **이벤트 핸들러 프로퍼티** | HTML 코드와 JavaScript 코드 분리 가능 | 이벤트 핸들러 프로퍼티에</br>하나의 이벤트 핸들러만을</br>바인딩할 수 있음</br>(마지막에 바인딩된 메소드만 실행됨)|
| **addEventListener** |\- addEventListener의 인자를 통해 좀 더 세밀한 이벤트 제어 가능</br>\- 하나의 이벤트에 대해 하나 이상의 이벤트 핸들러 추가 가능</br>\- 캡쳐링과 버블링 지원</br>\- HTML뿐 아니라 모든 DOM(HTML, XML, SVG)에 대해 동작</br>\-인라인 이벤트 핸들러와 이벤트 핸들러 프로퍼티의 단점 극복 |  |

👉 addEventListener를 사용하는 것이 유리

</br>
</br>

# **🌟 정리**

form 태그는 사용자로부터 데이터를 입력받고, 서버로 보내주는 역할을 한다.

submit을 통해 데이터를 보내고, 이벤트 핸들러를 작성하여 이벤트 처리가 가능하다.

이벤트 핸들러는 addEventListener를 활용하자.
