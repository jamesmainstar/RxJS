### Install
```bash
$ mkdir hello-webpack
$ cd hello-webpack
$ npm init
$ npm i webpack webpack-cli -D
```
### Getting start
#### webpack.config.js
```javascript
const path = require('path')

module.exports = {
  entry: './entry.js',
  output: {
    path: path.resolve(__dirname,'dist'),
    filename: 'bundle.js'
  }
}
```
#### 샘플 코드 만들기
##### entry.js
```javascript
import { foo } from './foo'
import { bar } from './bar'

foo()
bar()
```
##### bar.js
```javascript
export const bar = {
  bar () {
    console.log("bar")
  }
}
```
##### foo.js
```javascript
export const foo = {
  foo () {
    console.log("foo")
  }
}
```
#### build
##### package.json 에 `build`명령어 추가
```
"scripts": {
  "build": "webpack --config webpack.config.js"
}
```
##### webpack build
```bash
$ npm run build
```
```
├── dist
     └── bundle.js
```
### 웹팩 컨셉
#### 요약
* Entry : 웹팩 빌드 시작점
* Output : 웹팩 빌드 결과물 만들어지는 곳
* Loaders : .js 확장자 이외 파일이 import를 통해 사용될 때 전용 로더를 사용해야함. 예를 들어 .txt 파일을 raw-loader를 사용함
* Plugins : 코드 최적화를 하고 싶을 때 사용

#### Entry
- entry point는 웹팩 빌드의 시작점이다.
- 모듈과 의존성이 있는 라이브러리들을 계산해 내부적인 종속성 그래프를 만든다
- String으로 단일 파일을 Entry로 지정할 수 있고, Array / Object Literal를 통해 2개 이상의 Entry 를 만들수 있다.

#### Output
- 웹팩 빌드의 결과물을 지정한다.
- 빌드 결과물의 파일명을 지정한다.

#### Loaders
- webpack.config.js에 작성할 때 `module`이라는 프로퍼티명을 사용한다.
- 로더는 자바스크립트 파일이외 다른 파일을 처리할 수 있게 도와주는 역할을 한다.
- 로더를 사용하지 않으면 웹팩은 자바스크립트만 사용가능하다
```javascript
module.exports = {
  entry: './entry.js',
  output: {
    path: './dist',
    filename: 'bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
}
```
- rules[].test 는 변환될 파일들을 찾는다.
- rules[].use 는 변환을 위해 사용할 로더를 설정한다.
- 위 설정은 이렇게 해석할 수 있다. `import로 .txt파일을 사용할 경우 raw-loader를 사용해서 변환하라`

#### Plugins
- 로더보다 광범위한 역할을 한다.
- 성능 최적화와 코드 최소화 작업을 할 수 있다.
- webpack.config.js 파일에 require()를 통해 읽어온 뒤 new operator를 통해 정의해서 사용한다.
``` javascript
const webpack = require('webpack')
module.exports = {
  ..., //entry, output, module
  plugins: [
    new webpack.optimize.UglifyJsPlugin()
  ]
}
```