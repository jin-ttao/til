# 구현 중 고민들

## context

* 바닐라 자바스크립트, 리액트로 구현 중 생긴 고민을 기록한다.
* (고민) => (구체적인 액션 아이템)을 통해 나만의 구현 방법론을 최적화 한다.

## content

### 24.10.12 이번 과제 프로젝트 만들면서 아쉬웠던 점

#### 만약 다시 처음 부터 만든다면 무엇을 할거냐, 그 다음은? 그 다음은?: 요구사항을 소화하고, 내가 기능을 재정의 한다. 그리고 커밋 계획을 스케치할 거고, 일정을 맞추기 위해 주변에 도움을 적극적으로 요청한다.

기능 정의 부터 할거다. 요구사항 그대로 보는게 아니라, 요구사항을 보고 내가 소화한 기능으로 '재정의'할 것이다. 그 다음 커밋을 어떤 단위로 할지 쭉 나열해볼거다. 이 커밋 계획에서 각 커밋은 내 작업 단위가 된다. 그리고 5분 안에 가장 먼저 해야할 작업을 정해서 바로 들어갈 것이다. 그리고 매일 혹은 더 짧은 텀으로 커밋 계획을 수정하고 디벨롭 해 나갈 것이다. 만약 일정 대로 커밋 계획을 맞추지 못한다면, 그냥 흘려보내는게 아니라 어떻게든 일정을 맞출 수 있게 도움을 요청할 것이다.

#### 프로젝트 속도를 더 빨리 냈으려면 어떻게 했어야 했을까? 아래 옵션들이 기여를 할까?

```
- (1) 디버깅 - 개발자 도구
- (2) 디버깅 - prop validation?
- (3) 요구사항 소화 후 재정의 부족,
- (4)
```

제품을 만들 때 어디서 부터 어떻게 시작하면 좋을지 확신이 생기지 않는다. 나 혼자 만든다면 달랐을까. 다른 팀원들에게 합리적인 진행방식을 제안해야 한다고 생각해서, 고민을 더 했던 것 같다. 무턱대고 시작하기 싫었던 점도 있었고.

아직 경험이 부족한 것이니, 더 많이 부딪히면서 나만의 방법론을 찾아나가자. 다른 팀은 무언가 기능을 붙이기 위해 'UI 부터 그렸다'고 한다. 우리는 '리액트적 사고하기' 과정을 최대한 따르려고 했던 것 같은데, 아직은 자유자재로 활용하지 못하는 것 같다. 아직 '레시피'를 활용하는 수준.

이번 프로젝트 중 뭐에 시간 많이 썼나? 재발 방지하자.

* 참고: 문서를 먼저 작성하면 달라지는 것들 | Jbee.io 화수 커밋 돌아보기. 리덕스 이해에 이론적 시간 많이 쓴 듯, 실험도 많이 해보면 좋았을 것.
* 설계 -
* 디버깅 - 왜 타입 에러가 뜨지. 날짜 객체,
* 구현 - 저 클릭한 이벤트 날짜 어떻게 가져오지
* 아쉬움들: useReducer 미적용, prop validation 미적용, 의존성 배열 아직도 헷갈림..
