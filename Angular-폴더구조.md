```
angular
├─ e2e
│  └─ src
├─ src
│  ├─ app
│  ├─ assets
│  └─ environments
```
#### e2e
e2e 테스트 설정 파일과 테스트 코드를 포함하는 디렉토리이다.

#### src
애플리케이션 코드를 포함하는 디렉토리이다.

#### src/app
컴포넌트, 컴포넌트의 테스트 코드, 모듈을 포함하는 디렉토리이다.

#### src/assets
컴파일 되지 않은 파일과 정적 파일을 포함하는 디렉토리이다.

#### src/environments
애플리케이션의 환경 설정 파일을 포함하는 디렉토리이다.

---

Angular는 세부적인 사항은 [Style Guide](https://angular.io/guide/styleguide)를 통해서 가이드하고 있다. 

오픈빌더 서비스에서 Style Guide를 기반으로 프로젝트를 세팅했다. 하지만 몇가지의 파일의 위치에 대한 모호함으로 구조의 규칙이 위반되는 현상이 자주 발생하여 자체적으로 폴더 구조를 잡았다.

#### 문제점
1. 서비스가 헬퍼, 상태관리, 백엔드 API 연동 등 역할이 많다. 서비스 파일의 역할이 모호해지며 관리가 힘들었다.
2. 파이프, 디렉토리, 가드 등 Angular 아키텍쳐의 요소들의 위치가 모호했다.
3. FeatureModule, SharedModule, CoreModule의 모듈들의 역할을 이해하고 파일을 정의하지 않은 케이스가 빈번하게 발생했다.

#### 자체적으로 셋업한 폴더 구조
`src/app` 부분만 자체적으로 셋업을 했다.
```
├─ src
│  └─ app
│     ├─ app.module.ts
│     ├─ common
│     ├─ constant
│     ├─ decorators
│     ├─ models
│     ├─ core
│     │  ├─ core.module.ts
│     │  ├─ apis
│     │  ├─ guards
│     │  ├─ helpers
│     │  └─ services
│     ├─ modules
│     │  └─ block
│     │     ├─ block.module.ts
│     │     ├─ block.page.ts
│     │     ├─ block.page.html
│     │     ├─ pipes
│     │     ├─ constants
│     │     ├─ services
│     │     │  ├─ block.helper.ts
│     │     │  ├─ block.service.ts
│     │     │  └─ block-menu.service.ts
│     │     └─ components
│     │        ├─ block-menu.component.ts
│     │        ├─ block-menu.component.html
│     │        ├─ block-content.component.ts
│     │        ├─ block-content.component.html
│     │        └─ response
│     └─ shared
│        ├─ shared.module.ts
│        ├─ components
│        ├─ directives
│        └─ pipes
```