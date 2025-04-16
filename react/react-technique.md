# React 사용해보면서

## opinion

## research

`<div key={keywordId} >`에서 key 있고 없고의 차이 리액트는 이걸로 무엇을 처리하나, 결과가 달라지는지? key도 prop이므로 달라지면 완전히 새로 그린다.

```js
{
  isError ? (
    <div>에러 메시지</div>
  ) : (
    <>
      {dashboardType === "chart" ? (
        <div>차트</div>
      ) : (
        <div key={keywordId}>
          <PostListFilter />
          <PostCardList keywordId={keywordId} />
        </div>
      )}
    </>
  );
}
```

아래 2개의 차이는? 괄호 있고 없고 어떻게 판단해야 하나? 어떤 개념을 알아야 하나?

```js
useEffect(() => {
  setFilterList(() => {
    includedKeyword: [],
    excludedKeyword: [],
  });
}, [keywordId])

useEffect(() => {
  setFilterList(() => ({
    includedKeyword: [],
    excludedKeyword: [],
  });
}, [keywordId])
```

* `<del>` 이런 태그도 있구나.. 처음 알았다. 리액트에서 자주 쓰일 수 있는 태그를 한번 훑어보면 좋을 것 같다.
*   아래 공식 문서 예시처럼 컴포넌트를 더 잘게 쪼개는 연습. 모든 분기를 부모에서 할 필요 없이, 자식에서도 해보는 연습. [공식문서](https://ko.react.dev/learn/conditional-rendering#conditionally-assigning-jsx-to-a-variable)

    ```js
    function Item({ name, isPacked }) {
      let itemContent = name;
      if (isPacked) {
        itemContent = name + " ✅";
      }
      return <li className="item">{itemContent}</li>;
    }

    export default function PackingList() {
      return (
        <section>
          <h1>Sally Ride's Packing List</h1>
          <ul>
            <Item isPacked={true} name="Space suit" />
            <Item isPacked={true} name="Helmet with a golden leaf" />
            <Item isPacked={false} name="Photo of Tam" />
          </ul>
        </section>
      );
    }
    ```
