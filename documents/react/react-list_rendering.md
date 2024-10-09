# React 리스트 렌더링

## context
> 리스트 렌더링 [공식 문서](https://ko.react.dev/learn/rendering-lists)

- 바닐라 자바스크립트를 배우던 시기에, Tic-Tac-Toe 구현 프로젝트에서 여러 개의 `div` 태그를 구현할 때 동적으로 DOM을 생성해준 적이 있다. 
- 더 이 전에는 일일이 HTML로 `div`를 찍어두었는데, 미리 HTML 코드로 정적 마크업을 만들어두지 않는 편이 좋다. 브라우저가 스크립트를 실행할 때 동적으로 DOM을 만들어주는 것이 몇 개일지 모를 태그를 일일이 만들어주지 않아도 되는 장점이 있다. 무엇 보다 유연하게 대응(e.g. 사용자 입력값 등에 따라 유동적으로 생성) 가능하다는 점도 유용하게 썼던 부분이다.
- 본 문서에서는 자바스크립트에서의 이러한 작업을 당연히 리액트에서도 할 수 있는데, 어떠한 점에서 다른지, 리액트가 어떻게 이 작업을 수행하는지 중심으로 적어보려고 한다.

<br>

## opinion

### 리스트 랜더링 관점에서, Key는 React가 나중에 특정 배열 항목을 구별할 수 있게 해준다고 하는데 그 '나중'은 언제이고, 어떻게 구분할까? 


## research

### 1. 정의

- 유사한(똑같은 X) 컴포넌트를 여러 개 구성하려고 할 때, 로직과 반복 작업으로 원하는 컴포넌트를 만들 수 있다. 대표적으로 map(), filter()를 통해 구현하는 경우가 있다.

*"데이터 모음에서 유사한 컴포넌트를 여러 개 표시하고 싶을 때가 종종 있습니다. JavaScript 배열 메서드를 사용하여 데이터 배열을 조작할 수 있습니다. 이 페이지에서는 React에서 filter()와 map()을 사용해 데이터 배열을 필터링하고 컴포넌트 배열로 변환해보겠습니다."*

<br>

### 2. map() 호출 내부의 JSX 엘리먼트에는 항상 key가 필요하다.

*"Key는 각 컴포넌트가 어떤 배열 항목에 해당하는지 React에 알려주어 나중에 일치시킬 수 있도록 합니다. 이는 배열 항목이 정렬 등으로 인해 이동하거나 삽입되거나 삭제될 수 있는 경우 중요해집니다. key를 잘 선택하면 React가 정확히 무슨 일이 일어났는지 추론하고 DOM 트리에 올바르게 업데이트 하는데 도움이 됩니다."*

- 즉석에서 key를 생성하는 대신 데이터 안에 key를 포함해야 한다. (아래 참고) [공식 문서](https://ko.react.dev/learn/rendering-lists#keeping-list-items-in-order-with-key)

```js
// data.js
export const people = [{
  id: 0, // JSX에서 key로 사용됩니다.
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
  accomplishment: 'spaceflight calculations',
  imageId: 'MK3eW3A'
}, {
// app.js
export default function List() {
  const listItems = people.map(person =>
    <li key={person.id}> 
// 👉 JSX에서 이미 데이터에 있는 값을 key로 가져옴. 여기서 key 직접 만들지 말기.
```

- 추가로 궁금한 점: 나중에 언제 일치 시키도록 하고, 어떻게 같다고 알아서 추론하지? [링크](상단 opinion 링크 추가)

<br>

### 3. 여러 개의 DOM 노드를 렌더링해야 한다고, 모든 노드에서 구분이 필요한 것은 아니다. 동일 리스트에서 랜더링 되는 '형제' 사이들 끼리만!

*"컴포넌트가 `key`를 prop으로 받지 않는다는 점에 유의하세요. key는 React 자체에서 힌트로만 사용됩니다. 컴포넌트에 ID가 필요하다면 `<Profile key={id} userId={id} />`와 같이 별도의 prop으로 전달해야 합니다."*


key 구별이 필요한 범위는 동일 배열 안에서만 구분해주면 된다. 동일 데이터라고 모든 범위에서 구분 필요한게 아니라, 동일 데이터 소스더라도 다른 배열이라면 key로 구분해주지 않아도 무방하다고 한다.

key에는 배열 내 위치로 쓰기에는 ‘변할 수 있고’ == 식별 불가’ 할 수 있기 때문에 index로 key를 쓰기엔 리스크가 있다는 것이 주요한 이유다. 보다 더 ‘고유하게 식별 가능하도록’ 담겨야 하는 것이다.

### 4. 참고: spread 구문 사용 가능 + prop의 key 명시 안해줘도 되는 경우가 있음.


<br>


# React 조건부 렌더링

## context
> 조건부 렌더링 [공식 문서](https://ko.react.dev/learn/conditional-rendering)

## opinion

### 1.

### 2. 

### 3. 

## research

### 1.

### 2. 

### 3. 