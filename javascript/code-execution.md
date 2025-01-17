# JavaScript 코드 실행 로직

<!-- toc -->

- [맥락](#%EB%A7%A5%EB%9D%BD)
- [내용](#%EB%82%B4%EC%9A%A9)
  * [공통 key로 2개의 객체 배열을 병합하기 - 가급적 이중 for문 피할 수 있나 (24.12.31)](#%EA%B3%B5%ED%86%B5-key%EB%A1%9C-2%EA%B0%9C%EC%9D%98-%EA%B0%9D%EC%B2%B4-%EB%B0%B0%EC%97%B4%EC%9D%84-%EB%B3%91%ED%95%A9%ED%95%98%EA%B8%B0---%EA%B0%80%EA%B8%89%EC%A0%81-%EC%9D%B4%EC%A4%91-for%EB%AC%B8-%ED%94%BC%ED%95%A0-%EC%88%98-%EC%9E%88%EB%82%98-241231)
    + [주어진 배열 2개만 활용해서 `forEach` 메소드 이중으로 구현](#%EC%A3%BC%EC%96%B4%EC%A7%84-%EB%B0%B0%EC%97%B4-2%EA%B0%9C%EB%A7%8C-%ED%99%9C%EC%9A%A9%ED%95%B4%EC%84%9C-foreach-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%9D%B4%EC%A4%91%EC%9C%BC%EB%A1%9C-%EA%B5%AC%ED%98%84)
    + [주어진 배열 nameArr, countArr 있는 그대로 사용하지 않고 활용해서 새 데이터 만들기](#%EC%A3%BC%EC%96%B4%EC%A7%84-%EB%B0%B0%EC%97%B4-namearr-countarr-%EC%9E%88%EB%8A%94-%EA%B7%B8%EB%8C%80%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EA%B3%A0-%ED%99%9C%EC%9A%A9%ED%95%B4%EC%84%9C-%EC%83%88-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%A7%8C%EB%93%A4%EA%B8%B0)
  * [공통 key로 2개의 배열을 병합하기 - 1개만 객체 배열 (24.12.31)](#%EA%B3%B5%ED%86%B5-key%EB%A1%9C-2%EA%B0%9C%EC%9D%98-%EB%B0%B0%EC%97%B4%EC%9D%84-%EB%B3%91%ED%95%A9%ED%95%98%EA%B8%B0---1%EA%B0%9C%EB%A7%8C-%EA%B0%9D%EC%B2%B4-%EB%B0%B0%EC%97%B4-241231)
    + [Spread Operator도 연산자 우선순위를 따른다. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#:~:text=Spread%0A...x-,%5B13%5D,-1%3A%20comma)](#spread-operator%EB%8F%84-%EC%97%B0%EC%82%B0%EC%9E%90-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84%EB%A5%BC-%EB%94%B0%EB%A5%B8%EB%8B%A4-mdnhttpsdevelopermozillaorgen-usdocswebjavascriptreferenceoperatorsoperator_precedence%23textspread%250ax-%255b13%255d-1%253a%2520comma)

<!-- tocstop -->

## 맥락

- 어려웠던 코드 아카이빙

## 내용

### 공통 key로 2개의 객체 배열을 병합하기 - 가급적 이중 for문 피할 수 있나 (24.12.31)

```js
// 주어진 상황
const nameArr = [
  { id: "A", name: "피스타치오 프라페" },
  { id: "B", name: "꿀아메리카노" },
];

const countArr = [
  { id: "A", count: 1 },
  { id: "B", count: 2 },
];

// 원하는 결과
[
  { id: "A", name: "피스타치오 프라페", count: 1 },
  { id: "B", name: "꿀아메리카노", count: 2 },
];
```

<br>

#### 주어진 배열 2개만 활용해서 `forEach` 메소드 이중으로 구현

- 문제
  - O(n²) 시간 복잡도를 갖고 배열이 커질 수록 성능이 안좋을 수 있음.
  - 이중 반복으로 가독성이 좋지 않다고 느낄 수 있음. (의도 파악이 어려움)

```js
// 1차 시도
const final = [...arr1];

final.forEach((el) => {
  arr2.forEach((arr) => {
    if (el.id === arr.id) {
      el.count = arr.count;
    }
  });
});
```

<br>

#### 주어진 배열 nameArr, countArr 있는 그대로 사용하지 않고 활용해서 새 데이터 만들기

```js
// 개선 버전 - O(n) 시간 복잡도
const countMap = new Map(countArr.map((el) => [el.id, el.count]));
// console.log(countMap.get("A")); // 1

const final = nameArr.map((el) => ({
  ...el,
  count: countMap.get(el.id),
}));
```

<br>

### 공통 key로 2개의 배열을 병합하기 - 1개만 객체 배열 (24.12.31)

- 문제
  - 결국 아래 로직도 `forEach` 안의 `includes`로 인해 시간복잡도 O(n²)임.

```js
// 1차 시도
const arr = ["A", "B"];
const arrB = [{ _id: "A", postCount: 5 }];

const id = arrB.map((el) => el._id);

arr.forEach((el) => {
  if (!id.includes(el)) {
    arrB.push({
      _id: el,
      postCount: 0,
    });
  }
});
```

#### Spread Operator도 연산자 우선순위를 따른다. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#:~:text=Spread%0A...x-,%5B13%5D,-1%3A%20comma)

```js
// 개선 버전
const existedIds = new Set(b.map((el) => el._id));

const result = [
  ...b,
  ...a.filter((id) => !existedIds.has(id)).map((id) => ({ _id: id, postCount: 0 })),
];
```
