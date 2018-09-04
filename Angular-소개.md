### 프레임워크과 라이브러리
**프레임워크**를 사용하면 프레임워크에서 제공하는 설계 구조를 사용하며 그 구조에 어울리는 방식으로 코드를 작성해야 한다.

**라이브러리**는 컴포넌트와 API를 중심으로 기능을 제공하며 어떠한 코드라도 필요에 맞춰서 사용할 수 있다.

### Angular 살펴보기
#### SystemJS
- 모듈 로더
- ES6 모듈 문법 사용
- systemjs.config.js 파일은 SystemJS의 설정 파일
```html
<html>
<head>
  <script>
    System.import('app').catch((err) => console.error(err))
  </script>
</head>
<body>
  <app></app>
</body>
</html>
```

#### @NgModule : 모듈 선언
#### @Component
```js
@Component({
  selector: 'search-product',
  template: `
    <form>
      <div>
        <input id="prodToFind" #prod>
        <button (click)="findProduct(prod.value)">Find Product</button>
        Product name: {{ product.name }}
      </div>
    </form>
  `
})
class SearchComponent {
  @Input () productID : number;
  product : Product; // Product 클래스의 내용은 생략한다.
  findProduct (prodName : string) {
  }
}
class Product {
  id : number,
  name : string;
  description : string;
  bid : number;
  price : number;
}
```