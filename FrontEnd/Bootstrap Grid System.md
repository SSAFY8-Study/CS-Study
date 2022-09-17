# Bootstrap Grid System

- Bootstrap은 layout과 content 정렬을 위한 **Grid System 제공**
- Grid System은 **열을 나누어 content를 원하는 위치에 배치하는 방법(layout)**을 의미
- Grid layout 구성 시, **container**내에서 **row**를 먼저 배치 후 그 안에 col-opt1-opt2(**column**)을 배치하고 **content**를 마지막에 배치한다.

```html
.container or .container-fluid
  .row
    .col-opt1-opt2
      contents
    .col-opt1-opt2
      contents
  .row
    .col-opt1-opt2
      contents
    .col-opt1-opt2
      contents
```

## container

- Bootstrap은 콘텐츠를 감싸는 요소인 container를 포함해야 함
- container가 감싸고 있는 contents를 가운데 정렬
- **.container :** 반응형으로 width를 지정하고 싶을 경우
- **.container-fluid :** width를 화면의 100%로 지정하고 싶을 경우
- 두 개의 클래스를 중첩해서 사용 불가

## row

- **.row** : column을 감싸주는 역할

## column

- row에 들어가는 각각의 content
- 옵션을 지정 안 하면 블록 요소처럼 한 줄씩 차지함
- **.col-opt1-opt2**
    - option1은 size를 의미하고 option2sms row에서 차지하는 칸을 의미함
    - ⇒ option1의 size 이상일 경우, column이 row의 option2칸을 차지함을 의미. 그것보다 작을 때는 column의 가로 사이즈는 화면 전체 가로 사이즈가 됨
- 첫 번째 옵션 : xs |  sm | md | lg
    - 화면의 크기에 따라 가로 사이즈가 달라지도록 설정
    
    ![https://user-images.githubusercontent.com/44748142/190876341-7dbc1a8f-9016-466a-ae63-4484b429dfcd.png](https://user-images.githubusercontent.com/44748142/190876341-7dbc1a8f-9016-466a-ae63-4484b429dfcd.png)
    
- 두 번째 옵션 : 1개의 row를 가로로 12칸으로 나눴을 때, 몇 칸을 차지할 것인지를 숫자로 지정
    - ex) row에 4개의 columns가 있고, 모두 같은 width를 가지게 하려면, 12칸 중 3칸씩 차지하도록 class명을 col-3로 지정
- 화면의 크기가 Medium 이상일 경우 ⇒두 개의 div는 한 row에서 보여짐
    - col-md-8은 row의 8칸을 차지
    - col-md-4은 row의 4칸을 차지
- 화면의 크기가 Medium 이하일 경우 ⇒ 두 개의 div는 두개의 row로 보여짐
    - col-md-8은 화면 전체 가로사이즈 가 됨(즉, row의 12개 차지)
    - 원래 col-md-4의 역할은 사라지고, col-6로 row의 6칸을 차지

```html
<div class="container">
   <div class="row">
      <div class="col-md-8">.col-md-8</div>
      <div class="col-6 col-md-4">.col-6 .col-md-4</div>
   </div>
</div>
```

[Reference]

[https://mjmjmj98.tistory.com/19](https://mjmjmj98.tistory.com/19)
