### Install
```bash
$ npm init
$ npm i webpack webpack-cli -D
```
### webpack.config.js
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
### entry.js
```javascript
import { foo } from './foo'
import { bar } from './bar'

foo()
bar()
```
### bar.js
```javascript
export const bar = {
  bar () {
    console.log("bar")
  }
}
```
### foo.js
```javascript
export const foo = {
  foo () {
    console.log("foo")
  }
}
```
```bash
$ npm run build
```
```
├── dist
     └── bundle.js
```