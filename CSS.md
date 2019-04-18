### 기술정리
- [CSS 방법론](CSS-방법론)
- [CSS Flex](CSS-Flex)
- CSS Var
```css
:root {
  --main-color: #ff0;
  --main-column: 4
}
@media (min-width: 1024px) {
  :root {
    --main-color: #f00;
    --main-column: 2
  }
}
.box {
  /* Not Working! width: calc(--main-column * 100px); */
  background-color: var(--main-color)
}
.text {
  color: var(--main-color)
}
```

### 아이디어
- [Kakao i simpson | 텍스트 애니메이션](https://www.youtube.com/watch?v=fzXwGQeVNI4)