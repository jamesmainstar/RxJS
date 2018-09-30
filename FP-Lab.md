#### 상태 또는 참조 삭제하기
외부 상태와 참조를 조작하는 경우가 발생하는 데, 그때는 reduce로 외부변수를 접근하는 것을 방지할 수 있다.

for문에서 외부변수인 arr를 접근하여 변경하는 경우이다.
```js
const arr = []
for (let char of '12345') {
  arr.push(char)
}
console.log(arr) // => ['1','2','3','4','5']
```

reduce를 사용하면 내부에서 모두 처리한 결과만 리턴하여 외부변수를 접근하지 않게 할 수 있다.
```js
const arr2 = reduce([...'12345'], (acc, val) => {
  acc.push(val)
  return acc
}, [])
console.log(arr) // => ['1','2','3','4','5']
```

#### map : 데이터 변경하기
map은 컬렉션의 아이템을 인자로 받은 함수를 통해 데이터를 변경한다.
map :: fn -> val -> fn(val)

#### match : 일치하면 실행하기
match는 일치하면 실행하고, 일치하지 않으면 undefined를 반환한다.
match :: fn1, fn2 -> val -> fn1(val) ? fn2(val) : undefined

#### dispatch : 값이 있을 때 반환하기
dispatch는 인자로 받은 함수를 실행해 값이 undefined가 아닐 때 반환한다.