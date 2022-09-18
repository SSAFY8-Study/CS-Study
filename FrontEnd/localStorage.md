# localStorage

- 웹 스토리지 객체중 하나(sessionStorage, localStorage)로 키-값 쌍을 저장
- 오리진이 같은 경우 데이터는 모든 탭과 창에서 공유됨
- 브라우저나 OS가 재시작하더라도 데이터 유지

## 기본 API

```jsx
// 키에 데이터 쓰기
localStorage.setItem("key", value);

// 키로 부터 데이터 읽기
localStorage.getItem("key");

// 키의 데이터 삭제
localStorage.removeItem("key");

// 모든 키의 데이터 삭제
localStorage.clear();

// 저장된 키/값 쌍의 개수
localStorage.length;
```

## 주의사항

키-값 쌍은 문자열 타입만 지원, 객체를 저장할때 문제

```jsx
> localStorage.setItem('num', 1)
undefined
> localStorage.getItem('num') === 1
false
// 자동으로 문자열로 변환됨
> localStorage.getItem('num')
"1"
> typeof localStorage.getItem('num')
"string"
```

→ JSON을 사용하면 된다

```jsx
// 객체형 데이터를 저장할 때
> localStorage.setItem('json', JSON.stringify({a: 1, b: 2}))
undefined
> JSON.parse(localStorage.getItem('json'))
{a: 1, b: 2}

// 배열형 데이터를 저장할 때
> localStorage.setItem('nums', JSON.stringify([1, 2, 3]))
undefined
> JSON.parse(localStorage.getItem('nums'))
[1, 2, 3]
```

로컬 스토리지에 쓸 데이터를 JSON 형태로 직렬화하고, 읽은 데이터를 JSON형태로 역직렬화

## 데이터 청소

로컬 스토리지에 저장된 데이터는 웹페이지를 닫는다고 사라지지 않음 → 청소

```jsx
> localStorage.length
5
> localStorage.key(0)
"email"
> localStorage.removeItem('obj')
undefined
> localStorage.length
4
> localStorage.clear()
undefined
> localStorage.length
0
```