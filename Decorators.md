### 데코레이터 개요
- [tc39/proposal-decorators](https://github.com/tc39/proposal-decorators)에 정의
- [Orthogonal Classes](https://github.com/erights/Orthogonal-Classes)와 [Class Evaluation Order](https://onedrive.live.com/view.aspx?resid=A7BBCE1FC8EE16DB!442046&app=PowerPoint&authkey=!AEeXmhZASk50KjA) 제안을 바탕으로 Decorators와 [Class Field](https://tc39.github.io/proposal-class-fields/) 및 [Private methods](https://github.com/tc39/proposal-private-methods)를 함께 작동시키는 방법에 대한 결합 된 비전을 제안

#### Orthogonal = 직교성
- **직교**란 둘 이상의 서로 다른 체계가 서로 영향을 주지 않으면서 함께 동작할 수 있는 상태나 특징을 말한다.
- 어떤 프로그램이 변경이 되도 다른 프로그램에 영향을 주지 않는 다면 서로 직교한다고 한다.
- 일종의 독립성, 결합도를 낮추는 것을 말한다.

#### Field declarations
```js
// ES2015
class Counter {
  constructor () {
    this.x = 0
  }
}

// ESnext field declarations proposal
class Counter {
  x = 0
  constructor () { }
}
```

#### Private methods and fields
```js
class Counter {
  #x = 0
  #clicked () { }
}
```