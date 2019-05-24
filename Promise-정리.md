## Promise
Promise는 대기, 이행, 거부 상태가 있습니다.
- 대기 : 초기상태
- 이행 : 성공 상태, resolve(), Promise.resolve()
- 거부 : 실패 상태, reject(), Promise.reject()

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