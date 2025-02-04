# React State

<!-- toc -->

- [context](#context)
- [opinion](#opinion)
  - [1. 무엇을 state로, 어디에 둘 것인가? React는 편리하지만, 꼭 필요한 경우에만 쓸 것을 강조한다.](#1-%EB%AC%B4%EC%97%87%EC%9D%84-state%EB%A1%9C-%EC%96%B4%EB%94%94%EC%97%90-%EB%91%98-%EA%B2%83%EC%9D%B8%EA%B0%80-react%EB%8A%94-%ED%8E%B8%EB%A6%AC%ED%95%98%EC%A7%80%EB%A7%8C-%EA%BC%AD-%ED%95%84%EC%9A%94%ED%95%9C-%EA%B2%BD%EC%9A%B0%EC%97%90%EB%A7%8C-%EC%93%B8-%EA%B2%83%EC%9D%84-%EA%B0%95%EC%A1%B0%ED%95%9C%EB%8B%A4)
  - [2. 다른 코드 벤치마크할 때, 무엇을 state로 관리하는지, 무엇을 컴포넌트로 만들었는지 보면 어떤 생각으로 문제를 해결하려고 했는지 보일 것 같다.](#2-%EB%8B%A4%EB%A5%B8-%EC%BD%94%EB%93%9C-%EB%B2%A4%EC%B9%98%EB%A7%88%ED%81%AC%ED%95%A0-%EB%95%8C-%EB%AC%B4%EC%97%87%EC%9D%84-state%EB%A1%9C-%EA%B4%80%EB%A6%AC%ED%95%98%EB%8A%94%EC%A7%80-%EB%AC%B4%EC%97%87%EC%9D%84-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A1%9C-%EB%A7%8C%EB%93%A4%EC%97%88%EB%8A%94%EC%A7%80-%EB%B3%B4%EB%A9%B4-%EC%96%B4%EB%96%A4-%EC%83%9D%EA%B0%81%EC%9C%BC%EB%A1%9C-%EB%AC%B8%EC%A0%9C%EB%A5%BC-%ED%95%B4%EA%B2%B0%ED%95%98%EB%A0%A4%EA%B3%A0-%ED%96%88%EB%8A%94%EC%A7%80-%EB%B3%B4%EC%9D%BC-%EA%B2%83-%EA%B0%99%EB%8B%A4)
  - [3.](#3)
- [research](#research)
  - [1.](#1)
  - [2.](#2)
  - [3.](#3-1)

* [h1](#h1)
  - [context](#context-1)
  - [opinion](#opinion-1)
    - [1.](#1-1)
    - [2.](#2-1)
    - [3.](#3-2)
  - [research](#research-1)
    - [1.](#1-2)
    - [2.](#2-2)
    - [3.](#3-3)

<!-- tocstop -->

## context

<br>

## opinion

### 1. 무엇을 state로, 어디에 둘 것인가? React는 편리하지만, 꼭 필요한 경우에만 쓸 것을 강조한다.

- **결론: state로 둘 이유를 설명할 수 있다면 일단 state로 두고, 일반 변수로 바꾸거나 최적화 가능하다면 그때 바꾸자. 첫 술에 완벽할 수 없다.**
- 공식 문서를 보면, React는 useffect, useMemo 등 이미 있는 것들로 충분히 해결가능한 것을 굳이 사용하지 말 것을 거듭 권장한다. (학습 차원에서 테스트 목적으로 시도해보는 건 언제나 좋다.)
- React는 무엇을 state로 관리할 것인지 의사결정은 개발자의 몫이라고 넘기기 때문에, 이에 대한 기준을 정립하는 건 앞으로도 중요한 과제라고 생각한다.
- 최근 React를 활용해 간단한 과제를 수행했는데, state를 최소화 하다 못해 너무 사용하지 않았다. 동일한 과제를 수행한 다른 팀의 결과물과 큰 차이가 있었다. '로딩 상태', '오류 여부' 등 '이런 것 까지 상태로 관리할 수 있구나' 싶은 것들이 다양했다.
- 소프트웨어 개발에서는 일정에 맞추어 기능을 구현해내는 것이 가장 중요하고, 기본의 기본이기 때문에 일단 만들어내는 것이 가장 중요하다. 이러한 측면에서 충분히 state로 관리될법한 근거들이 보이면 우선 활용해보도록 하자.
- (추후) 추가하면 좋을 리서치 자료들 보인다면 추가해두기.

<br>

### 2. 다른 코드 벤치마크할 때, 무엇을 state로 관리하는지, 무엇을 컴포넌트로 만들었는지 보면 어떤 생각으로 문제를 해결하려고 했는지 보일 것 같다.

- 초반에 아카이빙 하고 비교해보면 큰 그림을 보고, 나중에 프로젝트 초반 전체 구조를 설계할 때 적용해볼 수 있겠다.
- 마치 알고리즘 문제에서, 함수 안에 '무엇을 변수로 두고', 각각의 코드는 '무엇을 return' 하는지를 중심으로 보면 알고리즘이 잘 읽히듯.
- (추후) 벤치마크로 테이블화 하고, 인사이트 정리 마무리 하고 핵심 같이 업로드.

<br>

### 3.

<br>

## research

### 1.

<br>

### 2.

<br>

### 3.

<br>

# h1

<br>

## context

<br>

## opinion

### 1.

<br>

### 2.

<br>

### 3.

<br>

## research

### 1.

<br>

### 2.

<br>

### 3.
