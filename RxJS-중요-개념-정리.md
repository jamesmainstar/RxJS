### Observable
시간을 축으로 연속적인 데이터를 저장하는 컬렉션을 표현한 객체이다. Observable은 데이터를 제공하는 소스를 Observer에게 전달한다.
오퍼레이터와 함께 RxJS의 핵심중의 핵심인 개념이다. 이를 스트림이라고 부른다.

Observable를 두가지 타입으로 나뉘다. 첫번째는 지금까지 우리가 사용해왔던 Observable인 Cold Observable과
두 번째는 하나의 Observable을 여러 Observable이 공유할 때 필요한 Hot Observable이다.

| 구분                  | Cold Observable                          | Hot Observable                                                     |
|-----------------------|------------------------------------------|--------------------------------------------------------------------|
| 데이터 주제 생성 시기 | Observable 내부                          | Observable 외부                                                    |
| Observer와의 관계     | 1:1                                      | 1:N                                                                |
| 데이터 영역           | Observer마다 독립적                      | N개의 Observer와 공유                                              |
| 데이터 전달 시점      | 구독하는 순간부터 데이터를 전달하기 시작 | 구독과 상관없이 데이터를 중간부터 전달                             |
| RxJS 객체             | Observable                               | fromEvent에 의해 생성된 Observable, ConnectableObservable, Subject |

### Subject
RxJS의 대표적인 Hot Observable로는 Subject가 있다. Subject는 Observable과 마찬가지로 rxjs 네임스페이스에 존재한다.
Subject는 위에서 언급한 Hot Observable과 같이 여러 Observable가 데이터를 공유한다.
뿐만 아니라 Subject는 Observable과 다르게 새로운 상태를 전달할 수 있다.

즉, Observable이 읽기 전용이라면 Subject는 읽기 쓰기가 가능한 Observable이다.

```js
const {Subject} = rxjs;
const subject = new Subject();

// observerA를 등록
subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`);
});
// 데이터 1을 전달
subject.next(1);

// observerB를 등록
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`);
});
// 데이터 2을 전달
subject.next(2);

// 결과
// "observerA: 1"
// "observerA: 2"
// "observerB: 2"
```

```js
const {Subject, Observable} = rxjs;
const subject = new Subject();
const keyup$ = fromEvent(document.getElementById('search'), 'keyup')
let [user$, reset$] = subject.pipe(partition(query => query.trim().length > 0));
user$.subscribe({ /* observer */ });
reset$.subscribe({ /* observer */ });

keyup$.subscribe(subject);
```

위와 같이 될 수 있는 이유는 Subject가 Observable을 상속하고 Observer가 구현되어 있기 때문에 가능하다. Subject는 Observable이기도 하고 Observer이기도 하다.

Subject를 연결하는 작업은 사실 좀 번거로운 작업이다. 또한 RxJS에서는 가급적이면 Subject를 외부에서 단독으로 사용하지 않기를 권고한다.
Subject는 Observable과 다르게 데이터를 변경할 수 있기 때문에 가급적이면 Subject를 구현의 내부로 감추어서 사이드 이벤트를 최소화하는 방향을 권고한다. RxJS에서는 "하나의 데이터 소스를 함께 공유한다"는 의미로 share이라는 오퍼레이터를 제공한다.

```js
const keyup$ = formEvent(document.getElementById('search'), 'keyup')
  .pipe(
    debounceTime(300),
    map(event => event.target.value)
    distinctUntilChanged(), // 특수티가 입력된 경우에 나오지 않기 위해 중복 데이터 처리
    tap(v => console.log('from keyup$', v)),
    share()
  );
```

### Operator
Observable를 생성 및 조작하는 함수를 오퍼레이터라고 한다. 오퍼레이터는 Observable를 생성하기도 하고, 각각의 Observable을 연결하기도 한다.
또한 Observable을 분리하거나 합치기도 한다. 오퍼레이터는 현재의 Observable 인스턴스를 기반으로 항상 새로운 Observable 인스턴스를 반환한다.

### Observer
Observable에 의해 전달된 데이터를 소비하는 주체이다. Observer는 next, error, complete 함수를 가진 객체를 가리킨다.
Observable에 의해 데이터가 전달될 때는 next 함수가 호출되고, 에러가 발생했을 때는 error 함수,
데이터를 전달이 완료되었을 때는 complete함수가 호출된다. Observer는 Observable과 subscribe 메소드를 통해 연결된다.

### Subscription
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