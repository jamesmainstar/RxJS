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

#### Throttle
연속적으로 콜백 실행 요청되어도, 지정된 시간 주기로 콜백이 실행하는 기법
Throttle 기법을 사용하면 일정한 시간을 주기로 콜백을 실행 할 수 있다.
```js
/**
 * Throttle
 * 
 * @param callback {Function} Callback function
 * @param _threshhold {Number} Throttle time
 * @return {Function} Event Listener
 */
function throttle(callback, _threshhold){
	var timer = null;
	var threshhold = _threshhold || 100;
	var last = 0;

	return function () {
		var self = this;
		var now = +new Date;
		var args = arguments;

		if (last && now < last + threshhold){
			clearTimeout(timer);

			timer = setTimeout(function () {
				last = now;
				callback.apply(self, args);
			}, threshhold);
		} else {
			last = now;
			callback.apply(self, args);
		}
	};
}
```

#### Debounce
다수의 이벤트 실행을 방지하기 위해 하나로 그룹화하여 특정 시간이 지난 후 실행되는 기법
여러개의 이벤트가 과다하게 사용이 되었을 때 부하를 줄여주는 역할을 한다.
```js
/**
 * Debounce
 * 
 * @param callback {Function} Callback function
 * @param _delay {Number} Delay time
 * @return {Function} Event Listener
 */
function debounce(callback, _delay){
	var timer = null;
	var delay = _delay || 100;

	return function(){
		var self = this;
		var args = arguments;
		clearTimeout(timer);
		timer = setTimeout(function () {
			callback.apply(self, args);
		}, delay);
	};
}
```