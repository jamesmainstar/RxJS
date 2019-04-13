## BEM
### 작업규칙
- 가능한 명확하게 작성
- 소문자, 숫자 조합
- 여러단어의 조합은 하이픈(-)으로 연결

### 블록
- 재사용 가능한 독립적인 페이지 구성요소
- 형태(color, size)가 아닌 목적(gnb, btn)에 맞게 결정해야 한다.
- 블록은 환경에 영향을 받지 않아야 한다. 즉, 여백이나 위치를 설정하면 안된다.
- 태그, id 선택자를 사용하면 안된다.
- 블록은 서로 중첩해서 작성 할 수 있다.
```css
.header {}
.menu {}
.search-form {}
```

### 요소
- 블록안에서 특정 기능을 담당하는 부분
- `block__element` 형태로 사용(더블 언더바)
- 형태(color, size)가 아닌 목적(item, text, title)에 맞게 결정해야 한다.
- 요소는 중첩해서 작성할 수 있다.
- 요소는 해당 블록에서만 사용할 수 있다.
```css
.header__title {}
.menu__item {}
.search-form__input {}
```

### 수식어
- 블록, 요소의 형태와 상태를 정의한다.
- `block__element--modifier`, `block--modifier` 형태로 사용(더블 하이픈)
- 수식어의 불리언 타입과 키-벨류 타입이 있다.
- 블리언 타입 : 수식어가 있으면 값이 true라고 가정한다. `form__buttom--disabled`
- 키-벨류 타입 : 키, 벨류를 하이픈으로 연결하여 표시한다. `color-red`, `theme-ocean`
- 수식어는 단독으로 사용할 수 없다. 즉 기본 블록과 요소에 추가하여 사용해야 한다.
```css
.header__title--color-red {}
.menu__item--disabled {}
.search-form__input--focus {}
```

### 혼합사용
- block1, block2__element 형태로 사용 할 수 있다.
- block2__element에 여백이나 위치를 지정하고 block1은 독립적으로 유지할 수 있다.
```html
<div class="header">
  <div class="search-form header__search-form"></div>
</div>
```

## OOCSS(Object-Oriented CSS)
### 2가지 기본원칙
- 구조와 모양을 분리 : 반복적인 시각적 기능을 별로의 **스킨**으로 정의하여 다양한 객체와 혼합하여 중복 코드없이 시각적 다양성을 표현할 수 있다.
- 콘테이너와 콘텐츠의 분리 : 스타일을 정의할 때 위치에 의존적인 스타일을 사용하지 않는다. 사물의 모양은 어디에 위치 하던지 동일하게 보인다. 