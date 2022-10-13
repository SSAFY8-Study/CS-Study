# OSI 7계층

## OSI 7계층이란?

국제표준기구 ISO가 발표한 네트워크 모델로, 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것

## OSI 7계층을 나눈 이유?

- 통신이 일어나는 과정을 단계별로 파악 가능
- 통신 과정에서 이상 발생시 현상에 따라 원인 파악이 용이해짐

## OSI 7계층

하위 계층으로 내려갈수록 Encapsulation(캡슐화)가 진행되고, 상위 계층으로 올라갈수록 De-Encapsulation(디캡슐화) 진행

![https://user-images.githubusercontent.com/44748142/195549973-c3e15c2c-59f7-4210-a5ea-384780cc502e.png](https://user-images.githubusercontent.com/44748142/195549973-c3e15c2c-59f7-4210-a5ea-384780cc502e.png)

## 계층마다 주된 기능

- 1-4계층 : 데이터 전달
- 5-7계층 : 프로세스들 간의 통신 프로토콜 설정

## Application Layer(7계층)

- 응용프로세스를 직접 사용하여 응용 서비스를 수행
- HTTP/HTTPS, FTP, SMTP 등의 프로토콜 포함

## Presentation Layer(6계층)

- 데이터의 표현 방식을 결정
- Application Layer로 부터 받은 데이터를 읽을 수 있는 형식으로 데이터의 인코딩, 디코딩, 암호화, 복호화 등 수행
- JPEG(그림), MPEG(동영상),ASCII(인코딩방식), MIDI(음원파일) 등의 확장자가 여기에 포함

## Session Layer(5계층)

- 응용 프로그램 간의 세션 관리
- 즉, 모든 통신 장치 간의 논리적 연결을 설정하고 관리 및 종료
- 송신자와 수신자의 통신을 위한 동기화 신호를 주고 받음
- 포트 연결이라고 하며, SSH, TLS 등이 대표적인 프로토콜

*논리적 연결 : IP, MAC adress(물리주소) 등을 통해 통신

## Transport Layer(4계층)

- 서로 다른 두 네트워크 간의 데이터 전송을 담당
- port번호와 전송방식(TCP/UDP) 결정
- 효율적인 데이터 전송을 위해 세그멘테이션, 흐름제어, 오류제어 등을 수행
    - 세크멘테이션 : 상위 계층 데이터를 받아 세그먼트 단위로 나누는 것. 데이터를 세그먼트 단위로 연속적으로 로딩하여 일부분을 먼저 제공하므로써 사용자의 경험을 최적화함. 또한 큰 데이터가 날라가는 것을 방지
    - 흐름제어 : 기기의 전송량에 따라 전송량 조절
    - 오류제어: 데이터의 오류 손실 확인 후 재요청

## Network Layer(3계층)

- 데이터를 수신지까지 가장 안전하고 빠르게 전송
- IP와 라우터가 속하여, 송신자와 수신자의 주소(IP)를 정하고 수신지까지 최적의 경로를 찾아 주는 기능 제공

## DataLink Layer(2계층)

- 동일한 네트워크 내에서의 데이터 전송 관리. 즉 다른 네트워크를 다룬 통신은 관여하지 않음.
- Physical Layer를 통해 송수신되는 정보의 오류제어와 흐름제어 관리
- 즉, 위의 계층으로 안전한 데이터를 보내기 위해 Physical Layer에서 받은 데이터에 오류가 있는지 확인하는 계층이라고 생각하면 됨.

## Physical Layer(1계층)

- bit 단위를 아날로그 신호로 바꾸거나, 받은 아날로그 신호를 bit로 변환하여 데이터의 전달 역할만 함.

# 💊데이터의 캡슐화

**데이터 전송 시 7계층 → 1계층**으로 진행. 이 과정에서 캡슐화 진행되는데, 각 계층은 **다른 계층과 통신할 때** 데이터의 특정 정보가 담긴 **Header와 Footer를 추가**한 후 다음 계층으로 전달

**Protocol Data Unit**은 프로토콜의 데이터 단위이며 OSI 모델의 정보 처리 단위. 

**캡슐화**

데이터가 아래 계층으로 전달될 때마다  PDU에 다양한 프로토콜의 정보가 추가된 Header와 Footer가 더해짐. 

**디캡슐화**

반대로 데이터를 받은 수신자는 PDU로 부터 Header와 Footer를 분석하며 최종 1계층에서는 원본 데이터만 얻음

# 수신과정

| OSI 7계층 | Protocol Data Unit | 하는 일 |
| --- | --- | --- |
| Application Layer | Data | HTTP/HTTPS 사용하여 데이터 전송 |
| Presentation Layer | Data | 받은 데이터를 변환하거나 암호화 혹은 압축 수행 |
|  Session Layer | Data | 송신자와 수신자의 통신을 위한 동기화된 정보를 삽입하여 전달 |
| Transport Layer | TCP/UDP Header+Data ⇒ segment | TCP/UDP와 송신지와 수신지에 대한 port정보를 설정하여 Header에 추가 후 윗 계층에서 받은 데이터에 추가. 흐름제어와 오류 제어 수행 |
| Network Layer | IP Header+TCP/UDP Header+Data ⇒ packet | 라우팅에 필요한 송신지와 수신지의 IP정보를 Header에 넣은 후 segment에 추가 |
| DataLink Layer | FrameHeader+IP Header+TCP/UDP Header+Data +FrameTrailer⇒ Frame | 해당 계층에서는 우선 Frame단위로 데이터를 나눔. 출발지와 라우터의 MAC 주소를 Header에 넣은 후 packet에 추가. 오류 제어를 위한 정보인 Frame Trailer 추가. |
| Physical Layer |  | bit를 아날로그 신호로 변환 후 전송 |

*MAC Address : MAC 프로토콜. 16진수의 총 6개의 조합으로 이루어진 주소

[Reference]

https://velog.io/@jeongs/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5-%EA%B7%B8%EB%A6%BC%EA%B3%BC-%ED%95%A8%EA%BB%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0

https://lxxyeon.tistory.com/155
