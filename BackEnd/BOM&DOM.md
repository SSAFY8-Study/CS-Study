# BOM(Browser Object Model)

## BOM이란?

JS가 Browser와 관련된 window기능을 제어하기 위한 방식

BOM의 최상위 객체는 window 객체!

## BOM의 대표 객체

| window | 최상위 객체로 각 프레임 별로 하나씩 존재 |
| --- | --- |
| navigator | 브라우저명과 버전 정보 제공 |
| document | 현재 문서에 대한 정보 제공 |
| location | 현재 URL에 대한 정보 제공 |
| history | 현재 브라우저가 접근했던 URL history 제공 |
| screen | 브라우저의 외부 환경에 대한 정보를 제공 |

![https://user-images.githubusercontent.com/44748142/192987093-c8048681-58b2-4615-a759-16755979a8d0.png](https://user-images.githubusercontent.com/44748142/192987093-c8048681-58b2-4615-a759-16755979a8d0.png)

# DOM

## **DOM이란?**

Document Object는 HTML의 tag를 JS가 활용할 수 있도록 만든 객체를 의미하고, 모델은 객체를 인식할 수 있도록 모듈화 진행을 의미.

➡️ 웹 브라우저에서 html 문서를 인식하는 방식.

## DOM의 구조

- 트리 구조
- HTML 페이지를 왼쪽의 DOM으로 변환시킨 후, JS가 사용할 수 있게 됨으로써 동적인 페이지 구성 가능

![https://user-images.githubusercontent.com/44748142/192977816-5ce14a50-38d0-45d3-ba5b-6a3e44dd5434.png](https://user-images.githubusercontent.com/44748142/192977816-5ce14a50-38d0-45d3-ba5b-6a3e44dd5434.png)

[img제공 : [https://cbw1030.tistory.com/46](https://cbw1030.tistory.com/46)]

## DOM 노드의 종류

- 주로 쓰이는 5가지 대표 노드

| 노드 | 설명 |
| --- | --- |
| 문서 노드(Document node) | HTML 문서 전체를 나타내는 노드.(root node) |
| 요소 노드(Element node) | HTML의 Tag. 속성 노드를 가질 수 있음. |
| 속성 노드(Attribute node) | Tag 안에 있는 name, value 등의 속성들. 요소 노드에 관한 정보를 가지고 있음. |
| 텍스트 노드(Text Node) | Tag 내 텍스트. 요소 노드의 자식이며 자신의 자식 노드는 가질 수 없으므로 DOM 트리의 최종단 |
| 주석 노드(Comment node) | HTML 내의 주석. |

## JS의 DOM 객체 접근법

- getElementById
- getElementByTagName
- getElementByClassName
- querySelector

➡️ 위의 선택자를 가지고 JS가 DOM객체에 접근해서 웹 페이지의 내용을 제어

# BOM과 DOM의 차이점

DOM은 document, 현재 눈에 보이는 웹 문서에 대한 제어와 변경

BOM은 window 속성에 속하여 document가 아닌, window를 제어
