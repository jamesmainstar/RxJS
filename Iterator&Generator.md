### Iterable Protocol
순차적으로 접근할 수 있는 Iterator Protocol를 접근하기 위한 엑세스 포인트를 정의할 수 있는 프로토콜
```javascript
const str = "hi"
const iterator = str[Symbol.iterator]()

console.log(iterator.next()) //{ value: 'h', done: false }
console.log(iterator.next()) //{ value: 'i', done: false }
console.log(iterator.next()) //{ value: undefined, done: true }
```

### Iterator Protocol
데이터를 순차적으로 접근할 때 실행되는 프로토콜

```javascript
function makeIterator(array){
  var nextIndex = 0;

  return {
    next: function(){ //next 메소드를 가져야 함
      return nextIndex < array.length ?
        {value: array[nextIndex++], done: false} :
        {done: true};
         //done : iterator의 반복 작업 종료 유무. boolean 사용
         //value : iterator로 부터 반환되는 값, done이 true일 때 생략 가능
      }
  };
}

var it = makeIterator(['yo', 'ya']);

console.log(it.next().value); // 'yo'
console.log(it.next().value); // 'ya'
console.log(it.next().done); // true
```

### Customize Iterables
```javascript
const obj = {
  name: 'Smith',
  age: 20,
  weight: 60
}

console.log([...obj]) //TypeError

obj[Symbol.iterator] = () => {
  const arr = Object.keys(obj)
  return {
    next () {
      return arr.length > 0 ?
        { value: obj[arr.pop()], done: false } :
        { done: true }
      }
    }
}

console.log([...obj]) // [60, 20, 'Smith']
```