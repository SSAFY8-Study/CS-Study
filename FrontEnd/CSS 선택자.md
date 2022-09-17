# CSS 선택자

- CSS 는 **선택자**와 **선언** 부분으로 구성
- **선언**은 **중괄호**로 감싸며, **속성**과 **값**으로 구성
- **여러 선태자**에 동일한 스타일 적용시, **comma(,)**로 구분
- 선언 블록 안에 **여러 속성 적용**시, **semi-colon(;)**으로 구분
- 주석 : **/* 주석 내용*/**

![image](https://user-images.githubusercontent.com/44748142/190870056-11ca83e5-e52d-48e6-80b1-a4361f6adaa8.png)

## **선택자 종류**

**일반 선택자**

- 일반 선택자 우선 순위 : **전제 선택자<타입 선택자<클래스 선택자<ID 선택자**
- 전체 선택자                     *{ }
- 타입 선택자                     E1, E2 { }
- 클래스 선택자                . class-name{ }
- ID 선택자                         #id-name{ }

**복합 선택자**

- 하위 선택자                     E1 E2 { }
- 자식선택자                      E1>E2 { }
- 인접 형제 선택자            E1+E2 { }
- 일반 형제 선택자            E1~E2{ }

**그 외 선택자**

- 가상 클래스 선택자
- 가상 엘리먼트 선택자
- 속성 선택자
    
    

### **일반 선택자 - 전체 선택자**

- HTML 문서 내 모든 element에 적용
- 우선 순위가 가장 낮음

css
```css
* {
		background: skyblue;
		color: magenta;
		font-weight: bold;
	}
```

### 일반 선택자 - 타입 선택자

- 태그명을 이용해서 스타일 적용
- 여러 element에 동일한 스타일 적용시, comma(,)로 구분

css
```css
div, p {
		padding: 10px;
		margin: 10px;
		font-weight: bold;
	}
```

### 일반 선택자 - 클래스 선택자

- element의 클래스 이름을 사용하여 스타일 적용
- 클래스 명은 공백없이 대소문자 또는 Hypen(-), UnderScore(_)로 시작하며, 기호나 숫자로 시작하지 않는다
- element의 class 속성 값에 하나 이상의 클래스 이름 적용시, 공백으로 구분

html

```html
<!--class 속성 값에 하나 이상의 클래스 이름 적용시, 공백으로 구분-->
<div class="name1 name2">div Class Selector</div>
<div class="name3">div Class Selector</div>
<p class="name1">p Class Selector</p>
```

css

```css
.name1,.name3 { /*여러 클래스에 동일한 CSS적용시 콤마로 구분*/
  background: skyblue;
  color: magenta;
}
div.name1 { /*div 중 클래스 명이 name1인 곳에 CSS적용 */
  font-weight: bold;
  font-size: 20px;
}
```

### 일반 선택자 - ID 선택자

- element의 ID를 사용하여 스타일 적용
- HTML문서에서 **동일한 ID 사용 불가**(**Class명은 동일**해도 되지만, **ID는 유일**해야 함)
- element의 **ID 속성 값에 1개의 ID만 사용 가능**
- 일반 선택자 중 **우선순위가 가장 높음**

html

```html
<div>div ID Selector</div>
<p id="ID1">p ID Selector</p>
```

css

```css
#ID1{
  background: skyblue;
  color: magenta;
}
```

### 복합 선택자 - 하위 선택자&자식 선택자

- **하위 선택자**는 **1단계 하위 요소와 2단계 이상 하위 요소**에 모두 적용
- **자식 선택자**는 **1단계 하위 요소에만** 적용

html

```html
<div>
  div Descendant Selector
  <p>div > p Descendant Selector</p> <!--style2적용가능 style4적용가능-->
  <div> <!--style1적용가능 style3적용가능-->
    div div Descendant Selector
    <span>
      <div> <!--style1적용-->
        <ul>
					<!--p에 style2적용-->
          <li><p>div p Descendant Selector</p></li>
        </ul>
      </div>
    </span>
  </div>
</div>
```

css

```css
div div { /*style1 : div 자식 중 모든 div에 적용 */
    background: blue;
    color: red;
}
div p { /*style2 :div 자식 중 모든 p에 적용*/
  background: lightgray;
  color: skyblue;
}
div > div { /*style3 :div 자식 중 바로 다음 div에만 적용*/
  background: green;
  color: orange;
}
div > p { /*style4 : div 자식 중 바로 다음 p에만 적용*/
  background: purple;
  color: pink;
}
```

### 복합 선택자 요소 - 인접 형제 선택자&일반 형제 선택자

- 인접 형제 선택자는 형제 관계 중 인접하는 첫 번째 element만 적용
- 일반 형제 선택자는 형제 관계 중 인접하는 모든 element에 적용
- 기준 element 중 아래 있는 element 만 생각하기

html

```html
<div>div</div>
<p>p style1 적용 가능</p>
<p>p style1 적용 불가</p>
<div class="class1">div</div>
<p>p style1 적용 가능, style2 적용 가능</p>
<p>p style1 적용 불가, style2 적용 가능</p>
<div>div</div>
<p>p style1 적용 가능, style2 적용 가능</p>
```

css

```css
div + p { /*style1 : div의 형제 element 중 첫번째 element가 p일 경우 적용*/
  background: lightgray;
  color: orange;
}
div.class1~ p {/*style2:div의 형제 element 중 모든 p element에 적용*/
  background: green;
  color: skyblue;
}
```

### 가상 클래스 선택자

- : 사용
- a 태그에서 많이 사용하는 선택자
    - : link  ⇒ 해당 링크를 방문하지 않았을 때 적용
    - :visited  ⇒ 해당 링크를 방문했을 때 적용
    - :hover  ⇒ 마우스가 올라간 경우 적용
    - :active  ⇒ 요소가 활성화 된 경우 적용 ex)마우스로 눌러진 경우
