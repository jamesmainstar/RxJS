#### Yield 동작 과정 및 조건
- 실행 우선 순위는 내부함수가 가장 높고 감싸고 있는 함수가 한단계씩 줄어든다.
- `yield`가 없을 경우 다름 루틴으로 이동한다.
- `yield`가 실행되면 `코드 블럭`에 위치가 저장되고, 해당 루틴에서 빠져나온다.
- 저장된 코드 블럭이 없으면 종료된다.
- `for...of` 또한 실행할 때 마다 `yield`를 호출하여 위치를 저장한다.

```js
function* odd(arr) {
  for (const v of arr) {
    console.log(`odd ${v}`)
    if (v % 2) {
      yield v
    }
  }
}

function* take(arr, n) {
  let count = 0
  for (const v of arr) {
    console.log(`take ${v}`)
    count++
    yield v
    if (count === n) {
      break;
    }
  }
}
```
```js
console.log(...take(odd(arr)), 2))

// for...of[0] odd
// for...of[1] odd[yield] take(2)[yield]
// for...of[2] odd
// for...of[3] odd[yield] take(2)[yield]

console.log(...take(odd(take(arr, 5)), 2))

// for...of[0] take(5)[yield] odd
// for...of[1] take(5)[yield] odd[yield] take(2)[yield]
// for...of[2] take(5)[yield] odd
// for...of[3] take(5)[yield] odd[yield] take(2)[yield]

console.log(...odd(take(odd(take(arr, 5)), 2)))

// for...of[0] take(5)[yield] odd
// for...of[1] take(5)[yield] odd[yield] take(2)[yield] odd[yield]
// for...of[2] take(5)[yield] odd
// for...of[3] take(5)[yield] odd[yield] take(2)[yield] odd[yield]
```

루프가 종료되고 저장된 코드 블럭이 없기 때문에 `take(5)` `odd`만 실행되고, 이것들을 감싸고 있는 `take(2)` `odd`는 실행되지 않는 다.
```js
function* odd(arr) {
  for (const v of arr) {
    console.log(`odd ${v}`)
  }
}

function* take(arr, n) {
  let count = 0
  for (const v of arr) {
    console.log(`take(${n}) ${v}`)
    count++
    yield v
    if (count === n) {
      break;
    }
  }
}

const arr = [0,1,2,3,4,5]

console.log(...odd(take(odd(take(arr, 5)), 2)))

// for...of[0] take(5)[yield] odd
// for...of[1] take(5)[yield] odd
// for...of[2] take(5)[yield] odd
// for...of[3] take(5)[yield] odd
// for...of[4] take(5)[yield] odd
```