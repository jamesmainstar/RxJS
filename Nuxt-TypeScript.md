## 개발환경세팅
### 설치 및 설정
#### NPX 설치
> [npx](https://www.npmjs.com/package/npx#description)는 `node_modules/.bin`에 설치되는 커멘드를 프로젝트 로컬에서 실행가능하도록 해주는 모듈이다.

TypeScript로 작성된 nuxt는 `npx`를 통해서만 빌드가 가능하다. 그렇기 때문에 `npx`를 설치한다.
```
npm i -g npx
```
#### Nuxt 프로젝트 설치
> [공식 가이드 문서](https://nuxtjs.org/guide/installation)를 참고한다.

nuxt를 설치하는 것은 JS로 개발할 때와 동일하다.
```
npx create-nuxt-app <project-name>
```

#### Nuxt TypeScript 설치
```
npm i -D @nuxt/typescript nuxt-property-decorator
npm i ts-node
```

#### 설정 파일 수정
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

### 개발 실행
Nuxt에서 TypeScript를 사용하기 위해서는 해당 명령어로 실행해야 한다.
```
npx nuxt
```

### 빌드
```
npx nuxt build
npx nuxt generate
```

### 빌드 실행
```
npx nuxt start
```

## TypeScript 코드 작성하기
### TypeScript로 설정하기
먼저 **주의**할 점은 `.vue`파일에 `<script>`는 `<script lang="ts">`로만 작성해야 한다. `lang="ts"`를 추가하면 IDE에서 컴포넌트를 자동으로 `import`가능하다.

### 컴포넌트 작성하기
> `v-for`를 사용하면 `:key`를 필수로 사용해야 한다.

```html
<template>
  <div class="VueToNuxtLogo">
    <template v-for="item in classes">
      <div :class="`${COMMON_CLASS} ${item}`" :key="item"></div>
    </template>
  </div>
</template>

<script lang="ts">
import Component from 'vue-class-component'
import { Vue } from 'nuxt-property-decorator'

@Component({})
class Logo extends Vue {
  COMMON_CLASS = 'Triangle'
  classes: string[] = [
    'Triangle--two',
    'Triangle--one',
    'Triangle--three',
    'Triangle--four'
  ]
}

export default Logo
</script>
```

```html
<template>
  <div class="container">
    <logo />
    <a class="button--green" @click.prevent="upCount()">
      Up
    </a>
    {{ count }}
    <a class="button--grey" @click.prevent="downCount()">
      Down
    </a>
  </div>
</template>

<script lang="ts">
import Component from 'vue-class-component'
import { Vue } from 'nuxt-property-decorator'
import Logo from '~/components/Logo.vue'

@Component({
  components: {
    Logo
  }
})
class Page extends Vue {
  count: number = 0
  upCount() {
    this.count++
  }
  downCount() {
    this.count++
  }
}

export default Page
</script>
```

### Vuex 루트에 사용하기
루트에 정의할 때는 `store/index.ts`에 `state`, `mutations`, `getters`, `actions`를 정의한다.
```ts
export const state = () => ({
  count: 0
})

export const mutations = {
  upCount(state) {
    state.count++
  },
  downCount(state) {
    state.count--
  }
}
```

컴포넌트에서는 데코레이터만 붙이면 사용가능하다.
```ts
class Page extends Vue {
  @State count
  @Mutation upCount
  @Mutation downCount
}
```

### Vuex 모듈 모드 사용하기
모듈 모드로 정의할 때는 `store`에 다른 파일을 정의한다. 파일 내부에는 `state`, `mutations`, `getters`, `actions`를 정의한다.
```ts
// page.ts
export const state = () => ({
  count: 0
})

export const mutations = {
  upCount(state) {
    state.count++
  },
  downCount(state) {
    state.count--
  }
}
```

컴포넌트에서 사용할 때는 모듈을 접근해서 사용한다.
```ts
class Page extends Vue {
  @State((state) => state.page.count)
  count
  @Mutation('page/upCount')
  upCount
  @Mutation('page/downCount')
  downCount
}
```

### 태스트