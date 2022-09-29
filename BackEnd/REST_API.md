# REST API

## 1. REST 구성

- **자원(RESOURCE)** - URI
- **행위(Verb)** - HTTP METHOD
- **표현(Representations)**

## 2. REST 특징

1. **Uniform (유니폼 인터페이스)**
    
    Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
    
2. **Stateless (무상태성)**
    
    REST는 무상태성 성격, 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않음, 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됨, 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해짐
    
3. **Cacheable (캐시 가능)**
    
    REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능, 따라서 HTTP가 가진 캐싱 기능이 적용 가능, HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능
    
4. **Self-descriptiveness (자체 표현 구조)**
    
    REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것
    
5. **Client - Server 구조**
    
    REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로 간 의존성이 줄어들게 됨
    
6. **계층형 구조**
    
    REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있게 함
    

## 3. REST API 디자인 가이드

1.  REST API 중심 규칙
    1. URI는 정보의 자원을 표현 (리소스명은 동사보다는 명사를 사용)
        
        `GET /members/delete/1`
        
        위 예시는 행위를 표현하는 delete같은 표현이 들어가므로 잘못됨
        
    2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현
        
        `DELETE /members/1` 로 수정 가능
        
        - 회원정보를 가져오는 URI
            
            `GET /members/show/1     (x)`
            
            `GET /members/1          (o)`
            
        - 회원을 추가할 때
            
            `GET /members/insert/2 (x)  - GET 메서드는 리소스 생성에 맞지 않습니다.`
            
            `POST /members/2       (o)`
            
    3. HTTP METHOD의 알맞은 역할
        
        
        | METHOD | 역할 |
        | --- | --- |
        | POST | POST를 통해 해당 URI를 요청하면 리소스를 생성 |
        | GET | GET를 통해 해당 리소스를 조회
        리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져옴 |
        | PUT | PUT를 통해 해당 리소스를 수정 |
        | DELETE | DELETE를 통해 리소스를 삭제 |
2. URI 설계 시 주의할 점
    1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용`http://restapi.example.com/animals/mammals/whales`
    2. URI 마지막 문자로 슬래시(/)를 포함하지 않음
        
        `http://restapi.example.com/houses/apartments/ (X)`
        
    3. 하이픈(-)은 URI 가독성을 높이는데 사용
    4. 밑줄(_)은 URI에 사용하지 않음
    5. URI 경로에는 소문자가 적합
    6. 파일 확장자는 URI에 포함시키지 않음
        
        `http://restapi.example.com/members/soccer/345/photo.jpg (X)`
        
3. 리소스 간의 관계를 표현하는 방법
    
    `/리소스명/리소스 ID/관계가 있는 다른 리소스명`
    
    `ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)`
    
    `GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)`
    
4. 자원을 표현하는 Collection과 Document
    1. Document : 문서, 한 객체
    2. Collection : 문서들의 집합, 객체들의 집합
    
    `http:// restapi.example.com/sports/soccer`
    
    sports라는 Collection과 soccer이라는 Document
    
    `http:// restapi.example.com/sports/soccer/players/13`
    
    sports, players라는 Collection과 soccer, 13이라는 Document로 이뤄진 URI
    

→ 더 직관적인 REST API를 위해 Collection과 Document를 사용할 때 복수, 단수를 지켜줌

1. HTTP 응답 상태 코드
    
    
    | 상태코드 |  |
    | --- | --- |
    | 200 | 클라이언트의 요청을 정상적으로 수행함 |
    | 201 | 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨
    (POST를 통한 리소스 생성 작업 시) |
    | 400 | 클라이언트의 요청이 부적절 할 경우 사용하는 응답 코드 |
    | 401 | 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때 사용하는 응답 코드 |
    | 403 | 유저 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클라이언트가 요청했을 때 사용하는 응답 코드 |
    | 405 | 클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우 사용하는 응답 코드 |
    | 301 | 클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때 사용하는 응답 코드 |
    | 500 | 서버에 문제가 있을 경우 사용하는 응답 코드 |