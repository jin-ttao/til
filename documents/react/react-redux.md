

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
import { Provider, useSelector, useDispatch } from 'react-redux';
// redux-toolkit
import { configureStore, createSlice } from '@reduxjs/toolkit';
```