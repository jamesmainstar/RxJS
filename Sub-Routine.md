### Sub Routine Flow
- Sub Routine remember Return point
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

### Communicate with routine
- Main routine communicate by Arguments with Sub routine
- Sub routine communicate by Return with Main routine
```
[Main Flow]
  => [Routine A Arguments] => [Routine A Sub Flow]
  <= [Routine A Return]
```

### Sub Routine in Sub Routine
- When Routine have Sub Routine, Routine have to remember Keep Point
```
[Main Flow]
  => [Routine A]
      => [Routine B]
      <= [Routine B Return]
  <= [Routine A Return]
```