### Sub Routine Flow
```js
const routineA = _ => 1
const routineB = _ => 2

const a = routineA()
console.log(a) // 1
const b = routineB()
console.log(b) // 2
```
```
[Main Flow]
  => [Routine A] => [Routine A Sub Flow]
  <= [Routine A Return]
  => [Routine B] => [Routine B Sub Flow]
  <= [Routine B Return]
```