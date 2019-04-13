## SMACSSS(Scalable and Modular Architecture for CSS)
### 정의
- CSS에 대한 확장형 모듈시 구조
- CSS의 프레임워크가 아닌 하나의 스타일 가이드

### 사용목적
- Class명을 통한 예측
- 재사용
- 쉬운 유지보수
- 확장 가능

### 핵심 규칙 분류
#### Base
- 기본 스타일(Reset, Default, Variables, Mixins)
- 기본 스타일에는 !important를 쓸 필요가 없다.
```css
* {margin:0; padding:0}
ul, ol {list-style:none}
```

#### Layout
- 레이아웃과 관련된 스타일 정의
- class명에 Prefix `l-`를 붙인다.
```css
.l-content { width: 600px; margin-right: 10px }
.l-aside { width: 20% }
```

#### Module(Components)
- 모듈 관련 스타일
- 스타일 재사용을 위한 요소
- Block, Element, Module
- 재사용을 위한 id셀렉터와 element를 사용하지 않는 다.
- 만약, element 셀렉터를 사용해야 한다면, `.box > span` 처럼 child 셀렉터를 사용한다.
```css
.box {}
.box > span {}
```

#### State
- 상태를 나타내는 스타일
- Hidden, expend, active, hover 등의 상태에서 사용
- class명에 Prefix `is-`를 붙여서 사용
```css
.btn {}
.btn.is-active {}
```
```html
<button class="btn is-active">버튼</button>
```

#### Theme
- 사이트 전반적 look and feel 제어
- 색상이나 이미지를 불변하는 스타일과 분리, 기존 스타일을 재선언하여 사용할 수 있다.
- 적용범위가 넓은 테마는 `theme-`를 붙여서 사용한다.
```css
.theme-color {}
```