# React Router

<!-- toc -->

- [opinion](#opinion)
  - [(복기) 모달을 라우트로 제어한 것을 개선하기. 상태로 처리하는게 나았을 것.](#%EB%B3%B5%EA%B8%B0-%EB%AA%A8%EB%8B%AC%EC%9D%84-%EB%9D%BC%EC%9A%B0%ED%8A%B8%EB%A1%9C-%EC%A0%9C%EC%96%B4%ED%95%9C-%EA%B2%83%EC%9D%84-%EA%B0%9C%EC%84%A0%ED%95%98%EA%B8%B0-%EC%83%81%ED%83%9C%EB%A1%9C-%EC%B2%98%EB%A6%AC%ED%95%98%EB%8A%94%EA%B2%8C-%EB%82%98%EC%95%98%EC%9D%84-%EA%B2%83)
  - [사용자의 로그인 여부를 App 컴포넌트에서만 하는게 좋을까, 각 페이지 컴포넌트에서 하는게 좋을까?](#%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%98-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%97%AC%EB%B6%80%EB%A5%BC-app-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%97%90%EC%84%9C%EB%A7%8C-%ED%95%98%EB%8A%94%EA%B2%8C-%EC%A2%8B%EC%9D%84%EA%B9%8C-%EA%B0%81-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%97%90%EC%84%9C-%ED%95%98%EB%8A%94%EA%B2%8C-%EC%A2%8B%EC%9D%84%EA%B9%8C)
    - [배경: 로그인 여부 검사를 안전하게 했는지 스스로 대답하기 어려웠던 상황이었다.](#%EB%B0%B0%EA%B2%BD-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%97%AC%EB%B6%80-%EA%B2%80%EC%82%AC%EB%A5%BC-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%ED%96%88%EB%8A%94%EC%A7%80-%EC%8A%A4%EC%8A%A4%EB%A1%9C-%EB%8C%80%EB%8B%B5%ED%95%98%EA%B8%B0-%EC%96%B4%EB%A0%A4%EC%9B%A0%EB%8D%98-%EC%83%81%ED%99%A9%EC%9D%B4%EC%97%88%EB%8B%A4)
    - [답변: 정답은 없고, 상황 마다 다르다. 본인이 '언제 어디서 로그인을 검사할 것인지' 먼저 정의하는게 중요하고, 그것에 맞게 정확히 구현하는 것이 더 중요하다.](#%EB%8B%B5%EB%B3%80-%EC%A0%95%EB%8B%B5%EC%9D%80-%EC%97%86%EA%B3%A0-%EC%83%81%ED%99%A9-%EB%A7%88%EB%8B%A4-%EB%8B%A4%EB%A5%B4%EB%8B%A4-%EB%B3%B8%EC%9D%B8%EC%9D%B4-%EC%96%B8%EC%A0%9C-%EC%96%B4%EB%94%94%EC%84%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8%EC%9D%84-%EA%B2%80%EC%82%AC%ED%95%A0-%EA%B2%83%EC%9D%B8%EC%A7%80-%EB%A8%BC%EC%A0%80-%EC%A0%95%EC%9D%98%ED%95%98%EB%8A%94%EA%B2%8C-%EC%A4%91%EC%9A%94%ED%95%98%EA%B3%A0-%EA%B7%B8%EA%B2%83%EC%97%90-%EB%A7%9E%EA%B2%8C-%EC%A0%95%ED%99%95%ED%9E%88-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EB%8D%94-%EC%A4%91%EC%9A%94%ED%95%98%EB%8B%A4)
    - [답변에 대한 의견: 로그인 여부를 점검하고 싶은 규칙을 내가 먼저 정의하고, 그걸 정확하게 구현하는 것이 중요하겠다. / 질문 장황하게 하지 말고, 핵심만 3문장으로 줄여보는 연습.](#%EB%8B%B5%EB%B3%80%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%98%EA%B2%AC-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%97%AC%EB%B6%80%EB%A5%BC-%EC%A0%90%EA%B2%80%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%9D%80-%EA%B7%9C%EC%B9%99%EC%9D%84-%EB%82%B4%EA%B0%80-%EB%A8%BC%EC%A0%80-%EC%A0%95%EC%9D%98%ED%95%98%EA%B3%A0-%EA%B7%B8%EA%B1%B8-%EC%A0%95%ED%99%95%ED%95%98%EA%B2%8C-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EC%A4%91%EC%9A%94%ED%95%98%EA%B2%A0%EB%8B%A4--%EC%A7%88%EB%AC%B8-%EC%9E%A5%ED%99%A9%ED%95%98%EA%B2%8C-%ED%95%98%EC%A7%80-%EB%A7%90%EA%B3%A0-%ED%95%B5%EC%8B%AC%EB%A7%8C-3%EB%AC%B8%EC%9E%A5%EC%9C%BC%EB%A1%9C-%EC%A4%84%EC%97%AC%EB%B3%B4%EB%8A%94-%EC%97%B0%EC%8A%B5)
    - [적용해본 것: before, after 비교 - 뭐가 다를까?](#%EC%A0%81%EC%9A%A9%ED%95%B4%EB%B3%B8-%EA%B2%83-before-after-%EB%B9%84%EA%B5%90---%EB%AD%90%EA%B0%80-%EB%8B%A4%EB%A5%BC%EA%B9%8C)
- [중첩 라우팅](#%EC%A4%91%EC%B2%A9-%EB%9D%BC%EC%9A%B0%ED%8C%85)
  - [``으로 prop 넘겨주려면 Hook을 사용해야 한다. (`useoutletcontext`)](#%EC%9C%BC%EB%A1%9C-prop-%EB%84%98%EA%B2%A8%EC%A3%BC%EB%A0%A4%EB%A9%B4-hook%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%9C%EB%8B%A4-useoutletcontext)
- [Router Hook](#router-hook)
  - [useNavigate](#usenavigate)
    - [navigate이 어떤 과정으로 진행되는지 알아?: URL 변경 > 그에 맞는 컴포넌트 준비 > Route 설정된 맨 위부터 리렌더링 시작 > 변경된 부분만 커밋.](#navigate%EC%9D%B4-%EC%96%B4%EB%96%A4-%EA%B3%BC%EC%A0%95%EC%9C%BC%EB%A1%9C-%EC%A7%84%ED%96%89%EB%90%98%EB%8A%94%EC%A7%80-%EC%95%8C%EC%95%84-url-%EB%B3%80%EA%B2%BD--%EA%B7%B8%EC%97%90-%EB%A7%9E%EB%8A%94-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%A4%80%EB%B9%84--route-%EC%84%A4%EC%A0%95%EB%90%9C-%EB%A7%A8-%EC%9C%84%EB%B6%80%ED%84%B0-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%8B%9C%EC%9E%91--%EB%B3%80%EA%B2%BD%EB%90%9C-%EB%B6%80%EB%B6%84%EB%A7%8C-%EC%BB%A4%EB%B0%8B)
  - [useEffect 의존성 배열로 `useNavigate()`의 return 값인 `navigate`를 포함해도 될까? #다시보기](#useeffect-%EC%9D%98%EC%A1%B4%EC%84%B1-%EB%B0%B0%EC%97%B4%EB%A1%9C-usenavigate%EC%9D%98-return-%EA%B0%92%EC%9D%B8-navigate%EB%A5%BC-%ED%8F%AC%ED%95%A8%ED%95%B4%EB%8F%84-%EB%90%A0%EA%B9%8C-%23%EB%8B%A4%EC%8B%9C%EB%B3%B4%EA%B8%B0)

<!-- tocstop -->

## opinion

### (복기) 모달을 라우트로 제어한 것을 개선하기. 상태로 처리하는게 나았을 것.

- 상태로 처리하는게 나았을 것.
  - 모달 중에서도 해당 모달이 페이지의 개념으로 특정 상세 페이지이거나 공유되기를 바란다면 라우트로 설계하는게 적절할 수도 있다.
  - 하지만 그게 아니라 오버레이 성격으로 화면의 일부로 띄우는 거라면 상태로 제어하는게 가장 적절한 수준의 구현이라고 생각됨.
- 생각해본 근거
  1. 단순: 상태 관리로 충분한 기능 구현 가능했을 것.
  2. URL
     - URL 까지 건드릴 것은 아니었던 것 같다. 해당 URL로 바로 진입할 것을 고려한 설계도 아니었음.
     - 현재 구조는 URL 변경이 실제로 "새로운 페이지"가 아닌 오버레이 UI를 위한 것이므로 적절한 사용이 아님.
  3. 뒤로가기 관점
     - 브라우저 뒤로가기 시 라우팅 처리도 불필요하지 않았나..

<br>

### 사용자의 로그인 여부를 App 컴포넌트에서만 하는게 좋을까, 각 페이지 컴포넌트에서 하는게 좋을까?

#### 배경: 로그인 여부 검사를 안전하게 했는지 스스로 대답하기 어려웠던 상황이었다.

- 처음 프로젝트 구현할 때에는, App 컴포넌트에서만 사용자 로그인 여부를 검사했다. 로그인 하지 않으면, 라우팅 자체가 적용되지 않도록 했다. 하지만 App 컴포넌트에서만 로그인 점검 장치를 두었다보니, '로그인 없이 특정 페이지에 접근 못하는 안전하게 구현이 되었는가'에 대해 확신을 갖고 대답하기 어려웠다. 리액트에서 로그인 여부 점검을 어디서 어떤 규칙으로 하는 것이 좋은 방향인지 여쭤보기로 했다.

#### 답변: 정답은 없고, 상황 마다 다르다. 본인이 '언제 어디서 로그인을 검사할 것인지' 먼저 정의하는게 중요하고, 그것에 맞게 정확히 구현하는 것이 더 중요하다.

- 어쨋든, 실제 기능을 매끄럽게 하는게 중요하다.
- 한 가지 방법을 예로 들어보면, 페이지 마다 로그인 여부를 점검해보면 어떨까? 로그인이 예상치 못하게 풀릴 수도 있다. 갑자기 토큰이 만료되거나, 특정 이유로 갑자기 로그인이 풀릴 수 있는데 예측이 어려울 것이다. 그래서 각 페이지 마다 로그인 여부를 점검하고 렌더링 해주는 것도 상황에 따라 적합한 방법이 될 수 있다. next.js 혹은 react router에서 이러한 각 경로마다 특정 조건을 점검하고 렌더링 해주는 장치가 있을 것. 실제로 있을지, 그게 무엇일지는 찾아봐야 한다.
- 이 방향에서 구체적인 방법을 따지자면, App 컴포넌트에서 React Router가 라우팅 해주는 큰 페이지 단위 컴포넌트에서 로그인 조건을 검사하는 방법이 있다. 로그인 여부에 따라 일부 컴포넌트를 on/off할 것이 아니라면, 최하위 작은 컴포넌트 까지 로그인 점검 장치를 둘 필요는 없을 수 있다.
- 다른 방법으로, 만약 App 컴포넌트에서 로그인 여부 검사하는 로직을 그대로 둔다면 어떻게 할 수 있을까? 로그인 여부가 바뀔 때를 감지해서, 그 때 마다 특정 로직을 실행시키는 것을 생각해볼 수 있다. 이때 그럼 useEffect를 써야하나 생각이 들 수 있다. 하지만 useEffect의 특성을 고려해야 한다. 바로, 렌더링이 끝나고 나서 useEffect의 설정 함수가 실행된다는 것. 타이밍을 고려해야 한다. 렌더링이 되어 이미 사용자가 화면을 봤는데, 그제서야 로그인 여부를 점검하는 로직이 돌아서 '로그인 하세요'로 흐름이 가면 어색하지 않을까?

#### 답변에 대한 의견: 로그인 여부를 점검하고 싶은 규칙을 내가 먼저 정의하고, 그걸 정확하게 구현하는 것이 중요하겠다. / 질문 장황하게 하지 말고, 핵심만 3문장으로 줄여보는 연습.

- 질문하기를 잘 했지만, 잘 질문하지 못했다. 상황을 장황하게 설명하고, 마지막에 '그래서 궁금한 것은 이겁니다' 하고 질문했다. 질문 잘 하는 법. 궁금한 것, 궁금한 배경과 시도한 것 3문장 요약해서 상대방이 내 질문을 머리 속에 그릴 수 있게 질문하기. 그리고 내가 정리가 안된 상태일 수 있지만, 내 질문과 내가 궁금한 것은 결국 내가 스스로 정리해야 한다.
- 추가로 찾아본 것: react router conditional routing [출처](https://dev.to/salehmubashar/conditional-routing-with-react-router-v6-229g)
  - 로그인 상태가 참이면 Start 컴포넌트를 반환하지만, 거짓이면 Navigate 요소를 사용하여 사용자를 홈페이지로 리디렉션하는 방법도 있음.
  - 평소 잘 안써봤던 Navigate 엘리먼트도 발견 [공식문서]
    - useNavigate를 감싸는 wrapper component라고 한다.

```js
<Route exact path="start" element={loggedIn ? <Start /> : <Navigate replace to={"/"} />} />
```

- (참고) 인증이 필요한 컴포넌트를 위한 라우트 [출처](https://www.daleseo.com/react-router-authentication/)
  > 사용자가 로그인을 하지 않고 인증이 필요한 컴포넌트에 접근하려는 경우, 접근을 차단하고 로그인 페이지로 보내야합니다. <br> 이 로직을 인증이 필요한 모든 컴포넌트에 넣을 수도 있겠지만, 그러면 코드 중복이 생겨서 유지보수가 어렵게 됩니다. <br> 따라서 React Router의 `<Route/>` 컴포넌트를 확장하여 인증이 필요한 컴포넌트를 위한 전용 라우트를 구현하겠습니다.

#### 적용해본 것: before, after 비교 - 뭐가 다를까?

```js
// before
return (
  <main>
    <Header />
    <Routes>
      <Route path="/" exact element={<홈 />} />
      {isLogin && (
        <Route path="/경로1" exact element={<컴포넌트1 />}>
          <Route path=":파라미터" element={<컴포넌트2 />} />
        </Route>
      )}
    </Routes>
  </main>
);
```

## 중첩 라우팅

- Nested Routing, 말 그대로 2개가 동시에 렌더링 되는 것을 의미한다.
- 상위/하위 컴포넌트를 나누어서 위계를 두어 제어하고 싶거나 모달 등의 컴포넌트를 띄운 상태에서 뒤 배경 컴포넌트도 계속 렌더링을 유지하고 싶을 때 사용했다.
- 프로젝트로 확인한 걸 기록으로 남겨보자면, 중첩된 컴포넌트는 동시 렌더링이 되기 때문에 두 컴포넌트에서 정보를 어느정도 공유하는 것 '처럼' 쓸 수 있다.
  - 로컬 상태가 자동으로 공유되는 건 아니지만, 전역 상태라면 말이 다르다.
  - 부모 컴포넌트에서 전역 상태를 업데이트 해줬으면, 자식 컴포넌트에서 자연스럽게 해당 전역 상태를 자연스럽게 가져와서 사용할 수 있다.
  - 여기서 착각했던 점이 드러나는데, 자식 컴포넌트로 바로 라우팅 하더라도 부모도 렌더링 되고 있는 상태라는 점을 잊지 말자.
  - 이걸 다시 깨닫기 전에, 계속 부모 컴포넌트로 라우팅하고 특정 작업이 완료되면 다시 하위 자식 컴포넌트로 라우팅 해주는 작업을 나눠서 해주고 있었다.
  - 사실 그럴 필요가 없었다. 자식 컴포넌트로 렌더링 해주어도 위에서는 부모가 렌더링, 즉 실행이 된 것이기 때문에 굳이 거쳐갈 이유가 없다.
  - 스스로 중첩 라우팅을 의도했으면서, 이 사실을 간과하지 말자!
- #다시보기 추가 궁금한 것: 중첩 라우팅은 순서대로 부모 > 자식 호출될 것을 보장해주나?
  - 부모 컴포넌트에서 전역 상태를 업데이트 하고, 자식 컴포넌트에서 해당 데이터를 활용해야 하는데 중첩 라우팅이 항상 렌더링 선후관계를 부모 > 자식으로 유지해준다는 보장은 아직 확인하지 못한 것 같다.
  - 만약 자식 컴포넌트 부터 렌더링 부모 컴포넌트가 렌더링되거나, 부모 컴포넌트가 먼저 렌더링되었으나 Effect 타이밍이 밀려 데이터 작업이 안끝났다면 자식 컴포넌트에서 의도대로 해당 데이터를 활용하지 못할 것 같다.
  - 타이밍과 관계 없이 부모 컴포넌트에서 언젠가 전역 상태가 업데이트 되면, 해당 상태를 참조하고 있는 자식 컴포넌트가 반드시 리렌더링 될 것이기 때문에 문제가 되지 않는 걸까?

### `<Outlet />`으로 prop 넘겨주려면 Hook을 사용해야 한다. (`useoutletcontext`)

- 배경: 상위 경로에서 전역 상태를 가져와, 하위 경로에 prop으로 넘겨주었으나 동작하지 않았다. 이렇게 prop으로 넘기기 전 한 가지 의문도 있었는데, 하위 경로 `Outlet`이 2개라 둘 중 어떤 하위경로로 인자를 넘겨주는지 명시하는 것도 필요하지 않을까 생각했다.
- 찾아보니 React Router에서 `Outlet`과 상태, 값을 공유하려면 대체로 `Outlet` 세계관 안의 `useoutletcontext` 훅을 쓰면 된다고 한다. 이렇게 해서 하위 경로 컴포넌트들 중에서도, 필요한 컴포넌트에서만 접근해서 사용하면 되어서 prop으로 넘길 때 들었던 의문도 해소가 되었다.
  > Often parent routes manage state or other values you want shared with child routes. You can create your own context provider if you like, but this is such a common situation that it's built-into <Outlet />:

```js
// parent
function Parent() {
  const [count, setCount] = React.useState(0);
  return <Outlet context={[count, setCount]} />; // 선언
}

// child
import { useOutletContext } from "react-router-dom";

function Child() {
  const [count, setCount] = useOutletContext(); // 활용
  const increment = () => setCount((c) => c + 1);
  return <button onClick={increment}>{count}</button>;
}
```

## Router Hook

### useNavigate

- navigate("이동하고 싶은 경로"): 상대 경로로 작동해서, 현재 경로에서 navigate의 매개변수로 이동시켜줌.
  > A <Navigate> element changes the current location when it is rendered. It's a component wrapper around useNavigate, and accepts all the same arguments as props. <br> It's usually better to use redirect in loaders and actions than this hook <br> The useNavigate hook returns a function that lets you navigate programmatically, for example in an effect: [공식문서](https://reactrouter.com/en/main/hooks/use-navigate)

#### navigate이 어떤 과정으로 진행되는지 알아?: URL 변경 > 그에 맞는 컴포넌트 준비 > Route 설정된 맨 위부터 리렌더링 시작 > 변경된 부분만 커밋.

- navigate이 URL 변경
- React Router가 새 URL에 맞는 컴포넌트 찾아서 렌더링 준비
- 새 Route에 맞는 컴포넌트 렌더링하려고 최상단 App 컴포넌트부터 리렌더링 시작
- 변경된 부분만 실제 DOM에 반영(커밋)

### useEffect 의존성 배열로 `useNavigate()`의 return 값인 `navigate`를 포함해도 될까? #다시보기

```js
// 예시 코드
useEffect(() => {
  (...)
  데이터 요청;
  (...)
  navigate(특정 경로);
}, [dependencies]);
```

useEffect 안에서 외부 시스템으로부터 데이터를 요청, 업데이트하고 이어서 특정 경로로 라우팅하는 경우가 자주 있다. 이때 useEffect 상단부에 데이터 패칭, 하단부에 `navigate(특정 경로)`를 명시하는 패턴을 갖게 된다. 의존성 배열 안에 `navigate`를 포함하지 않으면 Lint Error가 발생하는데, 반응형 값이라 이를 감지한다. 항상 같은 값 혹은 참조를 반환할까?
const navigate = useNavigate();으로 렌더링 될 때 마다 useNavigate의 반환값이 navigate에 할당될 텐데, 참조값으로 매번 새롭게 리액트가 인식하지 않을까?
