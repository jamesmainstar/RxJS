### 컴포넌트
#### Attribue로 적용하기
컴포넌트 셀렉터를 []를 감싸면 Attribute 로 적용가능

#### 부모 컴포넌트에서 자식 컴포넌트 접근하기
```js
class ParentComponent {
...
  @ViewChild('childRef')
  childRef: ChildComponent;

  validate() {
    ...
    this.childRef.focus();
    ...
  }
}

class ChildComponent {
  focus() {}
}
```
```html
<child-component #childRef></child-component>
```

#### Anchor preventDefault
`<a href=“#” (click)=“onClick(); false”></a>`

#### HTTPClient
- http.get은 Observable를 리턴함
  - https://angular.io/tutorial/toh-pt6#http-methods-return-one-value
- 리턴값인 Observable를 Subscribing 하여 사용
  - https://rxjs-dev.firebaseapp.com/guide/observable#subscribing-to-observables