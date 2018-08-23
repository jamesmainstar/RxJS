## [2018.08.22] 인터페이스 정의
### 용어 정리
#### Spec
- 사용자에게 노출 될 단일 인터페이스이다.
- [Descriptor](#Descriptor)와 [Exporter](#Exporter)로 이뤄진다.
- SpecWrapper를 통해 `Immutable State`를 공유한다.
> Spec.js
```js
import * as Descriptor from './Descriptor'
import * as Exporter from './Exporter'
import SpecWrapper from './SpecWrapper'

export default (state = {}) => {
  return SpecWrapper(state, {
    ...Descriptor,
    ...Exporter
  })
}
```
> SpecWrapper.js, Immutable State 처리가 되지 않은 예제
```js
export default (state, operators) => {
  const newOperators = {}
  for (const [name, cb] of Object.entries(operators)) {
    newOperators[name] = (...args) => cb(state, ...args)
  }
  return newOperators
}
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

> on.js, Immutable State 처리가 되지 않은 예제
```js
import Spec from '../Spec'
export const on = (state, eventName, listener) => {
  state[eventName] = listener
  return new Spec(state)
}
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
export const toJSON = (state) => ({...state})
```

#### Hypertext
- [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) 객체 생성 오퍼레이터
- Hypertext의 각 오퍼레이터는 `Spec`의 펙토리 메서드이며, 항상 새로운 `Spec`을 반환한다.
- `div() : Sepc`
- div, p, ...tags