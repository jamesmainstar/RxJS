#### Flux란
- Facebook에서 클라이언트 사이드 웹 어플리케이션을 만들기 위해 사용하는 어플리케이션 아키텍쳐
- 단방향 데이터 흐름을 활용해 뷰 컴포넌트를 구성하는 React를 보완하는 역할

### Flux 구성
#### View
- 역할: 뷰 랜더링
- 협력
  - [Input] Store에게 상태를 수신
  - [Output] Action에게 사용자의 상호작용 송신

#### Action
- 역할: 사용자 상호작용을 받아 Dispatcher에게 전파
- 협력
  - [Input] View: 사용자 상호작용을 수신
  - [Output] Dispatcher에게 이벤트 송신

#### Dispatcher
- 역할: Flux 어플리케이션의 중앙허브로 모든 데이터의 흐름을 관리한다.
- 협력
  - [Input] Action의 이벤트를 수신
  - [Ouput] Store의 콜백에 송신

#### Store
- 역할: 어플리케이션 내의 개별적인 도메인에서 상태와 비즈니스 로직 담당
- 협력
  - [Input] Dispatcher에게 이벤트를 수신
  - [Output] View에게 새로운 상태 송신

#### 참고
https://haruair.github.io/flux/docs/overview.html