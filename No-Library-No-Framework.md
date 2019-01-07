#### 바닐라
- [jQuery 바닐라로 구현](http://youmightnotneedjquery.com/)
- [You Dont Need Lodash Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore)
- [You Dont Need Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs)
- [Slider](http://meandmax.github.io/lory/)
- [JS Animation](https://javascript.info/js-animation)

#### SVG Parser
```js
const parseSVG = (template) => {
  var tmp = document.createElementNS('http://www.w3.org/2000/svg', 'svg')
  tmp.innerHTML = template
  return tmp.children[0]
}
```