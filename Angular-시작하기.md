### Angular 애플리케이션의 구성 요소
#### 모듈(Module)
모듈은 관련된 컴포넌트나 서비스, 디렉티브 등을 편하게 사용하기 위해 하나로 모은 것이다.
애플리케이션을 기능 단위로 구분하기 위해 사용한다. 모듈은 클래스에 `@NgModule` 어노테이션을 붙여서 지정하고, 이 어노테이션 안에서 모듈 내용을 설정한다.
```js
@NgModule({
  imports: [BrowserModule],
  declarations: [HelloWorldComponent],
  bootstrap: [HelloWorldComponent] // 루트 컴포넌트로 렌더링 된다.
})
export class AppModule { }
```