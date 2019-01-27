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
const obj = { 
```