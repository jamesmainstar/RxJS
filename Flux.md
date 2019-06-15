### Flux
Flux는 클라이언트 사이드 어플리케이션 아키텍쳐이다. Flux는 대형 MVC 어플리케이션에서 나타나는 데이터 간의 의존성과 연쇄적인 갱신에서 발생되는 예측하기 힘들 데이터 흐름을 올바르게 다루기 위해 만들어 졌다.
Flux는 MVC와는 다르게 단방향으로 데이터가 흐른다. 
Flux는 Action, Dispatcher, Stores, Views로 구성되며 각 부분들은 단방향으로만 데이터가 흐르게 되어 있다.

각 구성의 역할은 이렇다. Action은 사용자의 상호작용, HTTP 응답 등이 될 수 있으며 type 프로퍼티에 역할을 지정한다. Dispatcher는 모든 Action을 받으며, Stores가 콜백들 등록할 수 있다. Stores는 데이터와 비즈니스 로직을 담당하고 Views가 변경감시를 할 수 있도록 제공한다. Views는 Controller-Views-Views 형태를 이루고, Store에게 데이터를 가져와 View를 갱신한다.

데이터가 흐르게 되면 이렇게 흐르게 된다. 사용자의 상호작용이 발생되면 View는 Action에게 전달한다. Action은 서버에서 데이터를 요청하고 응답이 오면 Dispatcher에게 type과 데이터를 전파한다. Dispatcher는 모든 Stores에게 type과 데이터를 전파한다. Stores는 전달된 type이 상태와 의존이 있으면 Views change 이벤트를 전파한다. Views는 변화를 감지하고 Store에게 새로운 데이터를 가져온 뒤 모든 Views에게 새로운 데이터를 제공한다.

#### Flux 구성
##### View
- 역할: 뷰 랜더링
- 협력
  - [Input] Store에게 상태를 수신
  - [Output] Action에게 사용자의 상호작용 송신

##### Action
- 역할: 사용자 상호작용을 받아 Dispatcher가 Store에게 송신할 수 있도록 함
- 협력
  - [Input] View에게 사용자 상호작용을 수신
  - [Output] Dispatcher에게 이벤트 송신

##### Dispatcher
- 역할: Flux 어플리케이션의 중앙허브로 모든 데이터의 흐름을 관리한다.
- 협력
  - [Input] Action의 이벤트를 수신
  - [Ouput] Store의 콜백에 송신

##### Store
- 역할: 어플리케이션 내의 개별적인 도메인에서 상태와 비즈니스 로직 담당
- 협력
  - [Input] Dispatcher에게 이벤트를 수신
  - [Output] View에게 새로운 상태 송신

#### 참고
https://haruair.github.io/flux/docs/overview.html