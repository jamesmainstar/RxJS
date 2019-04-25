#### 글의 목적
레이아웃을 코딩하는 방법은 다양한 방법이 있습니다.

## 그리드 시스템 구현
![스크린샷 2019-04-19 오후 6 45 16](https://user-images.githubusercontent.com/17817719/56418908-714cf080-62d3-11e9-9e57-fdc5bd1e1a4f.png)

#### Float
```html
<div style="overflow: hidden">
  <div style="width: calc((100% - 20px) * 1 / 6); float: left">1/6</div>
  <div style="width: calc((100% - 20px) * 3 / 6); float: left; margin: 0 10px">3/6</div>
  <div style="width: calc((100% - 20px) * 2 / 6); float: left">2/6</div>
</div>
```
#### Flex
```html
<div style="display: flex;">
  <div style="flex: 1">flex(1)</div>
  <div style="flex: 3; margin: 0 10px">flex(3)</div>
  <div style="flex: 2">flex(2)</div>
</div>
```
#### Grid
```html
<div style="display: grid; grid-template-columns: 1fr 3fr 2fr; grid-gap: 10px">
  <div>1fr</div>
  <div>3fr</div>
  <div>2fr</div>
</div>
```

## 슬라이드
![](https://user-images.githubusercontent.com/17817719/56421526-dd345680-62dd-11e9-8eb9-6983017959d3.png)

#### Float
```css
.float__wrapper {position: relative; height: 300px; overflow: hidden}
.float__wrapper__content,
.float__wrapper__radio,
.float__wrapper_bg {position: absolute}
.float__wrapper__content {left: 10%; bottom: 30px; width: 80%; height: 100px}
.float__wrapper__radio {z-index: 2; right: calc(10% + 20px)}
.float__wrapper_bg {left: 0; top: 0; z-index: 1; width: 100%; height: 100%}
```
```html
<div class="float__wrapper">
  <div class="float__wrapper__content">&nbsp;</div>
  <input type="radio" class="float__wrapper__radio" style="bottom: 95px">
  <input type="radio" class="float__wrapper__radio" style="bottom: 75px">
  <input type="radio" class="float__wrapper__radio" style="bottom: 55px">
  <div class="float__wrapper_bg">&nbsp;</div>
</div>
```

#### Flex
```css
.flex__wrapper {position: relative; height: 300px; display: flex; justify-content: center; align-items: flex-end; padding-bottom: 30px}
.flex__wrapper__content {width: 80%; height: 100px}
.flex__wrapper__radio,
.flex__wrapper_bg {position: absolute}
.flex__wrapper__radio {right: calc(10% + 20px); z-index: 2}
.flex__wrapper_bg {left: 0; top: 0; z-index: 1; width: 100%; height: 100%}
```
```html
<div class="flex__wrapper">
  <div class="flex__wrapper__content"></div>
  <input type="radio" class="flex__wrapper__radio" style="bottom: 95px">
  <input type="radio" class="flex__wrapper__radio" style="bottom: 75px">
  <input type="radio" class="flex__wrapper__radio" style="bottom: 55px">
  <div class="flex__wrapper_bg"></div>
</div>
```

#### Grid
```css
.grid__wrapper {
  display: grid;
  height: 300px;
  grid-template:
    '. . . .' 170px
    '. . . .' 20px
    '. . radio1 .' 20px
    '. . radio2 .' 20px
    '. . radio3 .' 20px
    '. . . .' 20px
    '. . . .' 30px
  / 10% auto 32px 10%
}
.grid__wrapper__content {grid-area: 2 / 2 / 7 / 4}
.grid__wrapper__radio {z-index: 2}
.grid__wrapper_bg {grid-area: 1 / 1 / 8 / 5; z-index: 1}
```
```html
<div class="grid__wrapper">
  <div class="grid__wrapper__content"></div>
  <input type="radio" class="grid__wrapper__radio" style="grid-area: radio1">
  <input type="radio" class="grid__wrapper__radio" style="grid-area: radio2">
  <input type="radio" class="grid__wrapper__radio" style="grid-area: radio3">
  <div class="grid__wrapper_bg"></div>
</div>
```