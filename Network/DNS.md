# DNS

# DNS란

- DNS(Domain Name System)는 사람이 읽을 수 있는 도메인 이름(예: www.amazon.com)을 머신이 읽을 수 있는 IP 주소(예: 192.0.2.44)로 변환
- 인터넷의 DNS 시스템은 이름과 숫자 간의 매핑을 관리하여 전화번호부 같은 기능
- DNS 서버는 이름을 IP 주소로 변환하여 도메인 이름을 웹 브라우저에 입력할 때 최종 사용자를 어떤 서버에 연결할 것인지를 제어, 이 요청은 쿼리

# DNS 서비스 유형

- **신뢰할 수 있는 DNS**
    - 신뢰할 수 있는 DNS 서비스는 개발자가 퍼블릭 DNS 이름을 관리하는데 사용하는 업데이트 메커니즘을 제공
    - 이 메커니즘을 통해 DNS 시스템은 DNS 쿼리에 응답하고 도메인 이름을 IP 주소로 변환 → 컴퓨터가 서로 통신 가능
    - 도메인에 대해 최종 권한이 있으며 재귀적 DNS 서버에 IP 주소 정보가 담긴 답을 제공
- **재귀적 DNS**
    - 보통 클라이언트는 신뢰할 수 있는 DNS 서비스에 직접 쿼리를 수행하지 않음
        
        → 일반적으로 재귀적 DNS 서비스(해석기)에 연결, 사용자를 대신해 DNS 정보를 가져오는 중간자 역할
        
    - 재귀적 DNS가 일정 기간 캐시된/저장된 DNS 참조를 가지고 있는 경우
        
        → 소스 또는 IP 정보를 제공하여 DNS 쿼리에 답을 함
        
    - 그렇지 않다면 → 해당 정보를 찾기 위해 쿼리를 하나 이상의 신뢰할 수 있는 DNS 서버에 전달

# DNS 서비스 개요

![https://d1.awsstatic.com/Route53/how-route-53-routes-traffic.8d313c7da075c3c7303aaef32e89b5d0b7885e7c.png](https://d1.awsstatic.com/Route53/how-route-53-routes-traffic.8d313c7da075c3c7303aaef32e89b5d0b7885e7c.png)

1. 사용자가 웹 브라우저를 열어 주소 표시줄에 www.example.com을 입력
2. www.example.com에 대한 요청은 일반적으로 인터넷 서비스 제공업체(ISP)가 관리하는 DNS 해석기로 라우팅
3. ISP의 DNS 해석기는 www.example.com에 대한 요청을 DNS 루트 이름 서버에 전달
4. ISP의 DNS 해석기는 www.example.com에 대한 요청을 이번에는 .com 도메인의 TLD 이름 서버 중 하나에 다시 전달, .com 도메인의 이름 서버는 example.com 도메인과 연관된 4개의 Amazon Route 53 이름 서버의 이름을 사용하여 요청에 응답
5. ISP의 DNS 해석기는 Amazon Route 53 이름 서버 하나를 선택해 www.example.com에 대한 요청을 해당 이름 서버에 전달
6. Amazon Route 53 이름 서버는 example.com 호스팅 영역에서 www.example.com 레코드를 찾아 웹 서버의 IP 주소 192.0.2.44 등 연관된 값을 받고 이 IP 주소를 DNS 해석기로 반환
7. ISP의 DNS 해석기가 마침내 사용자에게 필요한 IP 주소를 확보, 해석기는 이 값을 웹 브라우저로 반환. DNS 해석기는 다음에 누군가가 example.com을 탐색할 때 좀 더 빠르게 응답할 수 있도록 사용자가 지정하는 일정 기간 example.com의 IP 주소를 캐싱(저장) 
8. 웹 브라우저는 DNS 해석기로부터 얻은 IP 주소로 www.example.com에 대한 요청을 전송, 여기가 콘텐츠가 있는 곳
9. 192.0.2.44에 있는 웹 서버 또는 그 밖의 리소스는 www.example.com의 웹 페이지를 웹 브라우저로 반환하고, 웹 브라우저는 이 페이지를 표시