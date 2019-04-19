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