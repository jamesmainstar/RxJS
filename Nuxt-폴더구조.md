```
nuxt
├─ assets
├─ components
├─ layouts
├─ middleware
├─ pages
├─ plugins
├─ static
├─ store
└─ test
```
#### assets
LESS, SASS, JS 같은 컴파일되지 않은 에셋들을 포함하는 디렉토리이다.

#### components
VueJs 컴포넌트를 포함하는 디렉토리이다.

#### layouts
애플리케이션의 레이아웃을 포함하는 디렉토리이다.

#### middleware
애플리케이션의 미들웨어를 포함하는 디렉토리이다. 미들웨어는 **페이지나 레이아웃이 렌더링 되기 전**에 실행할 사용자 정의 함수를 정의할 수 있다.

#### pages
애플리케이션의 뷰와 라우트를 포함하는 디렉토리이다. NuxtJs는 모든 `.vue`파일을 읽고 애플리케이션의 라우터를 생성한다.\

#### plugins
**루트 VueJs 애플리케이션이 생성되기 전**에 실행하고 싶은 자바스크립트 플러그인을 포함하는 디렉토리이다.

#### static
정적 파일들을 포함하는 디렉토리이다.

#### store
Vuex Store 파일을 포함하는 디렉토리이다. Vuex Store 옵션은 NuxtJs 프레임워크에 의해 실행되며, `index.js` 파일을 생성하면 프레임워크가 자동으로 옵션을 활성화한다.

#### test
테스트 파일을 포함하는 디렉토리이다.