* [tc39/proposal-decorators](https://github.com/tc39/proposal-decorators)

#### 데코레이터 개요
- Orthogonal Classes와 Class Evaluation Order 제안을 바탕으로 Decorators와 Class Field 및 Private methods를 함께 작동시키는 방법에 대한 결합 된 비전을 제안
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
> Private fields
```
- 