> const, let, 화살표함수는 해당 글에서 논외이기 때문에 언급을 하지 않습니다.

this는 **호출부의 참조**이다. 호출부의 참조를 결정하는 방법은 네가지가 있다.

첫번째, 단독 함수 실행 할 경우 전역 객체가 **기본 바인딩**이 된다.
```js
function foo() {
  console.log(this.a);
}
var a = 'Hello World';
foo(); // Hello World
```

두번째, 호출부에 콘텍스트 객체가 있을 때, 객체가 **암시적 바인딩**을 한다.
```js
function foo () {
  console.log(this.a);
}
const obj = {
  a: 2019,
  foo
};
obj.foo();
```
객체 메소드를 변수에 할당 후 호출하면 **암시적 소실**이 된다.
```js
const myFoo = obj.foo;
myFoo(); // undefined
```

세번째, call, apply, bind를 사용하면 **명시적 바인딩**이 된다.
```js
function foo () {
  console.log(this.a);
}
const obj = { a: 2019 };
foo.call(obj); // 2019
foo.apply(obj); // 2019
foo.bind(obj)(); // 2019
```

네번째, new를 붙여 함수를 호출하면 생성된 객체를 this 바인딩한다.
```js
function foo () {
  setTimeout(() => {
    console.log(this.a);
  });
}
const bar = new foo();
bar.a = 2019;
```