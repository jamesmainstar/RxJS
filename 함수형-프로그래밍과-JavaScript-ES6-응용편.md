#### while을 range로
```js
function f3 (end) {
  let i = 0;
  while (i < end) {
    console.log(i)
    i++
  }
}
f3(10)
```
```js
function f3 (end) {
  return L.range(end)
}
```

#### 부수효과를 each로 구분
each를 사용하게 되면 부수효과를 일으키는 것이 명확하다.
그래서 each를 사용하는 **부수효과 블럭**과 **순수한 블럭**을 구분해서 작성해야 한다.

```js
// Not Cool
function f3 (end) {
  return _.each(console.log, L.range(end))
}

// Cool
function f3 (end) {
  return _.go(
    L.range(end),
    _.each(console.log)
  )
}
```

#### `reduce + 복잡한 함수 + add` 보다 `map + 간단한 함수 + reduce`
```js
const users = [
  { name: 'AA', age: 12 },
  { name: 'BB', age: 15 },
  { name: 'CC', age: 17 },
]
```
```js
// Not Cool
_.reduce((total, u) => total + u.age, 0, users)

// Cool
const add = (a, b) => a + b;
const ages = L.map(({age}) => age)
_.reduce(add, ages(users))
```