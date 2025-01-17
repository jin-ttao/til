# Side Effect & useEffect

<!-- toc -->

  * [context](#context)
  * [opinion](#opinion)
    + [1. 왜 side effect 가 중요한 개념으로 불리나? (WIP)](#1-%EC%99%9C-side-effect-%EA%B0%80-%EC%A4%91%EC%9A%94%ED%95%9C-%EA%B0%9C%EB%85%90%EC%9C%BC%EB%A1%9C-%EB%B6%88%EB%A6%AC%EB%82%98-wip)
    + [2. 왜 비동기로 하는 게 따로 만들어졌나? (WIP)](#2-%EC%99%9C-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%A1%9C-%ED%95%98%EB%8A%94-%EA%B2%8C-%EB%94%B0%EB%A1%9C-%EB%A7%8C%EB%93%A4%EC%96%B4%EC%A1%8C%EB%82%98-wip)
    + [3.](#3)
  * [research](#research)
    + [1.](#1)
    + [2.](#2)
    + [3.](#3-1)
- [useEffect](#useeffect)
  * [context](#context-1)
  * [opinion](#opinion-1)
    + [1. 의존성 배열에 아무 값도 없으면, 예상치 못한 동작이나 무한 루프가 발생할 수 있는 이유가 뭘까? useEffect가 의존하는 것이 없다면, useEffect는 아무것도 안하는 것 아닐까?](#1-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4%EC%97%90-%EC%95%84%EB%AC%B4-%EA%B0%92%EB%8F%84-%EC%97%86%EC%9C%BC%EB%A9%B4-%EC%98%88%EC%83%81%EC%B9%98-%EB%AA%BB%ED%95%9C-%EB%8F%99%EC%9E%91%EC%9D%B4%EB%82%98-%EB%AC%B4%ED%95%9C-%EB%A3%A8%ED%94%84%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EC%9D%B4%EC%9C%A0%EA%B0%80-%EB%AD%98%EA%B9%8C-useeffect%EA%B0%80-%EC%9D%98%EC%A1%B4%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EC%97%86%EB%8B%A4%EB%A9%B4-useeffect%EB%8A%94-%EC%95%84%EB%AC%B4%EA%B2%83%EB%8F%84-%EC%95%88%ED%95%98%EB%8A%94-%EA%B2%83-%EC%95%84%EB%8B%90%EA%B9%8C)
    + [2. useEffect 내부에 setter 함수를 함수형 업데이트(예: `setCount(cnt => cnt + 1)`)로 사용하면, 의존성 배열이 비어있어도 정확한 값을 참조할 수 있다고 한다. 그럼 의존성 배열을 빈배열로 두는 것 자체는 항상 나쁜 관습은 아닐까?](#2-useeffect-%EB%82%B4%EB%B6%80%EC%97%90-setter-%ED%95%A8%EC%88%98%EB%A5%BC-%ED%95%A8%EC%88%98%ED%98%95-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8%EC%98%88-setcountcnt--cnt--1%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%A9%B4-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4%EC%9D%B4-%EB%B9%84%EC%96%B4%EC%9E%88%EC%96%B4%EB%8F%84-%EC%A0%95%ED%99%95%ED%95%9C-%EA%B0%92%EC%9D%84-%EC%B0%B8%EC%A1%B0%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8B%A4%EA%B3%A0-%ED%95%9C%EB%8B%A4-%EA%B7%B8%EB%9F%BC-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4%EC%9D%84-%EB%B9%88%EB%B0%B0%EC%97%B4%EB%A1%9C-%EB%91%90%EB%8A%94-%EA%B2%83-%EC%9E%90%EC%B2%B4%EB%8A%94-%ED%95%AD%EC%83%81-%EB%82%98%EC%81%9C-%EA%B4%80%EC%8A%B5%EC%9D%80-%EC%95%84%EB%8B%90%EA%B9%8C)
    + [3.](#3-2)
  * [research](#research-1)
    + [1. useEffect의 의존성 배열](#1-useeffect%EC%9D%98-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4)
      - [case1. 의존성이 없는 경우 (빈 배열): useEffect 외부와의 안테나가 끊어진 상태임을 유의하자.](#case1-%EC%9D%98%EC%A1%B4%EC%84%B1%EC%9D%B4-%EC%97%86%EB%8A%94-%EA%B2%BD%EC%9A%B0-%EB%B9%88-%EB%B0%B0%EC%97%B4-useeffect-%EC%99%B8%EB%B6%80%EC%99%80%EC%9D%98-%EC%95%88%ED%85%8C%EB%82%98%EA%B0%80-%EB%81%8A%EC%96%B4%EC%A7%84-%EC%83%81%ED%83%9C%EC%9E%84%EC%9D%84-%EC%9C%A0%EC%9D%98%ED%95%98%EC%9E%90)
    + [2. 주의: 의존성 배열로 인해 계속 렌더링이 발생하지는 않을지 점검하자. 가급적 리렌더링을 야기하지 않는 구조로 짜보려고 고민할 것.](#2-%EC%A3%BC%EC%9D%98-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4%EB%A1%9C-%EC%9D%B8%ED%95%B4-%EA%B3%84%EC%86%8D-%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EC%A7%80%EB%8A%94-%EC%95%8A%EC%9D%84%EC%A7%80-%EC%A0%90%EA%B2%80%ED%95%98%EC%9E%90-%EA%B0%80%EA%B8%89%EC%A0%81-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%84-%EC%95%BC%EA%B8%B0%ED%95%98%EC%A7%80-%EC%95%8A%EB%8A%94-%EA%B5%AC%EC%A1%B0%EB%A1%9C-%EC%A7%9C%EB%B3%B4%EB%A0%A4%EA%B3%A0-%EA%B3%A0%EB%AF%BC%ED%95%A0-%EA%B2%83)
    + [3. cleanup 함수를 항상 써서, useEffect setup 함수를 일회용으로 쓰도록 하자 (최적화, 관습 측면).](#3-cleanup-%ED%95%A8%EC%88%98%EB%A5%BC-%ED%95%AD%EC%83%81-%EC%8D%A8%EC%84%9C-useeffect-setup-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%BC%ED%9A%8C%EC%9A%A9%EC%9C%BC%EB%A1%9C-%EC%93%B0%EB%8F%84%EB%A1%9D-%ED%95%98%EC%9E%90-%EC%B5%9C%EC%A0%81%ED%99%94-%EA%B4%80%EC%8A%B5-%EC%B8%A1%EB%A9%B4)

<!-- tocstop -->

## context

<br>

## opinion

### 1. 왜 side effect 가 중요한 개념으로 불리나? (WIP)

<br>

### 2. 왜 비동기로 하는 게 따로 만들어졌나? (WIP)

- 렌더링 하는 도중에, 동기적으로 무언가 바뀌지 않기를 원할 떄 사용하는 것이 맞을까? (검증 필요)
- 콜스택 구조상 LIFO이기 때문에 함수 도중 함수 바깥의 무언가 건드리면, 렌더링 과정이 꼬일 수 있어서 이러한 부분을 잘 통제하는 것이 중요해진 것은 아닐까? (검증 필요)

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
<br>

# useEffect

## context

<br>

## opinion

### 1. 의존성 배열에 아무 값도 없으면, 예상치 못한 동작이나 무한 루프가 발생할 수 있는 이유가 뭘까? useEffect가 의존하는 것이 없다면, useEffect는 아무것도 안하는 것 아닐까?

<br>

### 2. useEffect 내부에 setter 함수를 함수형 업데이트(예: `setCount(cnt => cnt + 1)`)로 사용하면, 의존성 배열이 비어있어도 정확한 값을 참조할 수 있다고 한다. 그럼 의존성 배열을 빈배열로 두는 것 자체는 항상 나쁜 관습은 아닐까?

- 의존성 배열이 빈 배열일 경우, 컴포넌트가 최초 마운트 될 때 1번만 실행되기 때문에 리렌더링 될 상황을 걱정하지 않아도 되겠지만 상황에 알맞게 가져다 쓰는 것이 필요할 것 같다. 하지만 아직 빈 배열을 의존성 배열로 쓰면 유용한 상황이 깔끔하게 정리가 되지 않아서 확인이 필요할 듯 하다.

<br>

### 3.

<br>

## research

### 1. useEffect의 의존성 배열

> (공식 문서)
> _The list of all reactive values referenced inside of the setup code. Reactive values include props, state, and all the variables and functions declared directly inside your component body._

- 키워드
  - useEffect 내부 셋업 코드에서 참조하는 (referenced inside of the setup code)
  - 변경될 수 있는 모든 값들 (all reactive values / include props, state, and all the variables and functions)
- 의존성 배열 안에 있는 값이 변할 때를 감지해서, useEffect 내부 코드(정리함수 둘다?)가 실행됨.

#### case1. 의존성이 없는 경우 (빈 배열): useEffect 외부와의 안테나가 끊어진 상태임을 유의하자.

```js
useEffect(() => {
  setCount(count + 1);
}, []);
```

- 컴포넌트가 마운트될 때 단 한 번만 (useEffect 내 모든 코드가?)실행되고, 이후에는 아무 것도 하지 않음.
- 위 예시에서 문제는, useEffect 바깥에서 바뀌는 `count` 값을 감지할 수 있는 안테나가 끊어졌다는 것이다.

  - useEffect 내부 setCount 함수는 `count`를 참조하는데, 의존성 배열이 비어있기 때문에 처음 알고 있던 초기값만 항상 참조하게 된다. 초기값이 0이었다면, setCount(count + 1)의 결과는 항상 1이 될 것인데, 이건 의도한 결과가 아닐 것이니 주의가 필요한 것.

- (의견) 만약 useEffect를 최초 마운트 때 단 1번만 실행하고 싶으면 어떡하지? => 먼저, 단 1번만 실행하고 싶다는 상황이 정확히 어떤 상황인가?

<br>

### 2. 주의: 의존성 배열로 인해 계속 렌더링이 발생하지는 않을지 점검하자. 가급적 리렌더링을 야기하지 않는 구조로 짜보려고 고민할 것.

> (공식 문서) _If you need to keep track of some data that isn’t used by rendering, a ref (which doesn’t trigger re-renders) might be more appropriate. Verify your Effect doesn’t update the state (and trigger re-renders) more than needed._ [링크](https://react.dev/reference/react/useEffect#my-effect-keeps-re-running-in-an-infinite-cycle)

- useEffect 사용시 '의존성 배열'을 잘 관리해야, 렌더링이 계속 발생하는 상황을 막을 수 있다.
- useEffect 쓸 때 체크리스트
  - useEffect는 자신이 변경하는 '상태'를 의존성 배열로 갖고 있어야 한다.
    - useEffect 내부 실행 코드에서 무언가의 '상태'를 변경한다면, 해당 '상태'가 의존성 배열에 포함되어 있는지 확인하자.
    - 만약 포함하지 않는다면 아래와 같은 상황이 될 수 있기 때문이다.
      - '상태' 변경 > 컴포넌트 리렌더링 > .. 정확한 flow, 이유 확인 필요! #다시보기
  - 단, 함수형 업데이트(예: `setCount(cnt => cnt + 1)`)를 사용하면, 의존성 배열이 비어있어도 정확한 값 참조할 수 있음.

### 3. cleanup 함수를 항상 써서, useEffect setup 함수를 일회용으로 쓰도록 하자 (최적화, 관습 측면).

> (공식 문서) _React will first run the cleanup function (if you provided it) with the old values, and then run your setup function with the new values. After your component is removed from the DOM, React will run your cleanup function._ [링크](https://react.dev/reference/react/useEffect#parameters)

- 메모리 누수를 방지하기 위해, useEffect 내에서 시작된 모든 작업은 컴포넌트가 언마운트 될 때 정리되어야.
- 컴포넌트의 생명주기에 따라 로직이 효율적으로 관리할 수 있고, 성능도 최적화할 수 있음.

<br>
