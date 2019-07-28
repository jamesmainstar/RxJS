### 2.2 단지 규칙일 뿐
#### 2.2.1 기본 바인딩
첫 번째 규칙은 가장 평범한 함수 호출인 '단독 함수 실행'에 관한 규칙으로 나머지 규칙에 해당하지 않을 경우 적용되는 this의 기본 규칙이다.

```js
function foo () {
  console.log(this.a)
}
var a = 2
foo() // 2
```

엄격 모드에서는 전역 객체가 기본 바인딩 대상에서 제외된다. 그래서 this는 undefined가 된다.
```js
function foo () {
  "use strict"
  console.log(this.a)
}
var a = 2
foo() // TypeError
```
#### 2.2.2 암시적 바인딩
두 번째 규칙은 호출부에 콘텍스트 객체가 있는지, 즉 객체의 소유/포함 여부를 확인하는 것이다.

```js
function foo () {
  console.log(this.a)
}
var obj = {
  a: 2,
  foo: foo
}
obj.foo() // 2
```

다음 예제처럼 객체 프로퍼티 참조가 체이닝된 형태라면 최상위/최하위 수준의 정보만 호출부와 연관된다.
```js
function foo () {
  console.log(this.a)
}
var obj2 = {
  a: 42,
  foo: foo
}
var obj1 = {
  a: 2,
  obj2: obj2
}
obj1.obj2.foo() // 42
```

##### 암시적 소실
'암시적으로 바인딩 된' 함수에서 바인딩이 소실되는 경우가 있다.
```js
function foo () {
  console.log(this.a)
}
var obj = { a: 2, foo: foo }
var bar = obj.foo
var a = 2
bar(2) // 2
```

#### 2.2.3 명시적 바인딩
this로 지정할 객체를 직접 바인딩 하므로 이를 '명시적 바인딩'이라 한다. `call()`, `apply()`, `bind()`를 사용한다.

#### 2.2.4 new 바인딩
함수 앞에 new를 붙여 생성자 호출을 하면 다음과 같은 일들이 저절로 일어난다.
1. 새 객체가 만들어진다.
2. 새로 생성된 객체의 `[[Prototype]]`이 연결된다.
3. 새로 생성된 객체는 해당 함수 호출 시 this로 바인딩 된다.
4. 이 함수가 자신의 또 다른 객체를 반환하지 않는 한 new와 함께 호출된 함수는 자동으로 새로 생성된 객체를 반환한다.

```js
function foo(a) {
  this.a = a
}
var bar = new foo(2)
console.log(bar.a) // 2
```
앞에 new를 붙여 foo()를 호출했고 새로 생성된 객체는 foo 호출 시 this에 바인딩 된다. 따라서 결국 new는 함수 호출 시 this를 새 객체와 바인딩 하는 방법이며 이것이 'new 바인딩'이다.

### 2.3 모든 건 순서가 있는 법
1. new 바인딩
2. 명시적 바인딩
3. 암시적 바인딩
4. 기본 바인딩

```js
function foo (a) {
  this.a = a
}
var obj1 = {
  foo: foo
}
var obj2 = {}

obj1.foo(2)
console.log(obj1.a) // 2

obj1.foo.call(obj2, 3)
console.log(obj2.a) // 3

var bar = new obj1.foo(4)
console.log(obj1.a) // 2
console.log(bar.a) // 4
```