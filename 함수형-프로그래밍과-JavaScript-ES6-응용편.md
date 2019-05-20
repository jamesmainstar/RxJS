#### while을 range로
```js
function f3 (end) {
  let i = 0;
  while (i < end) {
    console.log(i)
    i++
  }
}
f3(10)
```

```js
function f3 (end) {
  return L.range(end)
}
```