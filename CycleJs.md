> https://cycle.js.org/ 웹사이트 번역글

- [CycleJs Streams](CycleJs-Streams)
- [CycleJs Model-View-Intent](CycleJs-MVI)

## 데이터 흐름 Dataflow

> **Your app and the external world as a circuit**

> 순환으로의 앱과 외부 세상

<p>
  <img src="https://cycle.js.org/img/cycle-nested-frontpage.svg">
</p>

> Cycle's core abstraction is your application as a pure function `main()` 
where inputs are read effects (*sources*) from the external world and 
outputs (*sinks*) are write effects to affect the external world.
These I/O effects in the external world are managed by *drivers*: plugins that handle DOM effects, HTTP effects, etc.

Cycle의 중심 추상적 개념은 애플리케이션은 순수함수인 `main()`로, 입력(Sources)은 외부에서 전달된 해석된 이펙트이고 아웃풋(Sinks)은 외부에 영향을 주는 변경된 이펙트이다. 외부세상에 I/O 효과들은 드라이브로 관리된다. 드라이브는 DOM, HTTP을 다루는 플러그인이다.

> The internals of `main()` are built using Reactive Programming primitives, which maximizes separation of concerns and provides a fully declarative way of organizing your code. The *dataflow* is plainly visible in the code, making it readable and traceable.

`main()` 내부는 최대한 분리된 관심사와 완전히 선언적인 방법으로 제공한 프리미티브 리엑티브 프로그래밍으로 만들어진다. 데이터 흐름은 읽을 수 있고 추적할 수 있는 코드로 명확히 표현된다.

## 예제 Example

```
npm install xstream @cycle/run @cycle/dom
```

```js
import {run} from '@cycle/run'
import {div, label, input, hr, h1, makeDOMDriver} from '@cycle/dom'

function main(sources) {
  const input$ = sources.DOM.select('.field').events('input')

  const name$ = input$.map(ev => ev.target.value).startWith('')

  const vdom$ = name$.map(name =>
    div([
      label('Name:'),
      input('.field', {attrs: {type: 'text'}}),
      hr(),
      h1('Hello ' + name),
    ])
  )

  return { DOM: vdom$ }
}

run(main, { DOM: makeDOMDriver('#app-container') })
```

## 함수형과 반응형 Functional and Reactive

