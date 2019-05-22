#### async 함수
async 함수는 Promise를 반환한다.
```js
const f = async () => {}
f() // Promise
```
**정상적인 동작**으로 값을 반환하면 **then**에서 받을 수 있다.
```js
const f = async () => 'Hi!'
f().then(console.log) // Hi!
```

**비정상적인 동작**으로 에러를 발생하면 **catch**에서 받을 수 있다.
```js
const f = async () => die;
f().catch(error => console.log('에러 발생!')) // 에러 발생!
```

#### async에서 Promise 반환
async 함수의 반환값으로 Promise를 사용하면 호출자에서는 async 함수 사용과 동일하게 사용된다.
resolve 상태면 then으로 처리되고, reject 상태면 catch에서 처리된다.
```js
const f = async () => Promise.resolve('Hi!')
f().then(console.log) // Hi!
```
```js
const f = async () => Promise.reject('Hi!')
f().catch(error => console.log('에러 발생!')) // 에러 발생!
```

#### async await
#### async await reject
#### async await throw