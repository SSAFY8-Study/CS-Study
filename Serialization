# 0807 test

## Serialization

- 직렬화는 객체를 파일 등에 저장하거나 네트워크로 전송하기 위해 연속적인 데이터(byte형태)로 변환하는것이다. → JVM의 메모리(힙 또는 스택)에 상주되어있는 객체 데이터를 바이트 형태로 변환하는 기술.
- 반대로 파일에서 객체로 돌리는 행위는 역직렬화다. 역직렬화 시에는 모델의 버젼간의 호환성을 유지하기 위해서 동일한 serialVersionUID를 가지고 있어야한다. (객체가 업데이트 되었을 시에 문제 발생)

## Serialization 오류

- ObjectOutputStream을 통한 writeObject 메서드 호출 시 해당 객체에 Serializable 인터페이스가 구현되어 있지 않으면, NotSerializableException이 발생된다.

## Serialization 조건

- Serializable 인터페이스를 구현해야한다.
- 직렬화에서 제외하려는 멤버는 transient선언해준다. (ex. password)
