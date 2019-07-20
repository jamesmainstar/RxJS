### 글의 목적
서비스 개발 시 Angular를 사용중이다. AngularJs를 사용했던 경험이 있어 서비스 일원이 됬을 때 Angular에 대한 반감이 있었다. 하지만 최근들어 Angular는 Vue 못지 않게 강력하다는 것을 느끼고 있다.

내가 강력하다고 느끼는 것은 두가지이다. AngularJs부터 사용된 Angular의 아키텍쳐와 TypeScript 사용 강제성이다. Angular의 아키텍쳐에서는 코드의 볼륨을 줄이는 도구들이 제공된다. 적절하게 사용된다면 작은 단위의 코드를 만들어 조합할 수 있다. TypeScript는 컴파일 시점에 코드의 안정성을 보장해준다.

하지만 강력함속에도 아쉬운점 하나있다. AngularJs부터 사용된 Service이다. Service는 Angular에서도 메타몽(포캣몬)같은 도구이다. 무엇이든 될 수 있기 때문에 오용되기 쉽다. 

이 글에서는 Angular의 강력함과 아쉬운점을 정리해봤다.

### 목차
- TypeScript의 강력함
- Component의 볼륨을 줄여주는 강력한 도구들
  - Component가 무엇인가
  - 탬플릿 로직은 Pipe로 만들자
  - DOM의 동작은 Directive로 만들자
  - 그래도 Component가 커지면 Service로 분리하자
- Service의 역할 정의