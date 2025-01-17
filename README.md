# thoughts over theories

> 이론에 의견 덧붙이기
- 학습 내용을 정리하고 있습니다. (2025.01)

<br>
<br>

# 목차

<!-- toc -->

- [JavaScript](#javascript)
- [React](#react)
  * [React 공식 문서 - Thinkgin in React](#react-%EA%B3%B5%EC%8B%9D-%EB%AC%B8%EC%84%9C---thinkgin-in-react)
  * [React 공식 문서 - 튜토리얼](#react-%EA%B3%B5%EC%8B%9D-%EB%AC%B8%EC%84%9C---%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC)
  * [React 공식 문서 - 조건부 렌더링](#react-%EA%B3%B5%EC%8B%9D-%EB%AC%B8%EC%84%9C---%EC%A1%B0%EA%B1%B4%EB%B6%80-%EB%A0%8C%EB%8D%94%EB%A7%81)
  * [React 공식 문서 - 리스트 렌더링](#react-%EA%B3%B5%EC%8B%9D-%EB%AC%B8%EC%84%9C----%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EB%A0%8C%EB%8D%94%EB%A7%81)
  * [JSX 내부에서 자바스크립트 표현식(expression)만 사용 가능한 이유](#jsx-%EB%82%B4%EB%B6%80%EC%97%90%EC%84%9C-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%91%9C%ED%98%84%EC%8B%9Dexpression%EB%A7%8C-%EC%82%AC%EC%9A%A9-%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%9D%B4%EC%9C%A0)
  * [React Router](#react-router)

<!-- tocstop -->

<br>
<br>

# JavaScript

##

<br>
<br>

# React

## React 공식 문서 - Thinkgin in React
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-thinking.md)
- 기술적인 사고방식이나 코드의 패턴을 써먹기 전에, 어떤 멘탈 모델을 탑재하면 될지 익히기.
- 공식적으로 권장되는 '리액트를 사용하는 맥락', '관점', 'tip' 등을 확인해볼 것.

<br>

## React 공식 문서 - 튜토리얼
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-opinion-on-official_docs.md)
- 리액트 공식 문서에서 `<React 학습>` 파트를 읽고 의견을 기록한다.
- 진행 현황 (2024.10.23 기준)
  - UI 표현하기 90% (9/10)
  - 상호작용성 더하기 0% (0/8)
  - State 관리하기 0% (0/8)
  - 탈출구 11% (1/9)

<br>

## React 공식 문서 - 조건부 렌더링
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-conditional-rendering.md)

- 컴포넌트 안에서 원하는 컴포넌트의 일부만, 즉 컴포넌트를 구성하는 특정 JSX 조각을 의도에 맞게 보여주거나 가릴 수 있다.
- 이때 렌더링 기준이 될 '조건'이 필요한데, React 공식 문서의 <조건부 렌더링> 파트를 보면서 (1) 조건이라는 것을 명시하는 방법, (2) 그 조건 하에서 무언가 보여주거나 보여주지 않는 방법을 익혀보려고 한다.

<br>

## React 공식 문서 -  리스트 렌더링
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-list_rendering.md)

- 바닐라 자바스크립트를 배우던 시기에, Tic-Tac-Toe 구현 프로젝트에서 여러 개의 div 태그를 구현할 때 동적으로 DOM을 생성해준 적이 있다.
- 더 이 전에는 일일이 HTML로 div를 찍어두었는데, 미리 HTML 코드로 정적 마크업을 만들어두지 않는 편이 좋다. 브라우저가 스크립트를 실행할 때 동적으로 DOM을 만들어주는 것이 몇 개일지 모를 태그를 일일이 만들어주지 않아도 되는 장점이 있다. 무엇 보다 유연하게 대응(e.g. 사용자 입력값 등에 따라 유동적으로 생성) 가능하다는 점도 유용하게 썼던 부분이다.
- 본 문서에서는 자바스크립트에서의 이러한 작업을 당연히 리액트에서도 할 수 있는데, 어떠한 점에서 다른지, 리액트가 어떻게 이 작업을 수행하는지 중심으로 적어보려고 한다.

<br>

## JSX 내부에서 자바스크립트 표현식(expression)만 사용 가능한 이유
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-jsx_only_expression.md)

- 표현식이 값을 반환하는 건 이해했지만, JSX에는 왜 값만 있어야 할까?
- 이유들을 조사해보니 근본적 원인은 이미 배운 개념에 있었고, 새롭게 React & JSX에 접목시켜 이해하는 것이 중요했다.

<br>

## React Router
[문서 바로가기](https://github.com/jin-ttao/til/blob/main/react/react-router.md)
- 라우팅 구조, 적용하면서 고민을 기록.
- 사용자의 로그인 여부를 App 컴포넌트에서만 하는게 좋을까, 각 페이지 컴포넌트에서 하는게 좋을까?
- 중첩 라우팅
  - 중첩된 컴포넌트는 동시 렌더링이 되기 때문에 두 컴포넌트에서 정보를 어느정도 공유하는 것 '처럼' 쓸 수 있다.
  - 중첩 라우팅은 순서대로 부모 > 자식 호출될 것을 보장해주나?

