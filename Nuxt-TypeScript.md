## 개발환경세팅
### 설치
#### NPX 설치
```
npm i -g npx
```
#### Nuxt 프로젝트 설치
> [공식 가이드 문서](https://nuxtjs.org/guide/installation)를 참고한다.

```
npx create-nuxt-app <project-name>
```

#### Nuxt TypeScript 설치
```
npm i -D @nuxt/typescript nuxt-property-decorator
npm i ts-node
```
TypeScript 설정파일을 만든다.
```
touch tsconfig.json
```
nuxt 명령어를 실행하여 `tsconfig.json`를 업데이트한 뒤 종료한다.
```
npx nuxt
```
nuxt 타입을 IDE에서 자동완성을 할 수 있도록 `tsconfig.json`에 `@nuxt/config`을 추가한다.
```diff
  "types": [
    "@types/node",
    "@nuxt/vue-app",
+   "@nuxt/config"
  ]
```

#### 설정파일을 TypeScript로 변경
`nuxt.config.js`를 `nuxt.config.ts`로 변경한다. 그리고 아래와 같이 설정 파일을 변경한다.

```ts
import NuxtConfiguration from '@nuxt/config'

const config: NuxtConfiguration = {
  // Type or Press `Ctrl + Space` for autocompletion
}

export default config
```

### 실행
Nuxt에서 TypeScript를 사용하기 위해서는 해당 명령어로 실행해야 한다.
```
npx nuxt
```

## TypeScript 코드 작성하기

### TypeScript로 컴포넌트 작성하기
먼저 **주의**할 점은 `.vue`파일에 `<script>`는 `<script lang="ts">`로만 작성해야 한다. `lang="ts"`를 추가하면 IDE에서 컴포넌트를 자동으로 `import`가능하다.

