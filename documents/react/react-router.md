# React Router

## opinion

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
<Route exact path="start" element={
  loggedIn ? (
    <Start />
    ) : (
      <Navigate replace to={"/"} />
    )
  }
/>
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
          {isLogin &&
            <Route path="/경로1" exact element={<컴포넌트1 />} >
              <Route path=":파라미터" element={<컴포넌트2 />} />
            </Route>
          }
        </Routes>
    </main>
  )
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

