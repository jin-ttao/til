# Component

#### 생각) 클래스형 컴포넌트는 선언적이지 않다?

* 클래스형 컴포넌트는 명령형 프로그래밍에 가깝다는 생각이 든다. 덜 선언적인 것 같다.
* 리액트는 바닐라 자바스크립트로 만든 앱의 코드 보다 what에 집중한 선언형에 가깝다 생각했다. 함수형 컴포넌트는 그걸 잘 보여주는 것 같고.
* 실제로 함수형 컴포넌트로 컨셉을 틀면서 리액트 팀의 공식 입장은 어땠을까?

> React is responsible for rendering components and Hooks when necessary to optimize the user experience. It is declarative: you tell React what to render in your component’s logic, and React will figure out how best to display it to your user.\
> [React calls Components and Hooks](https://react.dev/reference/rules/react-calls-components-and-hooks?utm_source=chatgpt.com)

{% embed url="https://overreacted.io/how-does-react-tell-a-class-from-a-function/" %}

{% embed url="https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889" %}
Dan Abramov
{% endembed %}

{% embed url="https://dev.to/craigmichaelmartin/hooks-for-those-who-know-react-3n89" %}
Dan Abramov 트윗 아카이빙
{% endembed %}

{% embed url="https://dev.to/syakirurahman/react-functional-component-with-hooks-everything-you-need-to-know-5bjj" %}
정리 굿
{% endembed %}



#### 함수형 컴포넌트는 내부적으로 상태, 라이프사이클을 '직접' 갖고 있지 않음.

<table><thead><tr><th width="145.05902099609375">구분</th><th>클래스형 컴포넌트</th><th>함수형 컴포넌트</th></tr></thead><tbody><tr><td>컨셉</td><td>내가 상태, 라이프사이클 메소드 <br>전부 다 직접 가진다</td><td>그냥 JS 함수일 뿐. 소유 X</td></tr><tr><td>목적/정체성</td><td>상태, 생명 주기를 자기 안에 <br>직접 구현한 '객체'<br>- React는 클래스형 컴포넌트를 인스턴스(new) 로 만들고, 상태와 메서드를 그 인스턴스 안에 저장</td><td>JSX 반환<br>- 함수(컴포넌트) 자체에는 상태도 없고, 생명주기 메소드도 없음</td></tr><tr><td>state, effect 처리</td><td>- <code>this.state</code> 로  상태를 직접 가짐.<br>- <code>componentDidMount()</code>로 React가 직접 호출하는 메서드</td><td>React가 따로 내부에서 처리<br>- React가 훅 보면서 순서에 따라서 이어붙여주는 식 (linked list로 훅 관리하는 것과 연결되는 개념일지 더블 체크)</td></tr></tbody></table>



#### 함수형 컴포넌트는 훅(hook) 때문에 쓸 수 있는 것.&#x20;

* 훅(hook)은 함수형 컴포넌트를 설명할 때 빼놓을 수 없는 React의 중요한 인터페이스였음...
* `useState`, `useEffect`도 결국 캡슐화/추상화 된 React의 함수

```javascript
const [count, setCount] = useState(0);

// count 상태는 여기 컴포넌트에 없음.
// React한테 매번 요청해서 받아내는 것.
```



```javascript
// 클래스형
class MyComponent extends React.Component {
  state = { count: 0 };

  componentDidMount() {
    console.log("마운트 완료!");
  }

  render() {
    return (
      <button
        onClick={
          () => this.setState({ count: this.state.count + 1 })
        }
      >
        {this.state.count}
      </button>
    );
  }
}
```

```javascript
// 함수형
function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("마운트 완료!");
  }, []);

  return (
    <button
      onClick={
        () => setCount(count + 1)
      }
    >
      {count}
    </button>
  );
}
```





{% embed url="https://ko.javascript.info/class-inheritance" %}



### 재사용

* 컴포넌트라고 해서 항상 재사용해야하는 건 아닐 것. 재사용도 맥락에 따라 선택하면 된다.
* 리액트 공식 문서에서도 컴포넌트를 이렇게 정의하고 있음.

<figure><img src="../../assets/reusable-component.png" alt=""><figcaption><p>마크업, CSS, JavsScript를 <strong>/</strong> 앱의 ‘재사용 가능한(reusable)’ UI 요소로 / 사용자가 원하는대로 “컴포넌트”로써 결합할 수 있게 함</p></figcaption></figure>

마크업, CSS, JS 이 3가지 즉 “마크업, 스타일, 상호작용”을 묶어둘 필요가 있으면 컴포넌트가 될 수 있음. 워딩이 ‘재사용 가능한’이므로 이건 본인의 선택사항일 것이다.

### 재사용 가능한 컴포넌트가 실버 불렛?

> `SigninButton`, `SubmitButton` 이든 모든 `Button` 관련 컴포넌트를 하나의 Button 공통 컴포넌트로 재사용 가능한가?

버튼의 기능적 역할은 비슷하겠지만, 스타일이 달라서 재사용 못하는 경우가 꽤 많았다. 이걸 고려해서 만들어두지 않으면 구현이 바쁜 시기에 공통 컴포넌트를 수정하거나 새로 만들고 테스트하고 검증하는 과정이 부담스러웠다. 검증에 품이 많이 들고, 리스크를 지는 선택을 피하고 싶기 때문. 실제로 내가 구현하면서, 동일한 버튼(예시)이지만 Button 컴포넌트를 재사용하지 않고 구현한 것은 없는지 체크해보자.



### 추상화

#### 생각) 추상화도 결국 문제를 해결하는 수단.

낮은 유연성과 확장성을 가진 컴포넌트를 보고, 항상 문제라고 볼 수 있을까? 잠재적 문제의 원인이 될 수 있지만, 상황에 따라 다를 것. 과도한 추상화를 경계해야 할 필요도 있을 것이다.

생각) 추상화는 사실 쉽다.

