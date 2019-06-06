#### Flux란
- Facebook에서 클라이언트 사이드 웹 어플리케이션을 만들기 위해 사용하는 어플리케이션 아키텍쳐
- 단방향 데이터 흐름을 활용해 뷰 컴포넌트를 구성하는 React를 보완하는 역할

### Flux 구성
#### View
- 역할: 데이터를 뷰에 표시
- 협력
  - [Input] Store: 변경된 데이터 수신
  - [Output] Action: 사용자의 상호작용 전파

#### Action
- 역할: 사용자 상호작용을 받아 Dispatcher에게 전파
- 협력
  - [Input] View: 사용자 상호작용을 받음
  - [Output] Dispatcher: 이벤트 전파

#### Dispatcher
- 역할: Action에게 받은 이벤트를 Store에게 전파
- 협력
  - [Input] Action: 이벤트 전파
  - [Ouput] Store: 이벤트 전파

#### Store
- 역할: 데이터와 비즈니스 로직 담당
- 협력
  - [Input] Dispatcher: 이벤트 전파
  - [Output] View: 데이터 전달