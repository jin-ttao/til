# Redux

### 리덕스는 단방향 구조로 어떻게 이걸 가능하게 하지? 흐름을 한번 내 언어로 정리해보자.

Redux 구조에서 상태 변경하기

1. 액션을 디스패치 해야 함

***

1. Redux Toolkit을 활용한 애플리케이션 Redux 앱 셋업 방법
2. 주요 Redux API 셋업 방법

#### Redux, Redux 코어, Redux Toolkit의 차이점

* react-redux와 redux-toolkit은 서로 다른 목적을 가진 보완적인 라이브러리
* redux-toolkit으로 Redux 로직을 작성(Redux 로직 자체의 작성을 간소화)하고, react-redux로 이를 React 컴포넌트에 연결(Redux와 React의 통합에 초점)

```js
// react-redux
import { Provider, useSelector, useDispatch } from "react-redux";
// redux-toolkit
import { configureStore, createSlice } from "@reduxjs/toolkit";
```

\#추가확인

1. 어떤 의미로 reducer 단어를 쓸까? 역할이 연관있나? reducer라는 단어를 왜 사용하나.
2. configureStore 함수는 매개변수로 뭐가 들어가고, 무엇을 반환하는지. 그리고 내부 동작의 핵심 단계와 각 단계별 결과물이 궁금하다.
3. 왜 reducer라는 프로퍼티가 user, userReducer를 품고 있을까. 다른 slice 추가하려면 어떻게 코드를 작성하면 될까?



## Redux Toolkit

### context

* Redux Toolkit은 Redux 로직 작성 방법. Redux에서 공식적으로 추천하는 방법이라 이해하고 내 언어로 소화하기 위해 기록한다.
* 얼핏 보면 Redux, Redux 코어, Redux Toolkit 모두 같은 것을 가르키는 것으로 보이는데, 모두 다른 의미라 각각의 정의도 명확하게 이해해보자.

### content - opinion

![react-redux-realtionship](../../assets/react-redux-files-overview.jpg)

#### createSlice에서 왜 'slice'라고 이름을 붙였을까?

https://redux-toolkit.js.org/api/createSlice

#### createSlice 와 useState의 코드상 차이 말고 역할적 차이는 뭘까?

구조적으로 useState 쓰던 당시에는 컴포넌트들이 서로를 바라보고 상태를 서로 넘겨가면서 공유할 수 밖에 없었다. 하지만 redux 같은 모두와 연결된 상태 라운지/탕비실? 같은 공간을 두고 ...

* reducer 함수가 순수 함수여야 하며, 상태를 직접 변경하지 않고 새로운 상태 객체를 반환한다는 것은 무슨 뜻인가?
* reducer 함수 객체 안의 메소드들의 매개변수로 왜 꼭 state, action이 들어가야 하나?
* 왜 reducer는 함수라는데 왜 그 안에 key, value 쌍으로 함수들이 객체의 프로퍼티로 있는 구조로 짰을까?
* store 파일에서 왜 reducer 객체에 counter 프로퍼티가 있는가? 그리고 그 키의 value는 무엇인가?
* 리덕스에서 상태 업데이트 함수들을 굳이 왜 또 컴포넌트 안으로 옮겨줘야 할까? reducers 함수 안에서 모두 해결할 수 없는 건가?
* createSlice() 함수의 매개변수로 들어가는 name 프로퍼티의 value가 왜 useSelector 하면 해당 value가 key로 useSelector 돼?

### content - research

#### 정의

* Redux Toolkit은 Redux에서 공식적으로 추천하는 Redux 로직 작성 방법.

**=> Redux Toolkit: Redux를 더 간편하게 써보자**

* 기본적인 Redux 작업을 간단하게 만드는 API 제공을 위해 만들어짐.
  * 배경: Redux를 사용하려면 꽤나 장황하고 반복적인 코드가 필요함. 즉 많은 보일러 플레이트 코드들이 필요한데,
