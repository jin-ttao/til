# welcome-toast 회고

<!-- toc -->

- [12.09](#1209)
    + [keep) 좋은 수면 패턴 발견, 당분간 더 시도해볼 것. 👍](#keep-%EC%A2%8B%EC%9D%80-%EC%88%98%EB%A9%B4-%ED%8C%A8%ED%84%B4-%EB%B0%9C%EA%B2%AC-%EB%8B%B9%EB%B6%84%EA%B0%84-%EB%8D%94-%EC%8B%9C%EB%8F%84%ED%95%B4%EB%B3%BC-%EA%B2%83-%F0%9F%91%8D)
    + [keep) 아침 첫 업무로 알고리즘 문제 풀기를 성공했음 👍](#keep-%EC%95%84%EC%B9%A8-%EC%B2%AB-%EC%97%85%EB%AC%B4%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C-%ED%92%80%EA%B8%B0%EB%A5%BC-%EC%84%B1%EA%B3%B5%ED%96%88%EC%9D%8C-%F0%9F%91%8D)
    + [keep) 작업현황 정리, 회고 작성을 한 템포 빨리 가져가는 것 👍](#keep-%EC%9E%91%EC%97%85%ED%98%84%ED%99%A9-%EC%A0%95%EB%A6%AC-%ED%9A%8C%EA%B3%A0-%EC%9E%91%EC%84%B1%EC%9D%84-%ED%95%9C-%ED%85%9C%ED%8F%AC-%EB%B9%A8%EB%A6%AC-%EA%B0%80%EC%A0%B8%EA%B0%80%EB%8A%94-%EA%B2%83-%F0%9F%91%8D)
    + [problem) 공식 문서를 제대로 보자🔥=> 새로운 기술스택 사용 중 이전에 써본 기술 경험에 의존해서 추측하지 말기](#problem-%EA%B3%B5%EC%8B%9D-%EB%AC%B8%EC%84%9C%EB%A5%BC-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EB%B3%B4%EC%9E%90%F0%9F%94%A5-%EC%83%88%EB%A1%9C%EC%9A%B4-%EA%B8%B0%EC%88%A0%EC%8A%A4%ED%83%9D-%EC%82%AC%EC%9A%A9-%EC%A4%91-%EC%9D%B4%EC%A0%84%EC%97%90-%EC%8D%A8%EB%B3%B8-%EA%B8%B0%EC%88%A0-%EA%B2%BD%ED%97%98%EC%97%90-%EC%9D%98%EC%A1%B4%ED%95%B4%EC%84%9C-%EC%B6%94%EC%B8%A1%ED%95%98%EC%A7%80-%EB%A7%90%EA%B8%B0)
- [11.30](#1130)
- [11.29](#1129)
- [11.28](#1128)

<!-- tocstop -->

## 12.09

#### keep) 좋은 수면 패턴 발견, 당분간 더 시도해볼 것. 👍

- 1:30 - 7:00 수면으로 5h30m 정도 잠. 그닥 피곤하지도 않고, 바코에도 8:40에 도착할 수 있었음.
- 일찍 도착하면 컨디션 good. 7시 즈음 일어나는게 하루 시작하기에 가장 좋은 타이밍 같음.
- 바코에서 잤다면 4시쯤 자서 9 or 10시에 일어났을테니 5-6시간 자는 셈.
  - ⇒ 결국 비슷한 수면시간! 새벽에 안자고 하는게 단기, 장기적으료 나에게 효율적이지 않다는 생각이 점점 커진다.
  - 절대적인 시간 외에, 1시간의 밀도도 챙기자.

#### keep) 아침 첫 업무로 알고리즘 문제 풀기를 성공했음 👍

- 매번 첫 일과로 알고리즘을 풀어야 한다는 걸 느꼈지만 실제로 실천한 적이 많지 않았음. 마음이 급해서, 중요해보이는 업무 먼저 처리했기 때문. 하지만 막상 이렇게 먼저 푸니 하루종일 마음이 편했음. 더 중요한 업무에 집중할 수 있게 되었달까. 알고리즘 챌린지 실패하지 않도록 끝까지 해보자.

#### keep) 작업현황 정리, 회고 작성을 한 템포 빨리 가져가는 것 👍

- 미리 미리 하는 건 역시 항상 좋다.

#### problem) 공식 문서를 제대로 보자🔥=> 새로운 기술스택 사용 중 이전에 써본 기술 경험에 의존해서 추측하지 말기

- supabase OAuth 로그인 구현이 예상 보다 2시간 더 걸렸다. (기본 세팅 포함 3시간 예상했지만 5시간 걸림)
- 결국 해답은 React 관련 파트에 명확히 기재되어 있었음. 그전 까지는 Firebase 방식()처럼 로그인 구현, 로그인 유저 정보 할당을 시도하려고 했고, supabase는 다른 방식이라는 것을 결국 깨달았다.
- 새로운 기술스택 사용 중 이전에 써본 기술 경험에 의존해서 추측하지 말기
  - supabase 공식 문서에 기재된 상황이 내 상황과 100% 맞지 않을 수 있다는 생각에 머뭇거렸다.
  - 공식 문서 내 여러 문서를 최대한 충실히 살펴보고, 모두 시도해보고 다른 블로그를 보든 하는게 맞겠다.

## 11.30

- 고민) 어드민 GUI 구현이 중요할까, CLI 만으로 패키지 완성도 높이는게 우선일까? → 후자를 중요도 높이는게 좋지 않을까. 어차피 후자를 자동화 시키는 것이 전자일 것.
- 챌린지) 위치 정의 어떻게 하지. 텍스트가 길어지면 문제가 생길 수 있음. 강조할 것을 침범하지는 말아야 함. ⇒ 이거 고려하면서 구현하기. 테스트 때 모두 해결할 수 없음. 뭘 고려하면서, 어떤 작업해야하는지 정도만 검증
- 오랜만에 바닐라 JS로 DOM을 직접 제어하자니 헷갈렸지만 재밌었다. 가장 기초 개념이라, 동작 원리 단계 까지 이해가 필요하고 리마인드 기회가 많았음👍
- 챌린지) HTML 요소는 만들긴 했는데, 스타일/애니메이션은 어떻게 제어하지? 너무 레퍼런스에 얽매이지 말고, 나 스스로 구현해보면서 고민도 병행하자. 그래야 next step이 더 잘 보일 것.
  NPM 패키지 배포 - Zustand 2019년도 초기 커밋 보니 master 브랜치 하나만 있던데 다른 브랜치에서 만들다가 머지 하면서 삭제한 것 같다. 이런 방식을 벤치마크 해볼 것. [GitHub Commits·pmndrs/zustand](https://github.com/pmndrs/zustand/commits/main/?since=2019-04-09&until=2019-04-09)
- 오랜만에 DOM(Document Object Model) 공식문서를 보니, 비슷한 단어 ‘ODM(object data modeling)’이 떠올랐다. 둘 다 무언가 ‘연결(connect/map)’ 해주고 있었다. → ‘객체 지향 프로그래밍’과 비슷한 맥락인지 모르겠지만 더 파보고 싶다.
- 오… 인터콤, 채널톡 모두 상담 버튼 누르면 나오는 상담창은 `iframe` 이구나. 웹서비스 위 별도의 웹서비스가 띄워져야 하니 `iframe`으로 임베드 하는 방법이 적절했을 것. 추후 고도화 고민할 때 토스트 메시지 이상으로, 상호작용을 추가하거나 리소스를 더 보여주고 싶으면 `iframe`을 활용해서 띄워줘도 좋겠다.
  - (추가 아이디어) 성능 최적화를 iframe으로 해볼 수 있을까?
- SDK 레퍼런스의 소스 코드들은 왜 var 키워드로 선언했을까? 전역으로 해야 해서 그런가?
- script 방식이면 SPA, MPA 각각 대응을 해야할 것 같다. HTML 렌더링 방식 자체가 완전 다르기 때문인데, 채널톡도 이를 구분해서 안내하고 있음(Channel Developers 시작하기). npm 패키지로 하면 해결되려나? script 직접 로드 방식으로 하다 보니 더 영향 받는 것 같다.
- `.js` vs `.mjs` 확장자 [Stack Overflow What is the difference between .js and .mjs files?](https://stackoverflow.com/questions/57492546/what-is-the-difference-between-js-and-mjs-files)
- `CSSStyleDeclaration` 라는 개념도 있네? 동적으로 JS에서 DOM 요소에 CSS 스타일 주려다가 찾아봄. 그동안 개념을 모른채 사용하고 있었다.
- 인터콤의 js 파일에서 CSS 코드 벤치마크 https://widget.intercom.io/widget/
- 쌓임 맥락 관련해서도 알아야겠다. 사용자 웹사이트의 요소 보다 z-index 상 위에 위치시켜야 할 것. [MDN Web Docs Stacking context - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context)
- 아이디어) 코치 마크, 토스트 메시지 꼭 따로 구현해야 할까? 구분하기 애매하고, 유저도 헷갈릴 것: 코치 마크, 토스트 메시지 분리하지 말고 backgroundOpacity, highlight 조절하는 방식으로 구현
- 아이디어) 유저 메시지 로직 다양화 - 7일만에 돌아온 유저면 재방문 환영

## 11.29

- 내 코드가 다른 서비스 코드에 삽입, 빌드 과정에 함께 포함되어 배포(?)된다는 개념이 와닿지 않는다.
- 내 코드를 사용자(개발자)가 신뢰하고 사용할 수 있게 해야 한다. 그 뒤에, 스타일 커스텀 가능 여부를 논하는게 맞는 순서일 것. (중요)
  - 리스크 있는 SDK를 누가 쓸까?
- npm package으로 만들지 않을 이유가 없어보임.
  - 장단점 있음. package로 배포하면 버전 업데이트에 따라 사용자도 버전 업데이트 하고 써야 함.
  - 먼저 `script` 태그 로드 방식으로 테스트 하고 결정하자.
- 4년 전 2020년 방식으로 해보기. 채널톡 연동했던 당시에는 코드가 단순해서 내가 이해하기 쉬울 것이다.
  - https://jujeonghwan.github.io/service/how-to-add-channel-talk-chat-service-to-a-website-kr/
  - script 안에 즉시실행함수로 테스트하기.
- 예전 구글 Firebase Auth, RealTime Database 처음 사용할 때 인스턴스에 대해 궁금했는데, 이번에는 이걸 활용해서 내가 직접 구현하는 것이라 생각할 수 있겠다.
- `<script>` 태그의 역할은 실행 가능한 코드 혹은 데이터 삽입.

  - 자바스크립트 파일을 HTML page에서 바로 사용 가능.
    > The `<script>` tag is what we use to includes our JavaScript. It's a lot like the `link` tag you've already been using to include your CSS files.
    > Here's a very basic snippet of JavaScript using the script tag. This JavaScript is written directly into our HTML page. It will call and alert box as soon as the page loads. ([출처](https://www.notion.so/14d4196d295c8069964df8354d8e157a?pvs=21))

- 왜 npm 패키지 모듈 방식 보다 `<script>` 태그를 통해 연동하는 걸 우선 구현해야 하는가?
  - 발췌) 하지만 서비스 초창기에 제작된 일부 페이지들은 아직 React가 아닌 jQuery 기반의 페이지로 사용되고 있습니다. 따라서 ESM 방식으로 SDK를 사용할 수 없고 html 레벨의 Script 로딩이 필요하게 되었습니다. [마이리얼트립 블로그 링크](https://medium.com/myrealtrip-product/%EC%9B%B9%EB%A1%9C%EA%B7%B8-javascript-sdk-%EA%B0%9C%EB%B0%9C-%EB%A7%9B%EB%B3%B4%EA%B8%B0-ffc8a1a00f8d#:~:text=%EB%94%B0%EB%9D%BC%EC%84%9C%20ESM%20%EB%B0%A9%EC%8B%9D%EC%9C%BC%EB%A1%9C%20SDK%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%A0%20%EC%88%98%20%EC%97%86%EA%B3%A0%20html%20%EB%A0%88%EB%B2%A8%EC%9D%98%20Script%20%EB%A1%9C%EB%94%A9%EC%9D%B4%20%ED%95%84%EC%9A%94%ED%95%98%EA%B2%8C%20%EB%90%98%EC%97%88%EC%8A%B5%EB%8B%88%EB%8B%A4.)
- 체크) Amplitude 연동할 때 배포에 push하지 않았음에도 개발 환경에서 script 태그 연동을 알고 앰플리튜드에서 데이터가 나온게 신기했다. 어떻게 가능했을까?
- 칸반을 어떻게 짜야할까.
  - 칸반 빠르게 구성하는 연습 (내가 뭘 해야하는지 빠르게 정의하는 연습)
    - 필요한 화면 목록들, 필요한 기능 목록들 ⇒ 눈에 보이는 명확한 것들 위주로. 아직 모르는 개념은 하위작업 쪼개면서, 구현하면서, 물어보면서 정의 가능.
