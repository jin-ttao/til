# JavaScript Runtime

### 자바스크립트 런타임이 새롭게 계속 나오는 이유는 무엇인가? (결론 없이 생각 메모)
- 링크드인에서 `shadcn/ui` 글을 접하고 더 구글링 하다가 Bun을 만났다. 작년 2023년 한해 동안 `shadcn/ui`이 Bun, Excalidraw 보다 GitHub Star를 많이 받았다는 맥락. `shadcn/ui` 뿐 아니라 Bun도 처음 보는 개념이라 검색해보니, 최신 자바스크립트 런타임 환경이라는 것을 알게 되었다.
- 이전까지, 내 개발 세계관에서 자바스크립트 런타임은 몇 없었다. 브라우저, Node.js 정도. Bun을 알게 되면서 ‘이 2개의 런타임이 전부가 아니구나’를 깨달았다. 그리고 앞으로 또 새로운 런타임이 계속 생겨날 수 있겠다는 생각이 들었다.
- 그럼 왜 새로운 환경이 태어났을까? (당장 깊게 파지는 못 했다. 이렇게 메모를 남겨두면 그냥 슥 보기 보다 기억에 남을 수 있어서 10분을 투자해서 써두는 편.) Bun은 GitHub 리포지토리에서 자신을 이렇게 소개한다.
> “Bun Incredibly fast JavaScript runtime, bundler, test runner, and package manager – all in one”.
- ‘올인원’ 이라는 키워드가 눈에 들어온다. 기존의 다른 런타임과 달리 하나로 충분하다는 뜻일까. 그러고 보니 node.js에서는 번들러(e.g. Vite, Webpack), 테스트 실행을 위해 필요한 라이브러리(e.g. Cypress, Vitest), 패키지 매니저(e.g. Npm, yarn) 등 각각 달랐다. 처음에 이 기술들도 특정 문제를 해결하기 위해 등장했겠지만, 상황은 변하고 있고 더욱 복잡해진 애플리케이션 환경에서는 또 다른 문제를 낳았을 것이다.
- Bun은 애플리케이션 개발에 필요한 이 기능들을 런타임 자체에 내장시킴으로써, 성능이나 복잡성 등 문제를 해결한 것일까? 아직 깊게 찾아보지 않았지만 흥미로운 생각으로 이어질 수 있었다.
- 참고할 문서
  - https://bun.sh/
  - https://ykss.netlify.app/translation/bun_vs_node_js_everything_you_need_to_know/
