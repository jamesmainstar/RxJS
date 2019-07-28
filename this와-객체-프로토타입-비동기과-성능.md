## this와 객체 프로토타입
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
1. 명시적 바인딩
2. new 바인딩
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

## 비동기와 성능
### 2 콜백
콜백은 큐에서 대기 중인 코드가 처리되자마자 본 프로그램으로 '되돌아올' 목적지기 때문에 콜백이다.

#### 2.2.2 중첩/연쇄된 콜백
```js
listen('click', function handler(event) {
  setTimeout(function request() {
    ajax('http://some.url.1', function response(text) {
      if (text === 'hello') {
        handler()
      } else if (text === 'world') {
        request()
      }
    })
  }, 500)
})
```
이른 바 콜백 지옥 또는 운명의 피라미트라고도 불리는 코드다.

하지만 콜백 지옥은 중접/들여쓰기와는 무관하고 그보다 훨씬 심각한 문제를 안고 있다.

중첩이 원인일까? 비동기 흐름을 따라가기 어렵게 만드는 주범이 중첩인가? 물론 중첩이 원인 제공을 한 공범자인 건 맞다. 그러나 중첩 없이 이벤트/타임아웃/ajax 예제를 다시 써보면,
```js
listen('click', handler)

function handler(event) {
  setTimeout(request, 500)
}

function request() {
    ajax('http://some.url.1', response)
}

function response(text) {
  if (text === 'hello') {
    handler()
  } else if (text === 'world') {
    request()
  }
}
```
중첩/들여쓰기로 도배했던 이전 코드보다 알아보기는 훨씬 편하다. 하지만 콜백 지옥에 취약한 것 매한가지다.

순차적으로 이 코드를 추론하자면 한 함수에서 다름 함수로, 또 그다음 함수로, 시퀀스 흐름을 '따라가기' 위해 코드 베이스 전체를 널뛰기해야 한다.

일일이 모든 내용을 단계별로 하드 코딩하는 방법도 가능하지만 십중팔구 다른 단계나 비동기 흐름에서는 재사용할 수 없는, 매우 반복적인 코드가 낭비가 초래 될 것이다.

바로 이것이 콜백 지옥이다. 중첩/들여쓰기 같은 건 주의를 분산시키는 부수적인 요소일 뿐이다.