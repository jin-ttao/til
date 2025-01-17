# React Inside

<!-- toc -->

- [Opinion](#opinion)
  - [infinite loop Error가 발생했는데, 유용한 정보들이 있는 듯 하다. 리액트 내부 동작 알 수 있는 부분들 체크.](#infinite-loop-error%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%96%88%EB%8A%94%EB%8D%B0-%EC%9C%A0%EC%9A%A9%ED%95%9C-%EC%A0%95%EB%B3%B4%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%8A%94-%EB%93%AF-%ED%95%98%EB%8B%A4-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%82%B4%EB%B6%80-%EB%8F%99%EC%9E%91-%EC%95%8C-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B6%80%EB%B6%84%EB%93%A4-%EC%B2%B4%ED%81%AC)
  - [React Strict Mode는 정확히 왜 존재하나?](#react-strict-mode%EB%8A%94-%EC%A0%95%ED%99%95%ED%9E%88-%EC%99%9C-%EC%A1%B4%EC%9E%AC%ED%95%98%EB%82%98)
- [Learned](#learned)

<!-- tocstop -->

## Opinion

### infinite loop Error가 발생했는데, 유용한 정보들이 있는 듯 하다. 리액트 내부 동작 알 수 있는 부분들 체크.

![react-error-infinite-loop](/assets/react-error-infinite-loop.png)

### React Strict Mode는 정확히 왜 존재하나?

- 부수 효과 검출을 위해 존재하나. 그만큼 부수효과가 치명적인걸까. 만약 검출하고 나서 결과에 따라서 리액트가 어떻게 해줄까?

## Learned

리액트는 계산하지 않고, 전달 받은 '값'을 그리기만 할 뿐.
![reac-inside-creatElement](/assets/reac-inside-creatElement.png)

- 추가로 확인
  - HTML 태그가 JSX에서 React element로 변환되는 구체적인 과정은 어떻게 되는지. 태그들이 결국 자바스크립트 객체가 된다는 것일까? 그럼 JSX 안에 있는 모든 코드는 하나의 큰 객체 안에, 각각 자바스크립트 객체가 담겨있는 걸까?

제어 컴포넌트. 비제어 컴포넌트 (useState, ref)

- 왠만하면 제어 컴포넌트 쓸 것. 상태 변수로 데이터 동기화 + 다른 이유도 있음(명재님)?
- 한솔님) 돔ref 먼저 했다가, 상태 보존을 위해 배틀에서 상태로 변경해서 썻음. 제어 컴포넌트

useEffect 의존성 배열 빈배열이면 초기 마운팅에도 실행?

- useEffect: 단순 이벤트 핸들러로 해결할 수 있으면 핸들러로 해결해라. — 퍼퓰러도 이걸로 가능함 (한솔님)
- (명재님) 리액트에서 굳이 ‘부수효과’를 언급했을까? 자바스크립트에서 함수… 함수의 순수성. > 리액트 컴포넌트는 직접 돔 조작을 하지 않음. (>> 객체만 갈아끼워주는 것? == 컴포넌트만 갈아끼워주는 것?)
- (명재님) main.jsx 5-9번줄. ‘/‘는 패키지 안 폴더 를 의미. React, React DOM 둘다 왜 임포트 해올까? 리액트는 2개다 깔아야 함. >> root의 패키지 제이슨. 디펜던시에 리액트, 리엑트돔 따로 있음.

리액트에서 렌더링 정확하게 이해하기.

리액트 - 어떻게 부분만 바뀌는지. 실제 돔에서.

세터 함수 바로 실행하려면, 업데이터 함수.

질문) 그럼 로그만 찍는 외부를 건드리는 것만 하면, 컴포넌트 내부 상태나 데이터를 건드리는 건 안하는게 좋겠다다고 판단?
클린업 함수의 동작 타이밍 정확히…

비동기 - 할당 없이 awiat 만 쓸 수 있음.

리액트 공식 문서
리스트 렌더링 링크
useEffect 클린업 함수 링크
useContext 링크
