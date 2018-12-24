#### operator를 사용하면 항상 데이터는 불변 객체가 만들어 지나??

여기 of operator를 통해 Observable를 생성했습니다.
```js
const data$ = of({n: 1}, {n: 2}, {n: 3});
```
그리고 자신을 반환하는 함수와 제곱를 하는 함수를 pipe를 통해 받았습니다.
```js
const identity$ = data$.pipe(map(v => v));
const div$ = data$.pipe(
  map((v) => {
    v.n = v.n * v.n;
    return v;
  })
);
```
여기서 순서대로 실행하면 이와 같은 결과를 얻을 수 있습니다.

```js
data$.subscribe(console.log);
// output { n: 1 }
// output { n: 2 }
// output { n: 3 }

identity$.subscribe(console.log);
// output { n: 1 }
// output { n: 2 }
// output { n: 3 }

div$.subscribe(console.log);
// output { n: 1 }
// output { n: 4 }
// output { n: 9 }
```

하지만 순서를 뒤집에서 실행하면 아래와 같은 결과가 나오게 됩니다.

```js
div$.subscribe(console.log);
// output { n: 1 }
// output { n: 4 }
// output { n: 9 }

identity$.subscribe(console.log);
// output { n: 1 }
// output { n: 4 }
// output { n: 9 }

data$.subscribe(console.log);
// output { n: 1 }
// output { n: 4 }
// output { n: 9 }
```

누구도 `data$`를 구독했을 때 변경된 값이 나오는 것을 원하지 않을 것입니다. 여기서 알 수 있는 것은
`operator`를 사용하더라도 내부 값은 공유를 하고 있다는 것입니다. 즉, `operator`에 등록하는 함수도 모두 순수함수로 작성을 해야 합니다.