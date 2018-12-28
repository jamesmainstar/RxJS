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
```html
<ul>
  <li *ngFor="let num of number$ | async">{{num}}</li>
</ul>
<input type="button" (click)="add()" value="Add 4">
<input type="button" (click)="remove()" value="Remove 4">
```
```ts
export class AppComponent {
  update$: BehaviorSubject<Mapper> = new BehaviorSubject<Mapper>(identity);
  add$: Subject<number> = new Subject<number>();
  remove$: Subject<number> = new Subject<number>();
  number$ = this.update$.pipe(
    scan((numbers: number[], operator: Mapper) => operator(numbers), [1, 2, 3])
  );

  constructor(private todoService: TodoListService) {
    this.add$.pipe(
      map((v): Mapper => {
        return (numbers: number[]) => numbers.concat(v);
      })
    ).subscribe(this.update$)
    this.remove$.pipe(
      map((v): Mapper => {
        return (numbers: number[]) => numbers.filter(n => n !== v);
      })
    ).subscribe(this.update$)
  }

  add() {
    this.add$.next(4);
  }

  remove() {
    this.remove$.next(4);
  }
}
```

#### 참고 자료
- https://github.com/RxJS-CN/angular-rxjs-todos/blob/master/src/app/services/todo.service.ts
- https://angular.io/api/common/AsyncPipe
- https://angular.io/api/forms/FormControlDirective