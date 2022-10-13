# **📎 TCP의 3-Way HandShake**

### **개념**

-   TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정하는 과정이다.
-   양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고,  
    실제로 데이터 전달이 시작 전 다른 한 쪽이 준비되었다는 것을 알 수 있도록 한다.
-   TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에  
    정확한 전송을 보장하고자 상대 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

</br>

### **동작 방식**

![image](https://user-images.githubusercontent.com/59721896/195627016-1f55518e-1b95-45d8-a0ed-239b50cb7336.png)

**\[ Step 1 \]**

-   Client는 Server와 커넥션을 생성하기 위해 SYN(x)을 보낸다.
-   이 때 Client는 CLOSED에서 SYN\_SENT로 변하고, Server는 LISTEN 상태이다.

**\[ Step 2 \]**

-   Server가 SYN(x)을 받고, Client에게 받았다는 신호로 ACK(x+1)와 SYN(y)패킷을 보낸다.
-   요청을 수락했으며, 포트를 열어달라는 메시지를 전송한 후, 클라이언트의 ACK 응답을 기다린다.
-   이 때 Client는 CLOSED이며 Server는 SYN\_REVEIVED 상태이다.

**\[ Step 3 \]**

-   Client는 Server의 ACK(x+1)와 SYN(y)패킷으로 응답을 받고, ACK(y+1)를 Server에 보낸다.
-   이 때, Client는 ESTABLISHED 상태이며,  
    Server는 ACK응답을 통해 SYN\_RECEIVED에서 ESTABLISHED로 바뀐다.

**_👉 연결이 이루어지고, 데이터 전송이 가능하다._**

</br>

# **📎 TCP의 4-Way HandShake**

### **개념**

-   TCP 통신에서 연결을 해제하는 과정이다.
-   데이터 전송을 완료하고, FIN 플래그와 ACK를 통해 서로의 안전한 종료를 확인한다.

</br>

### **동작 방식**

![image](https://user-images.githubusercontent.com/59721896/195627120-beead613-a8a3-4f58-9571-a1dbf20b605e.png)

**\[ Step 1 \]**

-   Client가 연결을 종료하겠다는 FIN 플래그(ACK도 포함)를 전송한다. (Client가 close() 호출)
-   이 때 Client는 FIN\_WAIT 상태가 된다.

**\[ Step 2 \]**

-   Server는 FIN을 받고, 확인했다는 ACK를 Client에 보낸다.
-   이 때 Server는 CLOSE\_WAIT 상태가 되고, 남은 데이터가 있다면 마저 전송을 마친 후에 close()를 호출한다.
-   Client는 Server에서 ACK를 받은 후에 서버가 남은 데이터 처리를 끝내고 FIN을 보낼 때까지 기다린다. (FIN\_WAIT2)

**\[ Step 3 \]**

-   모든 데이터 전송을 완료했다면, 서버는 연결 종료에 합의한다는 의미로 FIN 패킷을 Client에 보낸다.
-   그리고 이 때 Server는 승인 번호를 보내줄 때까지 기다리는 LAST\_ACK 상태에 들어간다.

**\[ Step 4 \]**

-   Client는 FIN을 받고, 확인했다는 ACK를 Server에 보낸다.
-   이 때 Client는 아직 받지 못한 데이터가 있을 수 있으므로 TIME\_WAIT을 통해 기다린다.  
    **👉 TIME\_WAIT 상태를 통해, 의도치 않은 에러로 인하여 연결이 데드락으로 빠지는 것을 방지한다.**  
    *(만약 에러로 인해 종료가 지연되거나 타임이 초과되면 CLOSED로 들어간다.)*
-   Server는 ACK를 받은 후 소켓을 닫고 CLOSED 상태가 된다.
-   TIME\_WAIT 시간이 끝나면 Client도 CLOSED 상태로 들어간다.

</br>

#### **📍 TCP의 연결 설정 과정과 해제 과정의 단계가 다른 이유**

Client가 데이터 전송을 마쳤다고 하더라도, Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고,

데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.

</br>

참고

-   [https://ddooooki.tistory.com/21](https://ddooooki.tistory.com/21)
-   [https://bangu4.tistory.com/74](https://bangu4.tistory.com/74)
-   [https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)