* Redux Toolkit 2가지 핵심 API로 간소화가 가능해짐.
  * configureStore: 간편한 store 설정.
  * createSlice: 단 번에 reducer 함수 작성.

#### Redux Toolkit 체크리스트

[링크](https://ko.redux.js.org/tutorials/quick-start/)

* 리액트 리덕스로 리덕스 툴킷 설치하고 사용하기
* 아래 내용은 알고 있다는 전제.
  * Redux Fundamentals, Part 2: Concepts and Data Flow -- [Redux terms and concepts](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow)
    * 본 링크에 리덕스 전체 플로우 정리되어 있으니 #다시보기
  * 이 내용은 포함 안함: Redux가 무엇인지, 어떻게 작동하는지, 그리고 Redux Toolkit을 사용하는 전체적인 예시에 대해서는 "튜토리얼 목차" 페이지에 링크된 다른 튜토리얼들을 참고. [링크](https://ko.redux.js.org/tutorials/index)

#### 1. 설치: Install Redux Toolkit and React-Redux

#### 2. 공용 창고 생성: Create a Redux Store (위치: 별도의 store.js 파일 만들어서)

* store 생성

#### 3. 공용 창고 연결: Provide the Redux Store to React (위치: 메인 js파일인 index.js 파일에서)

* Provider: store를 React 컴포넌트에서 사용할 수 있게 해주는 Provider를 감싸기.

#### 4. Create a Redux State Slice (위치: 해당 상태가 필요한 특정 컴포넌트 파일)

* \#다시보기 -- 어렵다. 보다보니 useState와 비슷한 역할인 것 같다. 상태를 초기값과 함께 처음 선언해주고, 상태 업데이트 함수를 정해주는 것을 보면 공통점이 있다.
* createSlice() 함수
  * 기능1: 상태의 초기값, Reducer 함수의 객체, slice 이름을 받는 함수.
  * 기능2: action 관련 부분 자동 생성 (action creators, action types)
  * (의견) 결국 함수이기 때문에 코드 예시를 보면서 매개변수, 반환값을 보면 역할이 이해될 것.

#### 5. Add Slice Reducers to the Store (위치: #2에서 만들어둔 store.js 파일)

#### 6. Use Redux State & Action in React Components (위치: 해당 상태가 필요한 특정 컴포넌트 파일)

* ✅ 이제 React-Redux 훅 써서, 컴포넌트가 공용 창고(Redux Store) 들락날락('상호작용' 이라 표현) 할 수 있음.
  * 마치 컴포넌트 내부에 상태를 선언하고 그 상태를 쓴 것 처럼, Redux를 쓰고도 상태를 활용할 수 있는 환경이 마련된 것.
  * 이 상태에서 Redux 동작 흐름을 정리하자면:
    * click event 발생 -> 해당 Redux 액션이 store로 전송
    * Redux 액션이 전송되면, 담당 reducer 함수가 액션을 감지하고, 상태를 업데이트 해줌 (#다시보기 reducer의 정확한 역할)
    * 이제 해당 컴포넌트는 당연히 상태가 업데이트 되었으니, 업데이트 된 값으로 컴포넌트 본인을 리렌더링 하는 구조.
* 어떻게?: 데이터 읽기 `useSelector` & 액션 디스패치 `useDispatch`
  * (의견) 마치 js의 `querySelector` 함수처럼 특정 데이터를 선택해서 읽어올 수 있겠다.
  * \#다시보기 액션 디스패치의 의미, 액션을 보내줘야 하는 이유가 뭐일지 체크.

## draft

* '상태'는 만들고 변경할 수 있어야 한다. 그래야 재생산이 가능할 것.
* Redux를 쓸 때, 상태를 변경하려면 '액션을 보내야 한다(dispatch an action)' -- 어디로 구체적으로 무엇을 어떻게 보내나?
