# HTTP/HTTPS

# HTTP란

HTTP(Hyper Text Transfer Protocol)란 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜, 서로 다른 시스템들 사이에서 통신을 주고받게 해주는 가장 기초적인 포로토콜이다.

# HTTP의 구조

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkdJ4Q%2FbtqK6AXLEtC%2FjBZzMuJBWzdLYmqILo5Ri1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkdJ4Q%2FbtqK6AXLEtC%2FjBZzMuJBWzdLYmqILo5Ri1%2Fimg.png)

HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP위에서 작동. Stateless 프로토콜이며, Method, Path, Header, Body등으로 구성됨.

![https://blog.wishket.com/wp-content/uploads/2020/02/03-3.png](https://blog.wishket.com/wp-content/uploads/2020/02/03-3.png)

HTTP는 암호화가 되지 않은 평문 데이터를 전송 → HTTP로 비밀번호나 주민등록번호 등을 주고 받으면 제3자에 노출 가능성 → HTTPS의 등장

# HTTPS란

HTTPS(Hyper Text Tranfer Protocol Secure)란 일반적인 HTTP의 문제점인 서버에서부터 브라우저로 전송되는 정보가 암호화되지 문제점을 TLS(Transport Layer Security)을 사용함으로써 해결 → TLS은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들게 도와주고, 민감한 정보를 주고받을 때 도난을 방지

# TLS/SSL

- TLS(Transport Layer Security)은 HTTPS에서 사용하는 암호화 프로토콜로 이전에는 SSL(Secure Sockets Layer)로 알려져 있었음
- 비대칭 공개 키 구조
    - 개인키 : 개인키는 공개키로 암호화된 정보를 복호화하는데 사용
    - 공개키 : 공개키는 안전한 방식으로 서버와 상호 작용하는 모든 사람이 사용 가능, 공개키로 암호화된 정보는 개인키로만 복호화 가능
    1. 사용자는 웹 브라우저 실행, [https://를](https://를) 사용해 안전한 페이지를 요청
    2. 웹 브라우저는 HTTPS포트로 웹 서버에 접근, 안전한 커넥션 요청
    3. 서버는 SSL 인증서의 카피와 함께 응답
    4. 웹 브라우저는 응답된 인증서의 카피를 사용해서 서버의 정보를 인증하고 서버의 공개키를 추출
    5. 웹 브라우저는 세션키를 생성, 서버의 공개키를 사용해서 세션키를 암호화하고 서버에 전송
    6. 서버는 서버의 개인키를 사용해 세션키를 복호화
    7. 클라이언트와 서버는 세션키를 사용해 이후의 정보들을 암호화 전송
