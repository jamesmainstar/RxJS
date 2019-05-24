#### 내부 상태
Promise는 대기, 이행, 거부 상태가 있습니다.
- 대기 : 초기상태
- 이행 : 성공 상태, resolve(), Promise.resolve()
- 거부 : 실패 상태, reject(), Promise.reject()

### 응답 결과 전달 방법
#### [Promise] Active Async Control
프로미스는 `then`을 호출해야 결과를 얻는 다.
```js
let result;
const promise = new Promise(r => $.post(url1, data1, r));
promise.then(v => {
    result = v;
});
```
```js
const promise1 = new Promise(r => $.post(url1, data1, r));
const promise2 = new Promise(r => $.post(url2, data2, r));
promise1.then(result => {
    promise2.then(v => {
        result.nick = v.nick;
        report(result);
    });
});
```
#### [Callback] Passive Async Control
콜백을 보낼 수는 있지만 언제 올지는 모른다.
```js
$.post(url. data, e=>{ // 언제 실행 되는 가 })
```

현실적으로 다수의 API 요청을 통해 결과를 만들기 때문에 언제 응답이 오는 지 중요하다.
```js
let result;
$.post(url1, data1, v => {
    result = v;
});
$.post(url2, data2, v => {
    result.nick = v.nick;
    report(result);
});
```

### 연속적인 동작
Promise는 비동기를 값으로 다룰 수 있다는 것이 큰 차이이다. 그래서 콜백으로 처리하는 함수는 리턴되는 값이 없지만 Promise로 처리하는 함수는 리턴된 Promise를 통해서 연속적인 동작을 할 수 있다.
```js
const add10 = (a, callback) => {
  setTimeout(() => callback(a + 10), 100);
};

add10(10, res => {
  add10(res, res => {
    console.log(res);
  });
});

const add20 = (a, callback) => {
  return new Promise(resolve => setTimeout(() => resolve(a + 20), 100));
};

add20(10)
  .then(add20)
  .then(console.log);
```

### Usage
#### resolve/reject
```javascript
const promise = new Promise((resolve, reject) => {
  getData(
    response => resolve(response.data), 
    error => reject(error.message)
  )
})
```
#### then / catch
```javascript
promise
  .then(data => console.log(data))
  .catch(err => console.error(err))
```
### Multiple
#### all
```javascript
Promise.all([
  getPromise(),
  getPromise(),
  getPromise()
])  //response all data
  .then(data => console.log(data))
  .catch(err => console.error(err))
```
#### race
```javascript
Promise.race([
  getPromise(), //1000ms
  getPromise(), //500ms
  getPromise() //250ms
])  //response of 250ms
  .then(data => console.log(data))
  .catch(err => console.error(err))
```

#### 참고자료
- [링크](https://www.inflearn.com/course/functional-es6#curriculum): 함수형 프로그래밍과 JavaScript ES6+ - 비동기:동시성 프로그래밍 1