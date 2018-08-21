#### 컴포넌트란 무엇인가
기본 HTML 엘리먼트를 `확장`하여 `재사용` 가능한 코드를 `캡슐화`하는 데 도움이 됩니다. Vue 인스턴스 이기 때문에 `모든 옵션 객체`와 `라이프 사이클 훅`을 사용할 수 있다.

#### 컴포넌트로 어떤것을 해결하고 싶었는 지

#### `data`를 함수로 사용하는 이유
세 개의 컴포넌트 인스턴스가 모두 같은 `data` 객체를 공유하므로 하나의 카운터를 증가 시키면 모두 증가합니다.
그래서 `새로운 데이터 객체`를 반환하여 이 문제를 해결합니다.
```js
Vue.component('my-component', {
  template: '<span>{{ message }}</span>',
  data: {message: 'hello'}
})
```
```html
<div id="example-2">
  <simple-counter></simple-counter>
  <simple-counter></simple-counter>
  <simple-counter></simple-counter>
</div>
```

#### 라이프 사이클 훅