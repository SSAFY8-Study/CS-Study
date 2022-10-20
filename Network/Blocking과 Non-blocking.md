# **📎 개념 비교**

Sync/Async와 Blocking/Non-blocking은 모두 프로세스를 운용하기 위한 방법이다.

<br>

### **Sync/Async**

"프로세스의 **수행 순서** 보장에 대한 매커니즘"

-   Sync : 요청이 들어온 **순서에 맞게** 하나씩 처리
-   Async : 하나의 요청이 끝나기도 전에, 다른 요청들을 **동시에** 처리

<br>

### **Blocking/Non-Blocking**

"프로세스의 **유휴 상태**에 대한 개념"

-   Blocking : 다른 주체의 **작업이 끝날 때까지** 기다렸다가 자신의 작업을 수행
-   Non-Blocking : 다른 주체의 **작업에 관련 없이** 자신의 작업을 수행

(Blocking/Non-Blocking의 경우 보통 IO에 많이 사용된다.)

<br>
<br>

# **📎 동작 비교**

Sync/Async와 Blocking/Non-blocking에 대한 동작 비교는

아래 그림과 같이 Thread1에서 여러 함수들이 실행을 기다리는 상황에서, Thread2로 첫 번째 함수를 나눈다고 가정하여 설명하겠다.

![image](https://user-images.githubusercontent.com/59721896/196991142-d0949577-885d-4c36-9ca5-edf84ff8dab6.png)

<br>

### **📍 Sync**

호출된 함수의 수행 결과 및 종료를 호출한 함수 및 호출된 함수가 신경쓴다.

![image](https://user-images.githubusercontent.com/59721896/196991234-7c580864-1aa9-4752-a301-df75f3276d02.png)

-   Thread1이 작업을 시작시키고, 함수1이 끝날 때까지 기다렸다가 함수2를 시작한다.
-   작업 요청을 했을 때의 요청의 결과값(return)을 직접 받는다.
-   호출한 함수 및 호출된 함수 모두 작업의 완료를 신경쓴다. (주기적으로 계속 물어본다.)

<br>

### **📍 Async**

호출된 함수의 수행 결과 및 종료를 호출된 함수 혼자 직접 신경쓰고, 처리한다.

![image](https://user-images.githubusercontent.com/59721896/196991306-feb1c785-0fd0-4d7a-ab18-f9f20bb499b0.png)

-   Thread1이 작업을 시작시키고(Callback 함수를 함께 전달), 완료를 기다리지 않고 Thread1은 다른 일을 처리한다.
-   작업 요청을 했을 때 요청의 결과값(return)을 간접적으로 받는다.
-   요청의 결과값이 return과 다를 수 있다.
-   함수1 혼자 작업 완료를 신경쓴다. (작업 완료 시 Callback 함수를 통해 결과값을 전달)

<br>

### **📍 Blocking**

호출된 함수가 자신이 할 일을 모두 마칠 때까지 제어권을 가지며, 호출한 함수에게 바로 돌려주지 않는다.

![image](https://user-images.githubusercontent.com/59721896/196991365-0d3d6e94-90dc-47bb-b741-37af5b70bf7c.png)

-   함수1이 있던 자리를 blocking 해놓고(일을 못하게 막음), 함수1이 작업을 마칠 때까지 대기한다.
-   함수1의 return 값을 받아야 다음 함수를 실행할 수 있다.
-   함수1이 return할 때까지 Thread1은 계속 사용/대기된다.

<br>

### **📍 Non-blocking**

호출된 함수가 자신이 할 일을 마치지 않았더라도 바로 제어권을 건네주어(return) 호출한 함수가 다른 일을 진행할 수 있게 해준다.

![image](https://user-images.githubusercontent.com/59721896/196991419-a44c78a9-24e8-4f54-a417-994f059f72ba.png)

-   요청한 작업을 즉시 마칠 수 없다면, 바로 return한다.
-   하나의 Thread가 여러 개의 IO를 처리할 수 있다.

<br>

### **✨ Sync/Async와 Blocking/Non-blocking의 핵심 차이점**

위의 동작 비교에서 Sync는 Blocking과 비슷하고, Async는 Non-blocking과 비슷하다고 보인다.

그러나 이들은 명확히 다른 개념으로, 관점의 차이로 구분이 가능하다.

-   Sync/Async는 **"어떤 함수가 신경쓰는지"** 의 관점에서 볼 수 있다.
-   Blocking/Non-blocking은 **"제어권이 어디있는지"** 의 관점에서 볼 수 있다.

<br>
<br>

# **📎 둘의 조합**

Sync/Async와 Blocking/Non-Blocking은 조합하여 많이 사용한다.

![image](https://user-images.githubusercontent.com/59721896/196991512-59422cea-c317-4e5b-a3c1-32a652eb29ef.png)

일반적으로 Sync와 Blocking, 그리고 Async와 Non-Blocking을 조합하여 많이 사용하며,

ASync와 Blocking 조합의 경우 사용하는 것에 대한 의미를 찾기 어렵기 때문에 잘 사용하지 않는다.

<br>
<br>

# **🌟 정리**

Sync/Async와 Blocking/Non-blocking은 모두 프로세스를 운용하는 방법이지만, 같은 개념은 아니다.

Sync/Async는 순서와 결과가 중요하며, 누가 신경쓰고 있는지에 대한 관점으로 볼 수 있다.

Blocking/Non-blocking은 제어권을 누가 가지고 있는지에 대한 관점으로 볼 수 있다.

Sync와 Blocking, 그리고 Async와 Non-blocking 조합으로 많이 사용된다.

<br>
<br>

참고

-   [https://www.inflearn.com/news/72620](https://www.inflearn.com/news/72620)
-   [https://steady-coding.tistory.com/531](https://steady-coding.tistory.com/531)
-   [https://velog.io/@wonhee010/%EB%8F%99%EA%B8%B0vs%EB%B9%84%EB%8F%99%EA%B8%B0-feat.-blocking-vs-non-blocking](https://velog.io/@wonhee010/%EB%8F%99%EA%B8%B0vs%EB%B9%84%EB%8F%99%EA%B8%B0-feat.-blocking-vs-non-blocking)
-   [https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC](https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)
-   [https://musma.github.io/2019/04/17/blocking-and-synchronous.html](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
