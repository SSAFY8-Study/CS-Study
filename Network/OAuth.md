# OAuth

# 1. OAuth란?

![https://user-images.githubusercontent.com/56240505/125554097-e3b5f9ff-0cda-4328-a673-03b817166aa2.png](https://user-images.githubusercontent.com/56240505/125554097-e3b5f9ff-0cda-4328-a673-03b817166aa2.png)

OAuth 는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준

→ 위 그림을 예로 들면, 외부 Application(원티드)은 사용자 인증을 위해 Facebook, Apple 그리고 Google의 사용자 인증 방식을 사용 → 이 때, OAuth를 바탕으로 제3자 서비스(원티드)는 외부 서비스(Facebook, Apple, Google)의 특정 자원을 접근 및 사용할 수 있는 권한을 인가받게 됨

# 2. OAuth 참여자

- Resource Server : Client가 제어하고자 하는 자원을 보유하고 있는 서버
    - Facebook, Twitter, Google, Apple, etc.
- Resource Owner : 자원의 소유자
    - Client가 제공하는 서비스를 통해 로그인하는 실제 유저가 이에 속함
- Client : Resource Server에 접속해 정보를 가져오고자 하는 Client(Application)

# 3. OAuth Flow

## 3.1. Client 등록

Client(Application)가 Resource Server를 이용하기 위해선 Client를 등록함으로써 사전 승인을 받아야 함 (ex. Github Developer Setting에서 Client 등록)

→ 등록 절차를 통해 세가지 정보를 Resource Server로부터 받음

1. Client ID : Client Application을 구별할 수 있는 식별자
2. Client Secret : Client ID에 대한 비밀키, 노출되면 안됨
3. Authorized redirect URL : Authorization Code를 전달받을 redirect URL

## 3.2. Resource Owner의 승인

Resource Server에서는 로그인을 하기 위해 Client에게 GET요청과 필요한 파라미터들을 보내도록 명시함

ex. `GET https://github.com/login/oauth/authorize?client_id={client_id}&redirect_uri={redirect_uri}?scope={scope}`

- scope는 Client가 Resource Server로부터 인가받을 권한의 범위
1. Client Application의 소셜 로그인 버튼을 클릭하면, Resource Owner는 Resource Server에 접속하여 로그인을 수행
2. 로그인이 완료되면 Resource Server는 Query String으로 넘어온 파라미터들을 통해 Client를 검사
    1. Client ID와 동일한 ID값이 존재하는지 확인
    2. 해당 Client ID에 해당하는 redirect URL이 파라미터로 전달된 값과 같은지 확인
3. 확인이 마무리되면 Resource Server는 Resource Owner에게 명시된 scope에 해당하는 권한을 Client에게 부여할 것인지 확인
4. 허용한다면 Resource Owner가 Resource Server에게 Client의 접근을 최종적으로 승인

## 3.3. Resource Server의 승인

1. Resource Owner의 승인이 마무리되면 redirect URL로 Client를 redirect시킴
2. Resource Server는 Client가 Resource Server의 자원을 사용할 수 있는 Access Token을 발급하기 전에, 임시 암호인 Authorization Code를 함께 발급(Query String의 code)
3. Client는 ID와 비밀키 그리고 Authorization Code를 Server에 직접 전달, Resource Server는 정보를 검사한 후 유효한 요청이라면 Access Token을 발급
4. Client는 해당 토큰을 서버에 저장해두고 Resource Server의 자원을 사용하기 위한 API 호출 시 해당 토큰을 헤더에 담아서 보냄

## 3.4. Refresh Token

Access Token은 만료 기간이 있으며, 만료된 토큰으로 API를 요청하면 401에러가 발생, 토큰이 만료될 때 마다 사용자가 재 로그인하는 번거로움 

→ 보통 Server는 Access Token을 발급할 때 Refresh Token을 발급

→ Client는 두 토큰을 모두 서버에 저장해두고, Resource Server의 API를 호출할 때 Access Token이 만료되어 401에러가 발생하면, Client는 Refresh Token을 보내 새로운 Access Token을 발급받음

(Refresh Token의 발급 여부와 방법 및 갱신 주기 등은 OAuth를 제공하는 Resource Server마다 다름)