> Functional enables "predictable" code, and Reactive enables "separated" code. Cycle.js apps are made of pure functions, which means you know they only take inputs and generate predictable outputs, without performing any I/O effects. The building blocks are reactive streams from libraries like [xstream](http://staltz.com/xstream), [RxJS](http://reactivex.io/rxjs) or [Most.js](https://github.com/cujojs/most/), which greatly simplify code related to events, asynchrony, and errors.

함수형은 예측 가능한 코드를 가능하게 하고, 반응형은 분리된 코드를 가능하게 한다. Cycle.js 앱들은 어떠한 I/O 이펙트가 없는 입력을 받으면 예측가능한 출력을 만들어내는 순수함수로 만들어진다. 빌딩 블록은 xstream, RxJs 또는 Most.js와 같은 라이브러리에서 발생하는 반응형 스트림으로, 이벤트, 비동기 및 오류와 관련된 코드를 엄청나게 단순화한다.

> Structuring the application with streams also separates concerns, because all [dynamic updates to a piece of data are co-located](streams.html#streams-reactive-programming) and impossible to change from outside. As a result, apps in Cycle are entirely `this`-less and have nothing comparable to imperative calls such as `setState()` or `update()`.

스트림이 포함된 애플리케이션 구조는 관심사를 분리한다. 왜냐하면 데이터 조각은 대한 모든 동적 업데이트는 함께 배치되어 외부에서 변경할 수 없기 때문이다.

## 간단함 그리고 간결함 Simple and Concise

> Cycle.js is a framework with very few concepts to learn. The core API has just one function: `run(app, drivers)`. Besides that, there are **streams**, **functions**, **drivers** (plugins for different types of I/O effects), and a helper function to isolate scoped components. This is a framework with very little "magic". Most of the building blocks are just JavaScript functions. Usually the lack of "magic" leads to very verbose code, but since functional reactive streams are able to build complex dataflows with a few operations, you will come to see how apps in Cycle.js are small and readable.

Cycle.js는 배우기 위해 몇가지 컨셉만 알면 된다. 중심 API는 `run(app, drivers)` 함수만 가지고 있다.
게다가 컴포넌트 범위를 격리하는 stream, functions, drivers 그리고 helper function들이 있다. 거의 "마법"이 없는 프레임워크이다. 대게 블록을 만드는 것은 자바스크립트 함수이다. 일반적으로 "마법"의 부재는 매우 장황한 코드와 연결되지만 함수형 반응형 스트림은 몇가지 오퍼레이터로 복잡한 데이터 흐름 구축할 수 있기 때문에 당신은 Cycle.js 앱이 얼마나 작고 읽기 쉬운지 알게 될 것입니다.

## 확장성과 테스트용이성 Extensible and Testable

Drivers are plugin-like simple functions that take messages from sinks and call imperative functions. All I/O effects are contained in drivers. This means your application is just a pure function, and it becomes easy to swap drivers around. The community has built drivers for [React Native](https://github.com/cyclejs/cycle-react-native), [HTML5 Notification](https://github.com/cyclejs/cycle-notification-driver), [Socket.io](https://github.com/cgeorg/cycle-socket.io), etc. Sources and sinks can be easily used as [Adapters and Ports](https://iancooper.github.io/Paramore/ControlBus.html). This also means testing is mostly a matter of feeding inputs and inspecting the output. No deep mocking needed. Your application is just a pure transformation of data.

## 명시적인 데이터 흐름 Explicit dataflow

In every Cycle.js app, each of the stream declarations is a node in a dataflow graph, and the dependencies between declarations are arrows. This means there is a one-to-one correspondence between your code and *minimap*-like graph of the dataflow between external inputs and external outputs.

<p class="dataflow-minimap">
  <img src="https://cycle.js.org/img/dataflow-minimap.svg">
</p>

```js
function main(sources) {
  const decrement$ = sources.DOM
    .select('.decrement').events('click').mapTo(-1);

  const increment$ = sources.DOM
    .select('.increment').events('click').mapTo(+1);

  const action$ = xs.merge(decrement$, increment$);
  const count$ = action$.fold((x, y) => x + y, 0);

  const vdom$ = count$.map(count =>
    div([
      button('.decrement', 'Decrement'),
      button('.increment', 'Increment'),
      p('Counter: ' + count)
    ])
  );
  return { DOM: vdom$ };
}
```

In many frameworks the flow of data is *implicit*: you need to build a mental model of how data moves around in your app. In Cycle.js, the flow of data is clear by reading your code. The dataflow graph can also be viewed in the [Cycle.js DevTool for Chrome](https://github.com/cyclejs/cyclejs/tree/master/devtool), which shows data moving in real-time through the graph:

<p>
  <img src="https://cycle.js.org/img/devtool.png" style="max-height:inherit">
</p>

## Composable

Cycle.js has components, but unlike other frameworks, every single Cycle.js app, no matter how complex, is a function that can be reused in a larger Cycle.js app.

<p>
  <img src="https://cycle.js.org/img/nested-components.svg">
</p>

Sources and sinks are the interface between the application and the drivers, but they are also the interface between a child component and its parent. Cycle.js components can be simply GUI widgets like in other frameworks, but they are not limited to GUIs only. You can make Web Audio components, network requests components, and others, since the sources/sinks interface is not exclusive to the DOM.

## Learn it in 1h 37min

<p>
  <img src="https://cycle.js.org/img/egghead.svg">
</p>

Got 1 hour and 37 minutes? That is all it takes to learn the essentials of Cycle.js. Watch [**this free Egghead.io video course**](https://egghead.io/series/cycle-js-fundamentals) given by the creator of Cycle.js. Understand Cycle.js from within by following how it is built from scratch, then learn how to transform your ideas into applications.

## Supports...

- [**Virtual DOM rendering**](https://github.com/cyclejs/cyclejs/tree/master/dom)
- [**Server-side rendering**](https://github.com/cyclejs/cyclejs/tree/master/examples/advanced/isomorphic)
- [**JSX**](http://cycle.js.org/getting-started.html)
- [**TypeScript**](https://github.com/cyclejs/cyclejs/tree/master/examples/intermediate/bmi-typescript)
- [**React Native**](https://github.com/cyclejs/cycle-react-native)
- [**Time traveling**](https://github.com/cyclejs/cycle-time-travel)
- [**Routing with the History API**](https://github.com/cyclejs/cyclejs/tree/master/history)
- [**And more...**](https://github.com/cyclejs-community/awesome-cyclejs)


[Read the docs >](getting-started.html)