- :focus  ⇒ 요소가 포커스 된 경우 적용 ex) input요소에 문자 입력시 적용
- :first-child  ⇒ 지정된 요소의 첫번째 자식에 적용
- :last-child  ⇒ 지정된 요소의 마지막 자식에 적용
- :nth-child(n)  ⇒ 지정된 요소의 n번째 자식에 적용
    - n은 0부터 시작하지만, 자식 순번은 1부터 시작
    - nth-child(odd) ⇒ 자식 중 홀수 적용
    - nth-child(even) ⇒ 자식 중 짝수 적용
    
    html
    
    ```html
    <ul>
      <li>첫 번째 li</li>
      <li>두 번째 li</li>
      <li>세 번째 li</li>
      <li>네 번째 li</li>
      <li>다섯 번째 li</li>
      <li>여섯 번째 li</li>
      <li>일곱 번째 li</li>
      <li>여덟 번째 li</li>
    </ul>
    ```
    
    css
    
    ```css
    li:nth-child(5) {
      color: magenta;
    }
    li:nth-child(3n + 1) {
      color: skyblue;
    }
    li:last-child {
      color: orange;
    }
    ```
    
    결과
    
    ![image](https://user-images.githubusercontent.com/44748142/190870086-49137e8a-d3ae-4a5f-b28f-194190e80217.png)
    
- :enabled  ⇒ 요소가 활성화 된 경우 적용
- :disabled  ⇒ 요소가 비활성화 된 경우 적용
- :checked  ⇒ 요소가 checked된 경우 적용

### 가상 엘리먼트 선택자

- :: 사용
- ::after  ⇒ 요소 뒤에 content 추가

css
```css
/*p태그의 마지막 요소 뒤에 추가*/
p:last-child::after {
        content: "안녕하세요";
        color: orange;
}
```

- ::before  ⇒ 요소 앞에 content 추가
- ::first-letter  ⇒ 요소의 첫번째 문자 적용
- ::first-line  ⇒ 요소의 첫번째 라인 적용
- ::selection  ⇒ 사용자에 의해 선택된 요소에 적용 ex) 문자를 드래그할 경우

### 속성 선택자

- [A] ⇒ 해당 속성을 가진 모든 element 적용
- [A=V] ⇒ A속성에 V를 속성값으로 가진 모든 element 적용
- [A~=V] ⇒ A 속성값에 V를 단어로 포함하는 element 적용(단어이므로 V 사이에 공백이 있어야함)
- [A^=V] ⇒ A 속성값이 V로 시작하는 element 적용
- [A*=V] ⇒ A 속성값이 V를 포함하는 element 적용(단어 아님)
- [A$=V] ⇒ A 속성값이 V로 끝나는 element 적용
- [A|=V] ⇒ A 속성값이 정확히 V이거나, V-로 시작하는 element 적용

html

```css
<div title="one">style1적용가능 </div>
<div title="two">style1적용가능, style2적용가능</div>
<p title="two">style1적용, style2적용가능, style3적용가능</p>
<p title="first second third">style1적용가능, style4적용가능</p>
<p class="second-container">style5적용가능, style8적용가능</p>
<p class="second-wrap">style5적용가능, style6적용가능, style8적용가능</p>
<div class="one-two-three">style7적용가능</div>
```

css

```css
[title] { /*style1*/
  color: steelblue;
  font-weight: bold;
}
[title="two"] { /*style2*/
  border: 2px solid pink;
}
p[title="two"] { /*style3*/
  color: orange;
}
p[title~="second"] { /*style4:p태그 중 second단어(공백필요)를 포함하는 element*/
  background: silver;
}
p[class^="second"] { /*style5:p태그 중 second로 시작하는 element*/
  background: cyan;
}
p[class$="wrap"] { /*style6*:p태그 중 wrap끝나는 element/
  color: deeppink;
  font-weight: bold;
} 
[class*="three"] { /*style7:class속성값이 three(단어아님)를 포함하는 element*/
  background: green;
}
[class|="second"] { /*style8:class속성값이 second(단어아님)로 시작하거나 포함하는 element*/
  border: 2px dotted darkgray;
}
```

### CSS 우선 순위

- 같은 element에 두개 이상의 CSS 규칙이 적용된 경우, **마지만 규칙**, **구체적인 규칙**, **!important**가 우선 적용

html

```html
<h1>CSS우선순위</h1>
<h3></h3>
<p id="id">p-id를 사용하여 구체적으로 표현된 style5 적용<b>b-!important로 style3적용</b><i>i-마지막 규칙으로 style2적용</i></p>
<p>style6적용</p>
```

css

```css
i { /*style1*/
  color: orange;
}
i { /*style2*/
  color: pink;
}
p b { /*style3*/
  color: green !important;
}
p b {  /*style4*/
  color: gray;
}
p#id{  /*style5*/
  font-size: 200%;
}
p {  /*style6*/
  font-size: 120%;
}
```
