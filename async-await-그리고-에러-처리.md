
#### async 함수
async 함수는 Promise를 반환한다.
```js
const f = async () => {}
f() // Promise
```
**정상적인 동작**으로 값을 반환하면 **then**에서 받을 수 있다.
```js
const f = async () => 'Hi!'
f().then(console.log)
```

**비정상적인 동작**으로 에러를 발생하면 **catch**에서 받을 수 있다.
```js
const f = async () => die;
f()
  .then(console.log)
  .catch(error => console.log('에러 발생!')) // 에러 발생!
```

#### async return Promise reject
#### async return Promise resolve
#### async await
#### async await reject
#### async await throw