* [tc39/proposal-decorators](https://github.com/tc39/proposal-decorators)

#### 데코레이터 개요
- [Orthogonal Classes](https://github.com/erights/Orthogonal-Classes)와 [Class Evaluation Order](https://onedrive.live.com/view.aspx?resid=A7BBCE1FC8EE16DB!442046&app=PowerPoint&authkey=!AEeXmhZASk50KjA) 제안을 바탕으로 Decorators와 [Class Field](https://tc39.github.io/proposal-class-fields/) 및 [Private methods](https://github.com/tc39/proposal-private-methods)를 함께 작동시키는 방법에 대한 결합 된 비전을 제안
> Field declarations
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
> Private methods and fields
```js
class Counter {
  #x = 0
  #clicked () { }
}
```