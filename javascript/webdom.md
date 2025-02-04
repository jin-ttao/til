# Web & DOM

<!-- toc -->

- [`querySelector`, `getElementById`는 무엇이 다를까? 각각 언제 사용하면 좋을까?](#queryselector-getelementbyid%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B4-%EB%8B%A4%EB%A5%BC%EA%B9%8C-%EA%B0%81%EA%B0%81-%EC%96%B8%EC%A0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%A9%B4-%EC%A2%8B%EC%9D%84%EA%B9%8C)

<!-- tocstop -->

## `querySelector`, `getElementById`는 무엇이 다를까? 각각 언제 사용하면 좋을까?

요전까진 ‘`querySelector`를 쓰자’고 개인적으로 기준을 잡았었다. 통일성이 가장 큰 이유 였는데, 다른 이유도 다시 찾아보고 보완해봐야겠다. 둘 중 확실히 뭐가 나중에, 왜 생겼을지도 궁금하다. 우선 그 전 이유들을 떠올려보면,

- 내 코드에선 `querySelector`와 `querySelectorAll`만 두려고 했다. 가독성, 예측하기 좋을거라 봤기 때문이다.
- 결국 DOM 객체를 1개 or N개를 가져오는 상황이 전부인데, 이 2가지 ‘도구’만으로 충분히 가능하다면 선택지를 넓힐 필요가 없다고 생각했다.
- 가져올 선택자에 따라 `getElementByClassName`, `getElementById` 등 매번 달리하는게 작성하는 것고 ‘비용’이라고 생각한 것이다.

사실 성능은 크기 고려하지 않았던 것 같다. ‘성능 차이로 둘 중 뭐 하나 강하게 권장하는 건 없구나’ 생각해서. 다시 생각해보니, 앱이 복잡해지면 성능차도 커질 것 같아서 생각해볼 주제일 것 같다. 구체적인 수치도 조사해보자. #추가확인

#추가확인 그러고 보니 React도 굳이 `getElementById`를 써서 root를 가져온다.

```js
ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <RouterProvider router={router} />
    </Provider>
  </React.StrictMode>
);
```
