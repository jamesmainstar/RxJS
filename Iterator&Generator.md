## Iterator
내부 표현부를 노출하지 않고 어떤 객체 집합에 속한 원소들을 순차적으로 접근할 수 있는 방법을 제공하는 패턴이다.

### Iterable Protocol
순차적으로 접근할 수 있는 Iterator를 접근하기 위한 프로토콜

Java에서 Iterator를 구현할 때는 hasNext/next 인터페이스를 사용하지만 Javascript에서는 next만 사용된다.

죵료된 것은 done property가 true일 때로 확인 가능하다.
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
Object는 Iterable 하지 않지만 Iterator/Iterable Protocol를 통해 Iterable 하게 만들 수 있다.
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
### Using Generator
```javascript
const obj = {
  name: 'Smith',
  age: 20,
  weight: 60
}

obj[Symbol.iterator] = function* () {
  const arr = Object.keys(obj)
  yield obj[arr.pop()]
  yield obj[arr.pop()]
  yield obj[arr.pop()]
}

console.log([...obj]) // [60, 20, 'Smith']
```
### Iterable data sources
Arrays, Maps, DOM queies, Strings, Sets, Arguments

## Generator
`yield`로 `Iterator`를 쉽게 정의하여 `Iterable`를 쉽게 만들 수 있음. `코루틴`을 지원함.

### 코루틴
- 실행 지점을 코드 블럭으로 저장하여, 해당 지점을 실행/중단/재시작을 할 수 있다.
- 그래서 자발적/주기적으로 유휴상태를 만들 수 있기 때문에 비선점 멀티태스킹이 가능하다.
- `동시성`과 `병렬 처리`가 가능하다.
- 코루틴 사이의 전환은 `컨텍스트 전환`이 발생하지 않음.
  - 컨텍스트 전환 : 프로세스나 스레드의 상태를 저장하는 프로세스, 나중에 복원하고 동일한 시점에서 실행 가능.
#### 비교
- 서브 루틴 : `Caller`가 호출되면 `Caller`에게 항상 `return`을 한다.
- 스레드 : `선점식 멀티태스킹`을 한다. 즉 `동시성`은 제공하만 `병렬 처리`는 제공하지 않는다.
- 재귀 : 반복적인 호출을 위해 새로운 `스택 프레임`이 필요하다.

### function*
```javascript
function* genFour () {
  yield 1
  yield 2
  yield 3
  return 4
}
let four = getFour()
```
### Generators are both an iterator and an iterable.
```javascript
four.next() // Object { value: 1, done: false)
four.next() // Object { value: 2, done: false)
four.next() // Object { value: 3, done: false)
four.next() // Object { value: 4, done: true)

[....getFour()] // Array [1, 2, 3, 4]
```
### yield* yields every yield inside a called generator
```javascript
function* flatten(arr){
  for (let x of arr) {
    if (x instanceof Array){
      yield* flatten(x)
    } else {
      yield x
    }
  }
}
let t = flatten([1, 2, [3, 4]])
```