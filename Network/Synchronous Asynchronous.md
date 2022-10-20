## Synchronous
![image](https://user-images.githubusercontent.com/64126100/196896232-c822a74d-bbe5-4cc5-b49a-7e4003b4197d.png)

- 동기식 통신이라고도 하며, Reqeust를 보내게 된다면 시간이 얼마나 걸리든 그 자리에서 Response를 받는 방식으로 두 서버 사이의 Transaction(업무 또는 연산 처리의 단위)을 맞추는 것을 의미한다.
- Request를 보내면 Response를 기다려야 하기 때문에 Request를 보낸 thread에서는 Response를 기다리는 상태를 유지하게 되고, 이를 Block 상태라고 한다.

<br>

## Synchronous의 장점
- Thread가 Request를 보내고 Response를 받은 후 다시 Request를 보내는 작업을 수행하기 때문에 요청과 응답 값의 순서를 보장할 수 있다.
- 보낸 Request에 대한 처리 결과 값을 보장 받을 수 있다.
- Request- Response가 한 세트로 처리되기 때문에 설계가 매우 간단하고 직관적이다.

<br>

## Synchronous의 단점
- Response가 지연되게 된다면 Request를 보낸 thread가 계속 Block상태를 유지하게 되는 단점이 있다.
- 순차적으로 Response를 받고 Request를 받는 구조로 Response가 계속 지연되게 된다면 뒤에 들어오는 Request들은 수행 가능한 Thread가 없어 연결을 맺지 못 해 성능이 떨어질 수 있다.

<br>

## Asynchronous
![image](https://user-images.githubusercontent.com/64126100/196897279-d29ce766-c08e-48aa-8f16-50eabe647262.png)

- 비동기식 통신이라고도 하며, Synchronous와 다르게 Request를 보내더라도 바로 Response를 Response를 언제 받아도 상관없는 상태를 가지는 방식이다.
- Request를 보낸 thread가 Response를 기다리지 않고 다른 연산이나 업무를 수행할 수 있게 되고, 이러한 상태를 Non Block이라고 한다.
- 비동기식 처리를 요청할 때 할 일이 끝난 후 처리 결과를 알려주는 콜백이라는 함수를 활용하고, 호출받은 함수는 처리가 끝나면 요청한 함수를 호출하여 처리 결과를 전달한다.
- DOS(Disk Operating Systemm, IBM PC 호환기종에서 널리 쓰이던 디스크 운영체제의 일종)같은 단일 운영체제에서는 불가능하고, windows 같은 멀티 태스킹 환경을 제공할 수 있는 운영체제에서만 활용이 가능하다.

<br>

## Asynchronous의 장점
- Response를 기다리지 않고, Non-Block 상태로 계속 업무나 연산을 수행할 수 있기 때문에 Synchronous에 비해 상대적으로 성능이 좋다.
- 결과가 주어지는데 시간이 오래 걸려도 다른 작업을 수행할 수 있어 자원을 효율적으로 활용할 수 있다.

<br>

## Asynchronous의 단점
- Thread가 Response를 받지 않고, 여러가지 Request를 보냈을 때, 뒤에 보낸 Request들이 먼저 처리될 수 있고, 이로 인해 작업 순서를 보장할 수 없다. (순서 보장이 필요한 업무에는 활용할 수 없다.)
- 처리 Logic이 Synchronous에 비해 복잡해진다.
