# Ajax

## Ajax란

- 언어나 프레임워크가 아닌 구현방식
- 웹에서 화면을 갱신하지 않고 데이터를 서버로부터 가져와서 처리하는 방식
- JavaScript의 XMLHttpRequest객체로 데이터를 전달하고 비동기 방식으로 결과를 조회
- 화면갱신이 없어서 사용자 입장에서 편리 but 동적으로 DOM을 구성해야 하므로 구현이 복잡
- data입력 → event발생 → 서버에서 처리한후 text, xml 또는 json으로 응답 → 브라우저에서 응답 data를 이용하여 화면 전환없이 현재 페이지에서 동적으로 화면을 재구성

## fetch() 이용 방식

```jsx
fetch("https://jsonplaceholder.typicode.com/posts", option)
   .then(res => res.text())
   .then(text => console.log(text));
```

1. fetch에는 기본적으로 첫번째 인자를 요청할 url이 들어감
2. 기본적으로 http메서드중 GET으로 동작
3. fetch를 통해 ajax를 호출 시 해당 주소에 요청을 보낸 다음, 응답 객체를 받음
4. 첫번째 then에서 그 응답을 받고, res.text()메서드로 파싱한 text값을 리턴
5. 그 다음 then에서 리턴받은 text값을 받고, 원하는 처리 가능

## response와 메서드

fetch를 통해 요청을 하고 서버로부터 값을 받으면 .then을 통해 함수의 인자에 response가 담기는데, 여러 정보를 담고 있고 필요한 변수나 메서드를 뽑아내서 값을 얻을 수 있다. 

→ API 호출이 실패하면 error객체를 reject함

- response.status - HTTP 상태 코드
- response.ok - HTTP 상태 코드가 200과 299사이일 경우 true
- response.body - 내용
- response.text() - 응답을 읽고 텍스트를 반환
- response.json() - 응답을 JSON으로 파싱
- response.formData() - 응답을 FormData객체로 반환
- response.blob() - 응답을 Blob(타입이 있는 바이너리 데이터)로 반환
- response.arrayBuffer() - 응답을 ArrayBuffer로 반환
- 응답 자료 형태 반환 메서드는 한번만 사용 가능 → response.text()를 사용해 응답을 얻었으면 뒤에 또 response.json()을 써도 동작 X
    
    ### async/await
    
    - await는 Promise객체를 리턴하는 부분 앞에만 붙일 수 있음
    - await는 비동기 작업의 결과값을 얻을 때 까지 기다려줌
    - await를 사용하려면 그 함수에는 반드시 async키워드가 붙어 있어야 함

## fetch API

1. GET : 존재하는 자원을 요청
    1. 단순히 원격 API에 있는 데이터를 가져올 때 쓰임
    2. fetch는 디폴트로 GET으로 작동
    3. 응답 response는 json()메서드를 제공 
2. POST : 새로운 자원을 요청
    1. 폼 등을 사용해서 데이터를 만들어 낼 때, 데이터의 양이 많거나 비밀번호 등 개인정보를 보낼 때 사용
    2. method를 POST로 지정해주고, header에 JSON사용 여부 설정
    3. body에 요청 data를 JSON형식으로 stringify하여 설정
    
    ```jsx
    fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST", // POST
      headers: { // 헤더 조작
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ // 자바스크립트 객체를 json화 한다.
        title: "test",
        body: "just testing",
        userId: 1,
      }),
    })
      .then((response) => response.json())
      .then((data) => console.log(data))
    ```
    
3. PUT : 존재하는 자원 변경 요청
    1. POST와 거의 비슷
    2. 아예 전체를 body의 데이터로 교체, 일부분만 보내는 경우 나머지는 default값으로 수정되므로 바뀌지 않는 속성도 모두 보내야 함 !
4. PATCH : 존재하는 자원 일부 변경 요청
    1. body의 데이터와 알맞는 일부만 교체, 일부분만 보내도 됨
5. DELETE : 존재하는 자원 일부 변경 요청
    1. 보낼 데이터가 없기 때문에 header, body 필요 X