## Rest 구성
- **자원(Resource)**: URI를 통해 Resource를 정의
- **행위(Verb)**: HTTP Method로 Resource에 대한 행위를 정의
- **표현(Representations)**: JSON, XML 등과 같은 여러가지 언어로 표현이 가능

## Rest Service의 특징
![image](https://user-images.githubusercontent.com/64126100/198790979-4b5ff055-e64e-4a34-973a-48861579ee8f.png)

- 기존 Service는 요청 처리 후에 가공된 data를 이용하여 플랫폼에 적합한 형태의 View로 만들어서 반환하고, Rest service는 View와 상관없이 요청 처리 후 반환될 data가 있다면 JSON이나 XML형식으로 전달한다.
- 기존과 달리 서버는 요청으로 받은 Resource에 대해 순수한 데이터 전송
- GET/POST 외에 PUT, DELETE 방식을 사용해 Resource에 대한 CRUD 처리가 가능

|작업|기존 방식|Rest 방식|비고|
|--|--|--|--|
|Create(Instert) Post|/write.do?id=troment|Post /blog/troment|글쓰기|
|Read(Select) Get|/view.do?id=troment&articleno=25|Get /blog/troment/25|글읽기|
|Update(Update) Post|/modify.do?id=troment|Put /blog/troment|글수정|
|Delete(Delete) Get|/delete.do?id=troment&articleno=25|Delete /blog/troment/25|글삭제|

<br>

- 언더바(_) 대신 하이픈(-)을 사용하고, 특별한 경우가 아니면 대문자 사용을 하지 않으며 URI 마지막에 슬래시(/)를 사용하지 않고, URI는 명사를 사용
- 슬래시(/)로 계층 관계를 나타내고, 확장자가 포함된 파일 이름을 직접 포함시키지 않는다.
- REST API 설정을 위해 객체를 JSON 포맷의 문자열로 변환시켜서 브라우저로 전송하는 jackson-databind 라이브러리와 객체를 xml로 변환하여 브라우저로 전송하는 jackson=dataformat-xml 라이브러리가 있다.

## Rest 관련 Annotation
- @RestController : Controller가 RESTY 방식을 처리하기 위한 것임을 명시
- @ResponseBody : JSP 같은 View로 전달되는 것이 아니라 데이터 자체를 전달
- @PathVariable : URL 경로에 있는 값을 파라미터로 추출
- @CrossOrigin : Ajax의 크로스 도메인 문제를 해결
- @RequestBody : JSON 데이터를 원하는 타입으로 바인딩

