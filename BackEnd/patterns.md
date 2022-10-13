# 디자인패턴

# MVC (Model, View, Controller)

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%2099c1386cf33f4c34872f783d75aae466/Untitled.png)

- **Model** : 데이터 (DB), 애플리케이션에서 사용되는 데이터와 그를 처리하는 부분
- **View** : Model에 포함된 데이터의 시각화 (화면), Model을 이용하여 화면을 나타냄
- **Controller** : 사용자의 입력을 받아 처리하는 부분, Model과 View의 중개자

**장점**

1. 동시다발적인 개발이 가능 (프론트엔드와 백엔드)
2. 높은 응집도
3. 개발용이성 (책임이 구분되어 있어 코드 수정이 용이)

**단점**

1. Controller가 다수의 View를 선택할 수 있어서 하는 일이 너무 많아질 수 있음
2. 코드 일관성 유지에 노력이 필요
3. View와 Model간 양방향으로 상태가 변경되었다는 정보를 주고 받음 
    
    → View와 Model 사이의 의존성이 높다
    
    → 규모가 커질수록 유지보수가 어려움
    

# **MVP (Model, View, Presenter)**

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%2099c1386cf33f4c34872f783d75aae466/Untitled%201.png)

- **Model** : 데이터를 저장하고, 처리하는 역할
- **View** : 화면을 담당, 사용자의 입력을 받음, Presenter를 이용해 데이터를 주고받기 때문에 매우 의존적
- **Presenter** : MVC의 Controller와 유사하지만, View에 직접 연결되어 1:1로 매칭되는 점이 다름

**장점**

1. Model과 View간의 결합도를 낮춰, 추가 및 수정에 대해 해당 부분만 수정하면 되기 때문에 확장성이 좋아지고, 유닛테스트시 테스트코드를 작성하기 편리
2. UI, Data각각 파트가 나눠지기 때문에 동시에 쉽고 빠르게 코딩 가능

**단점**

1. 애플리케이션이 복잡해질수록 View와 Presenter사이의 의존성이 강해지는 단점
    
    → 간단한 View를 만들더라고 Presenter를 매번 만들게 됨
    
2. MVC의 Controller처럼 Presenter도 어느정도 비대해질 수 있음
3. MVC의 단점인 View와 Model사이의 의존성은 많이 해결되지만, View와 Presenter가 1:1로 매칭되기 때문에 View가 많아짐에 따라서 Presenter도 같이 생성됨

# MVVN (Model, View, ViewModel)

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%2099c1386cf33f4c34872f783d75aae466/Untitled%202.png)

- **Model** : 데이터를 처리하는 부분
- **View** : 유저 인터페이스(UI), 사용자의 입력을 받음, HTML/CSS/XML 등으로 작성
- **ViewModel** : 상태와 연산 View의 실제 논리 및 데이터 흐름을 담당, 상태 데이터를 변경하면 즉시 View에 반영시킴

**장점**

1. MVVM 패턴은 **View**와 **Model** 사이의 의존성이 없음 (MVP와 같음)
2. Command패턴과 Data Binding을 사용하여 View와 ViewModel 사이의 의존성 또한 없앤 디자인 패턴

**단점**

1. ViewModel의 설계가 쉽지 않음

# Flux

![Untitled](%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%2099c1386cf33f4c34872f783d75aae466/Untitled%203.png)

**Flux**는 MVC모델의 단점을 보완하기 위한 아키텍쳐

1. **MVC**의 문제점
    - 양방향 데이터 흐름 → 기능이 추가 될 때마다 구조가 복잡해져서 관리하기 용이하지 않음
    
2. **Flux**로 해결
    
    장점 : 데이터의 단방향 흐름 (Dispatcher→Store→View→Dispatcher(by Action)) 으로 디버깅을 할 때에도 어디서 멈췄는지 바로바로 해결 가능, 구조의 흐름 파악하기 용이
    
    - **Dispatcher** : Flux의 모든 데이터 흐름을 관리하는 허브 역할, **Action**이 발생되면 **Dispatcher**는 전달된 **Action**을 확인하고 등록된 콜백함수를 실행하여 **Store**로 전달, (**Dispatcher**는 전체 애플리케이션에서 한 개의 인스턴스만 사용)
    - **Store** : 애플리케이션의 모든 상태변경은 **Store**에서 결정, **Dispatcher**로부터 수신받기 위해서는 **Dispatcher**에 콜백 함수를 등록해야 함, **Store**가 변경되면 **View**에 변경되었다는 사실을 알려줌
    - **View** : **View**는 화면에 나타내는 것 뿐만 아니라, 자식 **View**로 데이터를 흘러 보내는 **View** 컨트롤러의 역할도 수행
    - **Action** : **Dispatcher**에서 콜백 함수가 실행 되면 **Store**가 업데이트 되게 되는데, 이 콜백 함수를 실행 할 때 데이터가 담겨 있는 객체가 인수로 전달 되어야 함, 이 전달 되는 객체를 **Action**이라고 하는데, **Action**은 대체로 액션 생성자(**Action** creator)에서 만듦