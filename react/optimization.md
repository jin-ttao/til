# Optimization

## lazy component

* 정의
  * 필요할 때만 로드하면 되는 컴포넌트
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

## suspense

구현방법

동작 흐름