반복을 피하기 위해 추상화를 시도하는 것은 가장 쉬운 선택이 될 수 있을 것. 추상화를 가능한 미루는 것도 방법이 될 것이다. 눈에 보이는 반복되는 코드를 정리하는 차원이 유의미하긴 하지만, 이것이 가져오는 부작용도 trade-off일 것이다.

예를 들어 중복된 코드를 묶어 하나의 함수로 만들었는데, 나중에 새로운 요구사항이 생기면 어떡할까? 또 선택할 수 있는 옵션이 있을거다. 기존 추상화를 유지하거나 버리거나. 유지하더라도 새 요구사항에 대응해야 하기 때문에 당연히 기존 함수에 파라미터를 추가하든, 비동기 외에 동기 처리를 하는 로직을 추가하든 변형을 가해야 한다.

이렇게 단순한 공통 기능을 처리하는게 아니라, 다양한 엣지 케이스를 처리하는 무거운 코드가 될 수도 있다. 이미 많은 시간을 들여 컨텍스트가 쌓인 함수를 버리고 다시 시작하는 것도 심리적으로 쉬운 선택은 아니다.

{% embed url="https://velog.io/@clydehan/%EC%A2%8B%EC%9D%80-%EC%B6%94%EC%83%81%ED%99%94%EC%99%80-%EB%82%98%EC%81%9C-%EC%B6%94%EC%83%81%ED%99%94" %}

### 좋은 코드

#### 코드는 비즈니스를 함에 있어, 짐이 되면 안된다.

* 발췌) 좋은 코드란 반복이 적은 코드가 아니라, **요구사항을 정확하고 빠르게 반영하고/할 수 있는 코드**임을 항상 명심해야합니다. (출처 '코딩에서 사용하는 추상화')
* 코드는 비즈니스와 상호 보완적인 관계가 될 수 있을 것.

{% embed url="https://pgo-dev.medium.com/%EC%B6%94%EC%83%81%ED%99%94%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-bb8f3e6a8a1d" %}

