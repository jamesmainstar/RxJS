### Vuex
Vuex는 Vue 어플리케이션의 상태 관리 아키텍쳐를 라이브러리로 제공한 것이다.
Flux, Redux, Elm 아키텍처에서 영감을 받아 Vue의 반응형 시스템을 활용하도록 특별히 고안된 라이브러리이다.
애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 예측 가능한 방식으로 상태를 변경할 수 있다.

Vuex는 Store라는 컨테이너를 제공합니다. Store는 State, Getters, Mutations, Actions, Modules로 이루어 집니다.
State는 어플리케이션의 상태를 가집니다. Getters는 State의 계산된 속성을 가질 수 있습니다.
Mutations은 State의 변경을 위한 유일한 방법입니다. Actions는 비동기 작업을 하며, 상태를 변경하기 위해 Mutations에게 전파합니다. Modules는 어플리케이션의 규모가 커질 때, State, Getters, Mutations, Actions를 분할하여 선언하는 역할을 합니다. 

#### State
Vuex는 단일 상태 트리를 가진다. 단일 객체는 어플리케이션의 모든 상태를 포함하며 원본 소스의 역할을 한다.


#### 참고문헌
https://vuex.vuejs.org/kr/