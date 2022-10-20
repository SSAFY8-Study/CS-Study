# Load Balancing

- 트래픽이 많을 때 서버의 로드율 증가, 부하량, 속도저하 등을 고려하여 여러 대의 서버로 적절하게 분산처리해주는 서비스

# Load Balancer

- 서버의 부하를 분산해주는 장치 또는 기술로 보통 서버 상단 네트워크에 위치
- 서버 한대에 집중되지 않도록 트래픽을 관리하며 각 서버가 최적의 효율을 발휘할 수 있게 해줌

![https://user-images.githubusercontent.com/44748142/196907416-39c0da03-d3f3-4e30-bdc1-5e1bdd47c58a.png](https://user-images.githubusercontent.com/44748142/196907416-39c0da03-d3f3-4e30-bdc1-5e1bdd47c58a.png)

# Load Balancer 기능

## Health Check

- 서버가 정상적으로 살아있는지 check
- L4와 L7 기능을 가지고 있어 port로 서버가 열려있는지 check

## NAT(Network Address Transtation)

- IP 패킷에 있는 출발지 및 목적지의 IP 주소와 TCP/UDP 포트 숫자 등을 바꾸어 재기록하면서 네트워크 트래픽을 주고 받게 하는 기술
- NAT 방식으로 Load Balancing 수행
- 내부 네트워크에서 사용하던 사설 IP주소를 로드밸런서 외부의 공인 IP 주소로 변경해주어 여러개의 client가 하나의 공인 IP로 접속하게 해줌

## DSR(Direct Server Return/routing)

- client → load balancer → server →  **load balancer → client** 네트워크 트래픽 순서를 client → load balancer → **server → client** 로 단계를 줄여  load balancer의 부하를 줄여줌

## 알고리즘에 따른 분산 처리

### Round Robin

- 들어오는 트래픽을 서버 순서대로 배치
- 연결된 세션이 비교적 오래 사용되지 않는 경우 효과적
- 가장 단순한 방법

### Least Connection 알고리즘

- 현재 매핑되어 있는 커넥션이 가장 적은 서버로 전달
- 트래픽으로 인해 세션이 길어지는 경우 효과적

### Hash

- 특정 기준을 잡아 특정 서버에 매핑하여 고정적으로 트래픽 분산
- 일반적으로 사용되는 기준은 클라이언트의 IP가 됨

### Weighted Round Robin

- 서버의 가중치에 따라 가장 높은 가중치를 가진 서버를 우선적으로 트래픽 분산
- 서버 A의 가중치:5 / 서버B의 가중치:2 ⇒ A서버에 5개의 트래픽 요청, B서버에 2개의 트래픽 요청 할당

# Load Balancer 종류

L4와 L7을 주로 사용

### L2

- MAC 주소를 바탕으로 Load Balancing 진행

### L3

- IP주소를 바탕으로 Load Balancing 진행

### L4

- Transpor Layer Level에서 IP주소와 PORT번호, MAC 주소,TCP/UDP로 Load Balancing 진행

**장점**

- 속도가 빠르고 데이터 내용을 복호화할 필요가 없어 안전

**단점**

- 패킷내용을 확인하지 않으므로 세분화된 서버 분산이 불가
- 사용자의 IP가 수시로 바뀌는 경우 연속적인 서비스 제공 불가

### L7

- Application Layer Level에서 URL 또는 HTTP헤더 정보로 Load Balancing 진행

**장점**

- URL 혹은 HTTP 헤더, 쿠키 등과 같은 사용자 요청을 기준으로 트래픽을 분산하므로, 패킷 내용을 확인하고 그에 따라 로드를 특정 서버에 분배하는 것이 가능해 요청을 보다 세분화하여 서버에 전달 가능
- 캐싱 기능 제공
- 특정한 패턴을 지닌 바이러스를 감지해 네트워크 보호 가능
- 비정상적인 트래픽을 판별할 수 있어 서비스 안정성 높음

**단점**

- 패킷 데이터를 복호화해야함
- 클라이언트가 로드밸런서와 인증서를 공유해야하므로 보안상의 위험성 존재

# Load Balancer 장애 대비

- 트래픽의 규모와 노후화에 따라 Load Balancer의 문제가 발생할 경우를 대비해 Load Balancer를 이중화시켜 장애를 대비함
1. 각각의 Load Balancer는 Health check 진행
2. Main Load Balancer가 동작하지 않으면 가상 IP는 두 번째 Load Balancer로 변경
3. 해당 Load Balancer를 사용하여 서버 분산

![https://assets.digitalocean.com/articles/high_availability/ha-diagram-animated.gif](https://assets.digitalocean.com/articles/high_availability/ha-diagram-animated.gif)

# ‼️ 면접질문

### Q1. 로드밸런싱이란?

A . 서버 구축과 활용 시에 고려하는 것으로 서버에 가해지는 부하를 적절하게 분산시켜주는 장치 또는 기술입니다.

### Q2. 서버 확장 기술의 두 가지 방법은?

A. **Scale-Up** 방식은 서버 자체의 성능을 향상시키는 것으로, 서버의 CPU, RAM 등을 교체하여 성능을 향상시키는 것입니다.

**Scale-Out** 방식은 ****기존 서버와 동일하거나 낮은 서버를 여러 대 두어 운영하는 방식입니다. 보통 해당 방식을 사용하는데, 이유는 비용적 측면에서 위의 방법보다 효과적이며, 여러 대의 서버를 사용하므로 무중단 서비스를 제공할 수 있습니다.

### Q3. 로드 밸런싱 알고리즘 중 대표적인 라운드 로빈과 최소 연결 방식은?

A. 라운드 로빈 알고리즘은 서버에 들어오는 요청을 순서대로 돌아가면서 서버에 배치하는 방식이며 세션이 오래 지속되지 않는 경우 적합합니다. 

최소 연결 방식은 트래픽 연결이 가장 적은 서버에 배치하는 방식으로 트래픽이 일정하지 않고 세션이 길어질 때 적합합니다. 

### Q4. L4와 L7 로드 밸런싱에 대한 설명과 이 둘의 차이점은?

A. L4 로드 밸런싱은 Transpor Layer의 정보를 바탕으로 트래픽을 분산하는 방식으로 TCP/UDP,IP,PORT 정보를 바탕으로 분산합니다. 요청 정보를 자세하게 보지 않고 패킷 레벨에서만 트래픽을 분산하므로 속도가 빠르고 효율성이 높습니다. 

L7 로드 밸런싱은 Application Layer의 정보를 바탕으로 트래픽을 분산하며, 사용자가 요청한 정보를 바탕으로 트래픽을 분산하므로 섬세한 라우팅과 비정상적인 트래픽 판별이 가능하지만 비용이 높습니다. 

[Reference]

- [https://www.digitalocean.com/community/tutorials/what-is-load-balancing#how-does-the-load-balancer-choose-the-backend-server](https://www.digitalocean.com/community/tutorials/what-is-load-balancing#how-does-the-load-balancer-choose-the-backend-server)
- [https://www.youtube.com/watch?v=kYipnodgi2I](https://www.youtube.com/watch?v=kYipnodgi2I)
- [https://nesoy.github.io/articles/2018-06/Load-Balancer](https://nesoy.github.io/articles/2018-06/Load-Balancer)
- [https://ttaehee.github.io/cs/network/traffic/loadbalancing/](https://ttaehee.github.io/cs/network/traffic/loadbalancing/)
- [https://maivve.tistory.com/269](https://maivve.tistory.com/269)