### 컴포넌트 라이프사이클

* 컴포넌트는 생성되고 화면에 나타났다가 사라짐. 이 일련의 흐름을 생애주기라고 하는데, 함수형 컴포넌트 기준으로 이해하는 것과 클래스 컴포넌트 기준으로 이해하는 것 사이에 일부 차이가 있음.
* 함수형 컴포넌트 기준
  * 마운트 (mount)
  * 업데이트 (update)
  * 언마운트 (unmount)

```javascript
useEffect(() => {
  console.log('마운트됨');

  return () => {
    console.log('언마운트됨');
  };
}, []);

useEffect(() => {
  console.log('업데이트됨');
}, [someState]);
```



생애주기 (이해하기 쉽게 도식화 수정)

```
컴포넌트 생명주기 (Function Component Lifecycle)
──────────────────────────────────────────────

1. 마운트 (Mount)
────────────────────
  ┌─> [1] 컴포넌트 함수 호출
  │     - JSX 반환
  │     - 내부 state 초기화 (useState)
  │
  └─> [2] Virtual DOM 생성
        - 리액트가 JSX → Virtual DOM 트리 구성

  └─> [3] Reconciliation
        - 비교 대상 없음 (초기 렌더)
        - 변화 트리(Diff Tree) 구성

  └─> [4] Commit Phase (DOM 반영)
        - 실제 DOM 노드 생성 및 삽입
        - setAttribute, appendChild 등 수행

  └─> [5] Ref 연결
        - useRef로 선언한 ref가 DOM 요소에 바인딩

  └─> [6] useLayoutEffect 실행
        - DOM이 커밋된 즉시, Paint 전에 동기 실행

  └─> [7] Browser Paint
        - 화면에 사용자 UI 표시됨

  └─> [8] useEffect 실행
        - 비동기 실행 (화면 렌더 이후)
        - 주로 데이터 요청, 이벤트 리스너 등

──────────────────────────────────────────────

2. 업데이트 (Update)
────────────────────
  ┌─> [1] props 또는 state 변경 감지
  │     - setState, 부모 컴포넌트 변경 등

  └─> [2] 컴포넌트 함수 재호출
        - 최신 props, state 기반으로 JSX 재생성

  └─> [3] Virtual DOM 재생성
        - 변경된 구조 계산됨

  └─> [4] Reconciliation (비교)
        - 이전 VDOM과 비교하여 변화 추적
        - 최소한의 변경만 추적

  └─> [5] Commit Phase (DOM 반영)
        - 변경된 부분만 실제 DOM에 적용
        - setAttribute, removeChild 등

  └─> [6] Ref 업데이트
        - 필요한 경우 새로운 DOM 참조 연결

  └─> [7] useLayoutEffect 정리 및 재실행
        - 이전 layout effect → cleanup
        - 새로운 layout effect 실행

  └─> [8] useEffect 정리 및 재실행
        - 이전 effect → cleanup
        - 새로운 effect 실행

──────────────────────────────────────────────

3. 언마운트 (Unmount)
────────────────────
  ┌─> [1] 컴포넌트 제거 조건 발생
        - 조건부 렌더링, 라우팅 등

  └─> [2] Cleanup Phase
        - useEffect의 cleanup 함수 실행
        - useLayoutEffect의 cleanup 함수 실행

  └─> [3] Commit Phase (DOM 제거)
        - DOM 요소 제거
        - ref 정리

──────────────────────────────────────────────

※ 참고 요약

- useLayoutEffect
  - DOM 커밋 직후, Paint 전에 동기 실행됨
  - 레이아웃 측정 등에 적합

- useEffect
  - 브라우저 Paint 이후 비동기 실행
  - 네트워크 요청, 이벤트 등록 등에 적합

- cleanup 함수
  - useEffect/useLayoutEffect 내부 return 함수
  - 언마운트 시 또는 재실행 전 호출됨
```
