```css
.wrap {
  width: 200px;
  position: relative;
  background-color: #f9f9f9;
}

.wrap textarea {
  position: absolute;
  width: 100%;
  height: 100%;
  padding: 0;
}

.wrap .shadow {
  visibility: hidden;
  opacity: 0;
  word-break: break-all;
}

.wrap textarea,
.wrap .shadow {
  font-size: 20px;
  line-height: 120%;
}
```
```html
<div class="wrap">
  <textarea onkeyup="onChange(this)"></textarea>
  <div class="shadow">&nbsp;</div>
</div>
```
```js
function onChange({value}) {
  document.querySelector('.shadow').innerHTML = `&nbsp;${value}`;
}
```