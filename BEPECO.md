## [2018.08.22] 인터페이스 정의
### 용어 정리
#### Spec
[Descriptor](#Descriptor)와 [Exporter](#Exporter)로 이뤄진 단일 인터페이스이다.
```js
export * from './Descriptor'
export * from './Exporter'
```

#### Descriptor
- [Hypertext](#Hypertext)의 속성을 정의한다.
- Descriptor의 각 오퍼레이터는 [Spec](#Spec)의 펙토리 메서드이며, 항상 새로운 [Spec](#Spec)을 반환한다.
- `on(eventName: String, handle: Function) : Spec`

> Descriptor.js
```js
export { on } from './on'
export { className } from './className'
export { chlidren } from './chlidren'
```

> on.js
```js
export const on = () => new Spec()
```

#### Exporter
- [Hypertext](#Hypertext)를 데이터 타입으로 변환해주는 오퍼레이터를 제공한다.
- `toString() : String`, `toJSON() : Object`, `toDOM() : HTMLElement`
- toJSON, toDOM, toString
> Exporter.js
```js
export { toJSON } from './toJSON'
export { toDOM } from './toDOM'
export { toString } from './toString'
```
> toJSON.js
```js
export const toJSON = () => {}
```

#### Hypertext
- [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) 객체 생성 오퍼레이터
- Hypertext의 각 오퍼레이터는 `Spec`의 펙토리 메서드이며, 항상 새로운 `Spec`을 반환한다.
- `div() : Sepc`
- div, p, ...tags