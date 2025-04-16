# Optimization

## lazy component

* 정의
  * 필요할 때만 로드하면 되는 컴포넌트
  * 최적화 가능하게 하는 원리는 "JS 번들 분리"
    * lazy import 하면 해당 컴포넌트의 JS 번들 분리함
* 언제 사용?
  * 늘 그렇지만 최적화가 필요하겠다 판단이 들 때
  * 꼭 처음 부터 렌더링 할 필요 없는 컴포넌트가 있을 때
    * 예시: 사용자가 직접 진입하지 않는 페이지, 무거운 UI, 초기 렌더에 꼭 필요하지 않은 하위 컴포넌트들
  * 체크) 라우트 기반 분할 (code splitting)에 유용한 이유는?
* 다른 대안은?
  * ...

```javascript
import React, { lazy, Suspense } from 'react';

// import 지연
const MyComponent = lazy(() => import('./MyComponent'));

function App() {
  return (
    // 로딩 중 보여줄 fallback UI 지정해줌
    <Suspense fallback={<div>로딩 중...</div>}>
      <MyComponent />
    </Suspense>
  );
}
```

* Lazy Component는 import만 lazy 하면 끝? + Suspense와 꼭 함께 써야 하는가?
  * Suspense와 항상 세트로 사용해야 의도대로 완전한 동작 가능함.
  * lazy import 한다고 React가 특정 컴포넌트가 로딩중이라는 걸 알 수 없음.
  * Suspense로 까지 감싸줘야 로딩중임을 React가 알 수 있음. 그 사이 보여줄 fallback ui도 설정할 수 있음.
  *



## Suspense

> `<Suspense>` lets you display a fallback until its children have finished loading.

정의

* 자식 컴포넌트가 로딩이 끝날 때 까지 fallback ui를 보여주도록 하는 컴포넌트

언제 왜 사용?

* 자식 컴포넌트가 (의도대로/의도와 관계 없이) 로딩이 오래 걸릴 때&#x20;
  * 비동기 처리 (TanStack Qeury 기반 컴포넌트 혹은 데이터 페칭 기반 Server Component)
  * lazy 컴포넌트 로딩

동작 흐름

*

구현방법

*

```javascript
import React, { lazy, Suspense } from 'react';

const Profile = lazy(() => import('./Profile'));

function App() {
  return (
    // fallback으로는 컴포넌트 대신 어떤 JSX 든 가능함.
      // <div>프로필 불러오는 중...</div>
    <Suspense fallback={<Loading />}>
      <Profile />
    </Suspense>
  );
}
```

