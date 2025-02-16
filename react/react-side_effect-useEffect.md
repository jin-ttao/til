# react-side\_effect-useEffect

## Side Effect & useEffect

### context

\


### opinion

#### 1. 왜 side effect 가 중요한 개념으로 불리나? (WIP)

\


#### 2. 왜 비동기로 하는 게 따로 만들어졌나? (WIP)

* 렌더링 하는 도중에, 동기적으로 무언가 바뀌지 않기를 원할 떄 사용하는 것이 맞을까? (검증 필요)
* 콜스택 구조상 LIFO이기 때문에 함수 도중 함수 바깥의 무언가 건드리면, 렌더링 과정이 꼬일 수 있어서 이러한 부분을 잘 통제하는 것이 중요해진 것은 아닐까? (검증 필요)

\


#### 3.

\


### research

#### 1.

\


#### 2.

\


#### 3.

\
\


## useEffect

### context

\


### opinion

#### 1. 의존성 배열에 아무 값도 없으면, 예상치 못한 동작이나 무한 루프가 발생할 수 있는 이유가 뭘까? useEffect가 의존하는 것이 없다면, useEffect는 아무것도 안하는 것 아닐까?

\


#### 2. useEffect 내부에 setter 함수를 함수형 업데이트(예: `setCount(cnt => cnt + 1)`)로 사용하면, 의존성 배열이 비어있어도 정확한 값을 참조할 수 있다고 한다. 그럼 의존성 배열을 빈배열로 두는 것 자체는 항상 나쁜 관습은 아닐까?

* 의존성 배열이 빈 배열일 경우, 컴포넌트가 최초 마운트 될 때 1번만 실행되기 때문에 리렌더링 될 상황을 걱정하지 않아도 되겠지만 상황에 알맞게 가져다 쓰는 것이 필요할 것 같다. 하지만 아직 빈 배열을 의존성 배열로 쓰면 유용한 상황이 깔끔하게 정리가 되지 않아서 확인이 필요할 듯 하다.

\


#### 3.

\


### research

#### 1. useEffect의 의존성 배열

> (공식 문서) _The list of all reactive values referenced inside of the setup code. Reactive values include props, state, and all the variables and functions declared directly inside your component body._

* 키워드
  * useEffect 내부 셋업 코드에서 참조하는 (referenced inside of the setup code)
  * 변경될 수 있는 모든 값들 (all reactive values / include props, state, and all the variables and functions)
* 의존성 배열 안에 있는 값이 변할 때를 감지해서, useEffect 내부 코드(정리함수 둘다?)가 실행됨.

**case1. 의존성이 없는 경우 (빈 배열): useEffect 외부와의 안테나가 끊어진 상태임을 유의하자.**

```js
useEffect(() => {
  setCount(count + 1);
}, []);
```

* 컴포넌트가 마운트될 때 단 한 번만 (useEffect 내 모든 코드가?)실행되고, 이후에는 아무 것도 하지 않음.
* 위 예시에서 문제는, useEffect 바깥에서 바뀌는 `count` 값을 감지할 수 있는 안테나가 끊어졌다는 것이다.
  * useEffect 내부 setCount 함수는 `count`를 참조하는데, 의존성 배열이 비어있기 때문에 처음 알고 있던 초기값만 항상 참조하게 된다. 초기값이 0이었다면, setCount(count + 1)의 결과는 항상 1이 될 것인데, 이건 의도한 결과가 아닐 것이니 주의가 필요한 것.
* (의견) 만약 useEffect를 최초 마운트 때 단 1번만 실행하고 싶으면 어떡하지? => 먼저, 단 1번만 실행하고 싶다는 상황이 정확히 어떤 상황인가?

\


#### 2. 주의: 의존성 배열로 인해 계속 렌더링이 발생하지는 않을지 점검하자. 가급적 리렌더링을 야기하지 않는 구조로 짜보려고 고민할 것.

> (공식 문서) _If you need to keep track of some data that isn’t used by rendering, a ref (which doesn’t trigger re-renders) might be more appropriate. Verify your Effect doesn’t update the state (and trigger re-renders) more than needed._ [링크](https://react.dev/reference/react/useEffect#my-effect-keeps-re-running-in-an-infinite-cycle)

* useEffect 사용시 '의존성 배열'을 잘 관리해야, 렌더링이 계속 발생하는 상황을 막을 수 있다.
* useEffect 쓸 때 체크리스트
  * useEffect는 자신이 변경하는 '상태'를 의존성 배열로 갖고 있어야 한다.
    * useEffect 내부 실행 코드에서 무언가의 '상태'를 변경한다면, 해당 '상태'가 의존성 배열에 포함되어 있는지 확인하자.
    * 만약 포함하지 않는다면 아래와 같은 상황이 될 수 있기 때문이다.
      * '상태' 변경 > 컴포넌트 리렌더링 > .. 정확한 flow, 이유 확인 필요! #다시보기
  * 단, 함수형 업데이트(예: `setCount(cnt => cnt + 1)`)를 사용하면, 의존성 배열이 비어있어도 정확한 값 참조할 수 있음.

#### 3. cleanup 함수를 항상 써서, useEffect setup 함수를 일회용으로 쓰도록 하자 (최적화, 관습 측면).

> (공식 문서) _React will first run the cleanup function (if you provided it) with the old values, and then run your setup function with the new values. After your component is removed from the DOM, React will run your cleanup function._ [링크](https://react.dev/reference/react/useEffect#parameters)

* 메모리 누수를 방지하기 위해, useEffect 내에서 시작된 모든 작업은 컴포넌트가 언마운트 될 때 정리되어야.
* 컴포넌트의 생명주기에 따라 로직이 효율적으로 관리할 수 있고, 성능도 최적화할 수 있음.

\
