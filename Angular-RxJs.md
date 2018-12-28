### Observable 탬블릿 바인딩
#### ngFor
```js
number$ = of([1, 2, 3])
```
```html
<ul>
  <li *ngFor="let num of number$ | async">{{num}}</li>
</ul>
```
#### ngIf
```js
number$ = of([1, 2, 3]);
size$ = this.number$.pipe(map(v => v.length));
```
```html
<ul *ngIf="size$ | async">
  <li *ngFor="let num of number$ | async">{{num}}</li>
</ul>
<div *ngIf="!(size$ | async)">Empty</div>
```
#### Template
```html
Size: {{size$ | async}}
```
### 사용자 이벤트

#### 참고 자료
- https://github.com/RxJS-CN/angular-rxjs-todos/blob/master/src/app/services/todo.service.ts
- https://angular.io/api/common/AsyncPipe
- https://angular.io/api/forms/FormControlDirective