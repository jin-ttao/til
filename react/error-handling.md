# Error Handling

## Error Boundry&#x20;

정의

* 컴포넌트 트리 내에서 JavaScript 오류가 발생하면 앱 전체가 충돌나버림.
* 딱 해당 오류만 잡아내서 fallback ui를 보여주는 '컴포넌트'를 에러 바운더리라고 함
* React 앱에서 발생하는 모든 오류를 잡아내는 게 아님.
  * 못 잡는 것들: 이벤트 핸들러, 비동기적 코드, 서버 사이드 렌더링, 자식 컴포넌트가 아닌 에러 바운더리 자체에서 발생하는 에러
  * '이벤트 핸들러 오류를 못 잡는다'를 대표적으로 보면
    * 사실 React는 이벤트 핸들러의 에러 해결에 에러 바운더리를 쓸 필요가 없음.
    * 이벤트 핸들러 내부에 에러가 발생해도, 화면에 뭘 표시해야할지 React는 이미 알고 있기 때문.
      * 이벤트 핸들러는 '렌더링 중에 발생하지 않음'. (render 메서드 및 생명주기 메서드는 렌더링 중 발생)
    * 이벤트 핸들러 내 에러도 잡긴 잡아야 할텐데, 이때는 그냥 JavaScript `try / catch` 구문 사용하면 됨.



동작 흐름

* 이것도 React가 해주는 건데, 순서는 이러함.
  * 컴포넌트 트리에서 에러 발생
  * 부모 중 에러 바운더리로 등록된 컴포넌트의 `componentDidCatch()` 메소드 호출



구현 방법

* 클래스형 컴포넌트로 구현해야 함 (함수형 컴포넌트로는 불가 - 이유는 아래 참고)
* 생명주기 메소드 사용해서 에러 바운더리 컴포넌트로 만들 것
  * `getDerivedStateFromError()`
  * `componentDidCatch()`

> 생명주기 메서드인 static getDerivedStateFromError() 와 componentDidCatch() 중 하나 (혹은 둘 다)를 정의하면 클래스 컴포넌트 자체가 에러 경계가 됩니다.&#x20;
>
> * 에러가 발생한 뒤에 폴백 UI를 렌더링하려면 static getDerivedStateFromError()를 사용하세요.&#x20;
> * 에러 정보를 기록하려면 componentDidCatch()를 사용하세요.

```javascript
import React from 'react';

class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.error('Error caught:', error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>문제가 발생했습니다.</h1>;
    }
    return this.props.children;
  }
}

// 사용
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

#### 왜 함수형 컴포넌트는 안되나?

* 사용해야 하는 생명 주기 메소드 componentDidCatch 가 클래스형 컴포넌트에서만 가능함.
* 함수형 컴포넌트는 내부적으로 상태, 라이프사이클을 '직접' 갖고 있지 않음.
  * 훅(hook)으로 React한테 요청하는 것일 뿐 ("이런 타이밍에 이거 할래")
  * 함수형 컴포넌트는 '그냥 한 번 실행되는 함수'일 뿐. 내부에서 catch 가능한 구조가 아님. 오류 발생시 hook으로 catch 가능한 수단이 없음.

```javascript
// fallback 보여줄 수 있을 것 같지만,
// 실제로 에러 컴포넌트에서 발생한 에러는 동기적으로 try/catch로 못 잡음.
function MyComponent() {
  try {
    return <에러 컴포넌트 /> // 여기에 에러가 나면?
  } catch (e) {
    return <Fallback 컴포넌트 />;
  }
}
```

#### 함수형 컴포넌트 안에서 `componentDidCatch` 메소드를 호출하면 안되나? ⇒ **정의/호출 둘 다 안됨.**

`componentDidCatch` 메소드는 React가 클래스형 컴포넌트 안에서 쓰려고 만든 것

```javascript
// React가 클래스형 컴포넌트 렌더링 할 때 내부 동작
const instance = new MyComponent();
instance.render(); // error 발생 시 catch
instance.componentDidCatch(error, info); // React가 직접 호출
```

함수형 컴포넌트는 new로 인스턴스 만들지도 않고, 메서드도 없음.

<pre class="language-javascript"><code class="lang-javascript"><a data-footnote-ref href="#user-content-fn-1">function</a> MyComponent() {
  // 그냥 실행되는 함수
  return &#x3C;div>Hello&#x3C;/div>;
}
</code></pre>

그래서 아무리 함수형 컴포넌트 안에서 `componentDidCatch` 함수 호출해도 React 입장에서는 '부를 대상'이 없음.

```javascript
function MyComponent() {
  function componentDidCatch(error, info) {
    console.log("에러 잡음!");
  }

  return <에러컴포넌트 />;
}
```



{% embed url="https://ko.legacy.reactjs.org/docs/error-boundaries.html" %}



[^1]: 
