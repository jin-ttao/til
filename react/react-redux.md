리덕스는 단방향 구조로 어떻게 이걸 가능하게 하지? 흐름을 한번 내 언어로 정리해보자.

Redux 구조에서 상태 변경하기

1. 액션을 디스패치 해야 함

---

1. Redux Toolkit을 활용한 애플리케이션 Redux 앱 셋업 방법
2. 주요 Redux API 셋업 방법

#### Redux, Redux 코어, Redux Toolkit의 차이점

- react-redux와 redux-toolkit은 서로 다른 목적을 가진 보완적인 라이브러리
- redux-toolkit으로 Redux 로직을 작성(Redux 로직 자체의 작성을 간소화)하고, react-redux로 이를 React 컴포넌트에 연결(Redux와 React의 통합에 초점)

```js
// react-redux
import { Provider, useSelector, useDispatch } from "react-redux";
// redux-toolkit
import { configureStore, createSlice } from "@reduxjs/toolkit";
```

#추가확인

1. 어떤 의미로 reducer 단어를 쓸까? 역할이 연관있나? reducer라는 단어를 왜 사용하나.
2. configureStore 함수는 매개변수로 뭐가 들어가고, 무엇을 반환하는지. 그리고 내부 동작의 핵심 단계와 각 단계별 결과물이 궁금하다.
3. 왜 reducer라는 프로퍼티가 user, userReducer를 품고 있을까. 다른 slice 추가하려면 어떻게 코드를 작성하면 될까?
