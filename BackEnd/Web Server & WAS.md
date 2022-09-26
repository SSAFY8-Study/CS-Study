![image](https://user-images.githubusercontent.com/64126100/191742143-bed07876-68e5-488e-8a04-fe4ab1786dcb.png)
## Web Server

**개념**
- 웹 브라우저 클라이언트로부터 HTTP 요청을 받아들이고 HTML 문서와 같은 웹페이지를 반환하는 컴퓨터 프로그램
- 하드웨어(Web Server가 설치된 컴퓨터)와 소프트웨어(웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램)으로 구분된다.

**기능 및 예시**
- HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당
- 사용자가 웹 브라우저에서 페이지 요청을 하면 요청을 받아 WAS를 거치지 않고 바로 정적인 컨텐츠를 제공하는 역할
- 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 덜어줌
- 동적인 컨텐츠(Servlet 등)를 제공해야 할 때는 웹 브라우저의 요청을 WAS에 보내고, WAS가 처리한 결과물을 클라이언트에게 다시 전달
- 대표적인 예로는 Apache Server, Nginx, IIS(Windows 전용 Web 서버)가 있다.
<br>

## WAS (Web Application Server)

**개념**
- 데이터베이스 조회나 다양한 Logic 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
- HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)
- Web Container 또는 Servlet Container라고도 불리며, JSP와 Servlet 구동 환경을 제공
- 요청에 맞는 데이터를 데이터베이스를 통해 불러오고, Business Logic에 맞게 결과물을 생성하여 제공함으로써 자원을 효율적으로 사용

**기능 및 예시**
- 프로그램의 실행 환경과 데이터베이스 접속 기능을 제공
- 여러 개의 transaction(논리적인 작업 단위) 관리 기능 제공
- 작업을 수행하는 Business Logic을 수행
- 대표적인 예로는 Tomcat, JBoss, Jeus, Web Sphere 등이 있다.
<br>

## Web Server 와 WAS 기능을 구분하는 이유
- WAS가 동적 컨텐츠와 정적 컨텐츠 요청까지 모두 처리하게 된다면 부하가 커지면서, 동적 컨텐츠의 처리가 지연되어 수행 속도가 느려져 페이지 노출 시간이 증가하게 된다.
- 정적인 컨텐츠는 Web Server에서 제공하도록 기능을 분리하여 서버의 부하를 방지한다.
- SSL(Secure Sockets Layer, 브라우저와 서버 사이의 암호와된 연결을 수립하는데 사용)에 대한 암복호화(암호화: 평문을 암호문으로 변환, 복호화: 암호문을 평문으로 변환) 처리에 Web Server를 사용하도록 물리적으로 분리하여 보안 강화
- WAS에서 오류가 발생했을 때, 사전의 Web Server에서 오류가 발생한 WAS의 이용을 제한하고, WAS를 재시작하여 사용자가 오류를 느끼지 못하고 이용할 수 있도록 도와줌
- Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인(표준 기능을 확장해주는 것을 의미) 형태로 구성하면 더욱 효율적인 분산 처리가 가능
<br>

## Web Service 구조

**가질 수 있는 구조 형태**
- 클라이언트(User) -> Web Server -> DB
- 클라이언트(User) -> WAS -> DB
- 클라이언트(User) -> Web Server -> WAS -> DB

**대표적인 동작 과정 (User -> Web Server -> WAS -> DB)**
1. Web Server는 웹 브라우저로부터 HTTP 요청을 받는다.
2. Web Server는 클라이언트의 요청을 WAS에 전달한다.
3. WAS는 관련된 Servlet을 메모리에 올린다.
4. WAS는 web.xml을 참조해 Servlet에 대한 Thread(프로세스 내에서 실제로 작업을 수행하는 주체)를 생성한다.
5. HttpServletRequest와 HttpServletResponse 객체를 생성해 Servlet에 전달하고, Thread는 Servlet의 service()를 호출, service()는 요청에 맞는 doGet() 또는 doPost() 호출한다.
6. doGet() 또는 doPost()는 인자에 맞게 생성된 동적 페이지를 Response 객체 형태로 WAS에 전달한다.
7. WAS는 Response 객체를 HttpResponse 형태로 변환하여 Web Server에 전달한다.
8. 생성된 Thread를 종료하고, 생성했던 HttpServletRequest, HttpServletResponse 객체를 제거하고 과정을 종료한다.
