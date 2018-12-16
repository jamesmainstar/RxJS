#### Observable
시간을 축으로 연속적인 데이터를 저장하는 컬렉션을 표현한 객체이다. Observable은 데이터를 제공하는 소스를 Observer에게 전달한다.
오퍼레이터와 함께 RxJS의 핵심중의 핵심인 개념이다. 이를 스트림이라고 부른다.

| 구분                  | Cold Observable                          | Hot Observable                                                     |
|-----------------------|------------------------------------------|--------------------------------------------------------------------|
| 데이터 주제 생성 시기 | Observable 내부                          | Observable 외부                                                    |
| Observer와의 관계     | 1:1                                      | 1:N                                                                |
| 데이터 영역           | Observer마다 독립적                      | N개의 Observer와 공유                                              |
| 데이터 전달 시점      | 구독하는 순간부터 데이터를 전달하기 시작 | 구독과 상관없이 데이터를 중간부터 전달                             |
| RxJS 객체             | Observable                               | fromEvent에 의해 생성된 Observable, ConnectableObservable, Subject |

#### Operator
Observable를 생성 및 조작하는 함수를 오퍼레이터라고 한다. 오퍼레이터는 Observable를 생성하기도 하고, 각각의 Observable을 연결하기도 한다.
또한 Observable을 분리하거나 합치기도 한다. 오퍼레이터는 현재의 Observable 인스턴스를 기반으로 항상 새로운 Observable 인스턴스를 반환한다.

#### Observer
Observable에 의해 전달된 데이터를 소비하는 주체이다. Observer는 next, error, complete 함수를 가진 객체를 가리킨다.
Observable에 의해 데이터가 전달될 때는 next 함수가 호출되고, 에러가 발생했을 때는 error 함수,
데이터를 전달이 완료되었을 때는 complete함수가 호출된다. Observer는 Observable과 subscribe 메소드를 통해 연결된다.

#### Subscription
Observable.prototype.subscribe의 반환값이다. Subscription 객체는 자원의 해제를 담당한다.
등록된 Observable의 데이터를 더이상 전달받고 싶지 않을 경우 unsubscribe 메소드를 호출하여 자원을 해제한다.

#### RxJS 개발 방법
RxJS를 사용하여 개발할 경우 프로세스는 대부분 다음과 같은 과정을 거친다.
- 첫째. 데이터 소스를 Observable로 변경한다.
- 둘째. 오퍼레이터를 통해 데이터를 변경하거나 추출한다. 또는 여러 개의 Observable을 하나의 Observable로 합치거나 하나의
Observable을 여러 개의 Observable로 만든다.
- 셋째. 원하는 데이터를 받아 처리하는 Observer를 만든다.
- 넷째. Observable의 subscribe를 통해 Observer를 등록한다.
- 다섯째. Observable 구독을 정지하고 자원을 해지한다.