# Side effect

### useEffect와 순수성

* "계속해서 `render` 메소드를 호출함으로써 업데이트 사항들을 한번에 반영하는 것이었죠." 바코 블로그 보다가 리액트의 동작 방식에 대한 문구가 보였다. Angular나 다른 라이브러리와 다른 리액트만의 방식이라고 보여졌다. 그래서 `render` 메소드가 궁금해졌음.

\[검증] React 공식문서에는 "React expects every component to behave like a pure function with respect to its props" 라고 명시되어 있었다. 또한 "Don't mutate any objects that existed before rendering. During rendering, only change the objects that you've created during this same rendering." 라고 경고하고 있었다. 이는 렌더링 중에는 기존 객체를 변경하지 말고 순수성을 지켜야 한다는 의미였다.

\[render 메소드 관련] render 메소드는 클래스형 컴포넌트에서 UI를 그리는 핵심 메소드였다. 공식문서에는 "The render() method is the only required method in a class component" 라고 설명하며, "The render() function should be pure, meaning that it does not modify component state" 라고 강조하고 있었다. 함수형 컴포넌트에서는 이 render 메소드 대신 함수 자체가 렌더링을 담당하게 되었다.

\[참고]

* React 공식 문서: https://react.dev/learn/keeping-components-pure
* React 렌더링 동작 원리: https://legacy.reactjs.org/docs/react-component.html#render
