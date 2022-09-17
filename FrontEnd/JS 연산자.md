# JavaScript 연산자
<br>

## 연산자(Operator)

JavaScript에서 기본적으로 제공하는 문자의 표현식을 연산자라고 한다.
연산자에는 산술 연산자, 비교 연산자, 논리 연산자 등이 있다.
 

|연산자|설명|
|--|--|
|++|	변수의 값을 증가시킴, 선행은 값 반환 후 증가, 후행은 값을 증가시킨 후 반환|
|--|변수의 값을 감소시킴, 선행은 값 반환 후 감소, 후행은 값을 감소시킨 후 반환|
|-|부호를 전환한 후 값을 반환|
|+|	숫자로 값을 반환|
|~	|비트 연산에서 NOT 연산 수행|
|!|	Boolean 연산에서 NOT 연산 수행|
|delete|Property를 제거|
|typeof|변수의 type을 반환|
|void|Undefined 값을 알려줌|
|+,-,*,/|사칙연산 수행|
|+|문자열의 경우 서로 결합|
|<<, >>|비트연산자로 값을 해당 방향으로 이동|
|<,<=,>,>=|	대소 비교|
|instanceof|객체가 특정 객체 type인지 확인|
|in|Property가 존재하는지 확인|
|==|동등 관계인지 확인|
|!=	|동등하지 않은지 확인|
|===|	값이 일치하는지 확인 (Type 포함)|
|!==|	값이 일치하지 않는지 확인 (Type 포함)|
|&,^,ㅣ|	비트 연산자로 AND, XOR, OR 연산|
|&&|	AND 연산|
|ㅣㅣ	|OR 연산|
|?:|	조건에 해당하는 구문을 수행|
|=|	변수 또는 Property에 값을 할당|
|,|	1번째 구문은 버리고 다음 구문 값 반환|
 <br>
<br>

 

## == vs ===

==과 === 모두 값이 일치하는지를 확인하는 연산자이지만 차이점은 자료형까지 비교하는지 아닌지의 여부이다.

<pre><code>
var n= 10;
var s = "10";

console.log('n==s: ' + (n==s)); //true
console.log('n===s: ' + (n===s)); //false

s="20";

console.log('n!=s: ' + (n!=s)); //true
console.log('n!==s: ' + (n!==s)); //true
</code></pre>

위와 같이 서로 같은 숫자 값인데 type이 다른 두 변수를 비교할 때, ==의 경우 true를 반환하지만 ===의 경우 false를 반환하는 것을 알 수 있다.
<br>
<br>
 

## Short Circuit Evaluation
 
<pre><code>
console.log(true && true); //true
console.log(true && false); //false
console.log(false && true); //false
console.log(false && false); //false

console.log(true || true); //true
console.log(true || false); //true
console.log(false || true); //true
console.log(false || false); //false
</pre></code>

AND, OR 연산을 수행할 때 위와 같은 결과값을 얻을 수 있다.

 

AND(&&) 연산의 경우 두 조건이 모두 참이면 참, 둘 중에서 하나 이상이 거짓이면 거짓이 된다.

그래서 && 연산자는 앞의 조건이 거짓일 경우 바로 거짓을 반환하고, 뒤의 연산은 생략한다.

 

OR(||) 연산의 경우 두 조건 중 하나라도 참이면 참이 된다. 모두 다 거짓이 아니라면 항상 참이 된다.

그래서 || 연산자는 앞의 조건이 참일 경우 바로 참을 반환하고, 뒤의 연산은 생략한다.

Short Circuit Evaluation은 이미 참 또는 거짓이 결정이 되었기 때문에 뒤의 조건까지 따져볼 필요가 없게 되어 바로 결과를 내어 버리는 경우를 의미한다. 그러므로 && 연산자를 사용할 경우에는 앞의 조건에 거짓이 될 확률이 높은 조건을 넣고, || 연산자를 사용할 경우에는 앞에 참이 될 확률이 높은 조건을 넣는것이 좋다.
<br>
<br>
 

## Boolean (true, false)

JavaScript에서 false로 취급 받는 몇가지 type들이 있다.

- undefined; (아직 정의가 내려지지 않은 상태)
- null; (값이 없는 상태)
- 0;
- NaN; (Not a Number의 약자, 연산과정에서 잘못된 값을 입력받았을 때를 나타내는 기호)
- ''; (공백, 비어있는 상태)

위의 경우들을 제외하고는 대부분 true로 간주된다.
