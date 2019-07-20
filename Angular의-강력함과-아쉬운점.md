### 글의 목적
서비스 개발 시 Angular를 사용중이다. AngularJs를 사용했던 경험이 있어 서비스 일원이 됬을 때 Angular에 대한 반감이 있었다. 하지만 최근들어 Angular는 Vue 못지 않게 강력하다는 것을 느끼고 있다.

내가 강력하다고 느끼는 것은 두가지이다. AngularJs부터 사용된 Angular의 아키텍쳐와 TypeScript 사용 강제성이다. Angular의 아키텍쳐에서는 코드의 볼륨을 줄이는 도구들이 제공된다. 적절하게 사용된다면 작은 단위의 코드를 만들어 이해하기 쉬운 코드를 작성가능하다. TypeScript는 컴파일 시점에 코드의 안정성을 보장해준다. 코딩할 때마다 TypeScript가 안정성을 보장해주기 때문에 비서를 둔 듯한 느낌이 들었다.

하지만 강력함속에도 아쉬운점 하나있다. AngularJs부터 사용된 Service이다. Service는 Angular에서도 메타몽(포캣몬)같은 도구이다. 무엇이든 될 수 있기 때문에 오용되기 쉽다. AngularJs, Angular를 사용하는 프로젝트를 했을 때 항상 Service에서 오용이 발생되었다.

그래서 이 글에서는 지금까지 느꼈던 Angular의 강력함과 아쉬운점을 정리해봤다.

### 목차
- TypeScript의 강력함
- Angular의 강력한 Component의 볼륨을 줄여주는 도구들
  - 일단 Component가 무엇인가
  - 탬플릿만 사용되는 로직은 Pipe로 만들자
  - DOM의 동작은 Directive로 만들자
  - 그래도 Component가 커지면 Service로 분리하자
- Angular의 메타몽인 Service
  - 왜 오용이 발생되는 가
  - 오용을 예방하려면 어떻게 해야 할까

### TypeScript의 강력함
TypeScript는 사용한지 10개월 정도 됐는 데, 초기에 서비스 투입이 됐을 때 TypeScript를 어렵게만 느껴졌다. Javascript와 다르게 타입을 정의해야 하고 interface, type, enum 을 언제 사용해야 하는 지 익숙하지 않았기 때문이다.

요세들어서는 TypeScript 사용은 필수라고 생각하고 있다. 나는 TypeScript를 비유적으로 비서라는 표현을 사용한다. 나의 시간과 기억의 한계를 TypeScript가 해결해주고 있기 때문이다. 내가 느끼기엔 두 가지의 역할을 잘해주고 있다고 생각한다.

첫 번째는 스펙을 알려준다. 메소드의 인자의 값이 어떤 타입을 사용하는 지 알려준다. 타입은 string, number, boolean뿐만 아니라 사용자 정의형인 interface, type, enum을 사용했을 때 굉장히 좋은 결과를 가져다 준다.

Javascript로 작성했을 때는 코드를 분석해야 인자의 자세한 정보를 알 수 있다. 
movieTicket는 movie, startTime, endTime, count, seats, watched의 프로퍼티를 가진다.
```js
const movieInfo = movieTicket => {
  const {movie, startTime, endTime} = movieTicket
  return `${movie}(${startTime}~${endTime})`
}

const ticketInfo = movieTicket => {
  const {count, seats, watched} = movieTicket
  return `수량: ${count}, 좌석: ${seats.join(',')}<br>
  관련 여부: ${watched ? '관람' : '미관람'}`
}
```

하지만 TypeScript를 사용하면 인자의 타입으로 인자의 자세한 정보를 알 수 있다.
```ts
interface MovieTicket {
  movie: string // 관람 영화명
  count: number // 티켓 수량
  startTime: string // 상영 시작 시간
  endTime: string // 상영 종료 시간
  seats: string[] // 좌석 정보
  watched: boolean // 관람 여부
}

const movieInfo = (movieTicket: MovieTicket) => {
  const {movie, startTime, endTime} = movieTicket
  return `${movie}(${startTime}~${endTime})`
}

const ticketInfo = (movieTicket: MovieTicket) => {
  const {count, seats, watched} = movieTicket
  return `수량: ${count}, 좌석: ${seats.join(',')}<br>
  관련 여부: ${watched ? '관람' : '미관람'}`
}
```

두 번째는 안정성 보장이다.


### Angular의 강력한 Component의 볼륨을 줄여주는 도구들
#### 일단 Component가 무엇인가
#### 탬플릿만 사용되는 로직은 Pipe로 만들자
#### DOM의 동작은 Directive로 만들자
#### 그래도 Component가 커지면 Service로 분리하자
### Angular의 메타몽인 Service
#### 왜 오용이 발생되는 가
#### 오용을 예방하려면 어떻게 해야 할까