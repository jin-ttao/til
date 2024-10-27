# Tailwind CSS

### 테일윈드 기본 스타일 세트 'Preflight'가 있기 때문에 reset.css를 추가할 필요 없다. (Base Styles)

- 처음에 자바스크립트 때의 생각으로 Tailwind 사용할 대에도 `reset.css` 코드를 CSS 코드에 추가해주었다.
- 이때 일부 Tailwind 스타일이 적용되지 않아서, CSS의 'Cascading' 관련, 즉 나중에 선언된 스타일이 더 높은 우선순위를 갖게 되어서 발생한 것은 아닐지 가설을 세웠다.
- 다행히 금방 원인을 찾을 수 있었는데, 앱의 CSS 코드를 하나로 모은 `index.css` 파일에서 Tailwind를 가장 상단에 선언하고, reset.css 코드를 마지막에 명시한 상태라 나중에 선언된 reset.css가 높은 우선순위로 적용된 것이다.
- 문제를 해결하려면, `reset.css`를 먼저 선언하고 Tailwind를 나중에 작성해서 위치를 바꿔주면 되었다. 하지만 최종적으로 `reset.css` 코드를 완전히 삭제했다.
- Tailwind 기본 'Preflight 세팅' 개념에 대해 알게 되었는데, 이 개념이 `reset.css` 코드 의도를 충분히 대체해주기 때문이다. 'modern-normalize' 기반을 사용해서 모든 기본 마진을 제거해주고, 스타일링도 초기화 해주어서 브라우저 간 일관성을 제공하도록 한다. 그래서 `reset.css`, `normalize.css`를 해줄 필요가 없다.

- 참고 https://tailwindcss.com/docs/preflight
  > Preflight <br> - An opinionated set of base styles for Tailwind projects.

  > Overview <br> - Built on top of modern-normalize, Preflight is a set of base styles for Tailwind projects that are designed to smooth over cross-browser inconsistencies and make it easier for you to work within the constraints of your design system.

  > Tailwind automatically injects these styles when you include @tailwind base in your CSS
  ```
  @tailwind base; /* Preflight will be injected here */

  @tailwind components;

  @tailwind utilities;
  ```
