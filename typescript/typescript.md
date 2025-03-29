---
description: 튜토리얼 SDK 웰컴토스트의 어드민 페이지를 TypeScript로 마이그레이션한 과정을 담은 글입니다.
icon: tree-palm
---

# 웰컴토스트 어드민 TypeScript 이사하기

### 0. 왜 TypeScript로 마이그레이션해?

* 타입 안정성
* 내가 입사하고 싶은 회사에 기여하기



### 01. 초기 설정으로 시작하기

````
```shellscript
npm install -D typescript @types/react @types/react-dom @types/node
npm install -D @typescript-eslint/parser @typescript-eslint/eslint-plugin
```
````

TS 마이그레이션을 위해 먼저 초기 세팅이 필요했다. 필요한 의존성을 먼저 설치해주어야 하는데, 여러 의존성이 추가로 필요하다.

<details>

<summary><code>typescript</code> 외 다른 의존성은 역할이 뭘까?</summary>

| 의존성                              | 역할                                                  | 없으면? |
| -------------------------------- | --------------------------------------------------- | ---- |
| typescript                       | TypeScript 언어 자체이자, 컴파일러(tsc)를 제공하는 Core한 대장 패키지    |      |
| @types/react                     | React 라이브러리에 대한 TypeScript 타입 정의해주는 파일              |      |
| @types/react-dom                 | React DOM 라이브러리에 대한 TypeScript 타입 정의해는 파일           |      |
| @types/node                      | Node.js 환경에서 사용되는 API에 대한 TypeScript 타입 정의 파일해주는 파일 |      |
| @typescript-eslint/parser        | ESLint가 TypeScript 코드를 파싱할 수 있게 해주는 파서              |      |
| @typescript-eslint/eslint-plugin | TypeScript 코드에 대한 ESLint 규칙들을 제공하는 플러그인             |      |



</details>

<details>

<summary>그나저나, TypeScript 의존성 패키지 이름에 @ 기호 차이는 뭘까?</summary>

| 패키지 형태      | 의미              | 예시                                          |
| ----------- | --------------- | ------------------------------------------- |
| `패키지명`      | 일반 npm 패키지      | `typescript`, `react`                       |
| `@스코프/패키지명` | 스코프가 있는 npm 패키지 | `@types/react`, `@typescript-eslint/parser` |

npm 스코프(scope)를 나타낸다. 패키지 이름 앞 @ 기호가  붙는 경우가 있는데, 이건 관련 패키지들을 그룹화하고 이름 충돌을 방지하는 역할을 한다.

1. **네임스페이스 제공**: 관련 패키지들 그룹화
2. **이름 충돌 방지**: 동일한 이름 패키지가 다른 스코프에 존재할 수 있음!
3. **권한 관리**: 특정 스코프 패키지들에 대한 접근 권한 관리



참고

* [https://stackoverflow.com/questions/36293481/use-of-symbol-in-node-module-names](https://stackoverflow.com/questions/36293481/use-of-symbol-in-node-module-names)

- [https://docs.npmjs.com/cli/v9/using-npm/scope](https://docs.npmjs.com/cli/v9/using-npm/scope)

</details>



추가로 궁금한 점들

* 모듈은 왜 `ESNext`?
* import 쉽게 하기: `baseUrl: "."` 설정
* ts config 설정, tsconfig.node.json
  * ⁠tsconfig.node.json 파일은 Vite 프로젝트에서 필요한 이유
* path.resolve를 사용하는 이유

