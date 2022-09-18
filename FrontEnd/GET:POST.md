# GET/POST

## GET

- URL에 data를 포함시켜 요청
    - www.example.com/show?name1=value1&name2=value2
- idempotent(멱등) : 서버에게 동일한 요청을 여러번 전송하더라도 동일한 응답이 돌아와야 함 → 서버의 리소스에서 데이터를 요청할 때 사용, select
- data를 header에 포함시켜 전송
- URL에 data가 노출 → 보안에 취약
    - 브라우저 히스토리에 남음
- 전송하는 길이에 제한(브라우저마다 제한이 다름)
- 캐싱 가능(재요청시 빠르게 접근하기 위해 레지스터에 데이터를 저장)

## POST

- URL에 data를 노출하지 않고 요청
- Non-idempotent : 서버에게 동일한 요청을 여러번 전송해도 응답은 항상 다를 수 있음 → 서버의 리소스를 새로 생성하거나 업데이트할 때 사용, create
- data를 body에 포함시킴
- URL에 data가 노출 X → 기본적인 보안 O
    - data가 브라우저 히스토리 또는 로그에 저장되지 않음
- 전송하는 길이제한 X
- 캐싱 X