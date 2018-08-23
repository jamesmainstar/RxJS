## [2018.08.22] 인터페이스 정의
### 용어 정리
#### Spec
[Descriptor](#Descriptor)와 [Exporter](#Exporter)로 이뤄진 단일 인터페이스이다.

#### Descriptor
- on, className, ... attributes

#### Exporter
- toJSON, toDOM, toString

#### Hypertext
- [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) 객체 생성 오퍼레이터
- Hypertext의 각 오퍼레이터는 `Spec`의 펙토리 메서드이며, 항상 새로운 `Spec`을 반환한다.
- div, p, ...tags