- 칸반을 먼저 정의하고 싱크하고 싶은데, SDK 개발은 처음이라 어떤 것을 구현해야 할지 모호하다.
  - 어떤 절차로 구현해야 하는지 말이다. 속도가 나지 않아서 답답. 이럴 때 일수록 차분하게 생각해볼 것.
  - 사실 다시 생각해보면 구현할 것(what)은 정의할 수 있지만, 구현방법(how)가 명확하지 않아서 모호한 것 같다.

## 11.28

- 잠재 사용자인 부트캠프 선배, 동기들 5명 인터뷰를 완료했다. 덕분에 내가 집중할 것, 집중하지 않을 것을 선별할 수 있었다.
- 에디터를 어느 기능 까지 지원할 것인가. 사용자는 많은 텍스트를 원하지 않는다. 또 이미지도 해버리면 결국 화면이 복잡해질 수 있겠다.
- 칸반 짜는데 어려움이 있었다. 구현할 기능이 더 명확하고, 구체적인 구현 방법이 필요하겠다고 생각했다.
- 개선점: 하루 일정을 계획적으로 관리하기. 장기 일정과 그것을 받춰줄 단기 일정이 정의되어야겠다. 즉흥적으로 한게 많았는데, 내일은 계획 액션 비중을 더 늘리자.
