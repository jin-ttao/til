# JavaScript 코드 실행 로직

## 맥락
- 어려웠던 코드 아카이빙

## 내용

### 공통 key로 2개의 객체 배열을 병합하기 - 가급적 이중 for문 피할 수 있나 (24.12.31)

```js
// 주어진 상황
const nameArr = [
  { id: 'A', name: '피스타치오 프라페' },
  { id: 'B', name: '꿀아메리카노' }
];

const countArr = [
  { id: 'A', count: 1 },
  { id: 'B', count: 2 }
];

// 원하는 결과
[
  { id: 'A', name: '피스타치오 프라페', count: 1 },
  { id: 'B', name: '꿀아메리카노', count: 2 }
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

final.forEach(el => {
  arr2.forEach(arr => {
    if (el.id === arr.id) {
      el.count = arr.count;
    }
  })
})
```

<br>

#### 주어진 배열 nameArr, countArr 있는 그대로 사용하지 않고 활용해서 새 데이터 만들기
```js
// 개선 버전 - O(n) 시간 복잡도
const countMap = new Map(countArr.map(el => [el.id, el.count]));
  // console.log(countMap.get("A")); // 1

const final = nameArr.map(el => ({
  ...el,
  count: countMap.get(el.id)
}));
```

<br>

### 공통 key로 2개의 배열을 병합하기 - 1개만 객체 배열 (24.12.31)
- 문제
  - 결국 아래 로직도 `forEach` 안의 `includes`로 인해 시간복잡도 O(n²)임.
```js
// 1차 시도
const arr = [ 'A', 'B' ];
const arrB = [
  { _id: 'A', postCount: 5 },
];

const id = arrB.map(el => el._id);

arr.forEach(el => {
  if (!id.includes(el)) {
    arrB.push({
      _id: el,
      postCount: 0,
    })
  }
})
```

#### Spread Operator도 연산자 우선순위를 따른다. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#:~:text=Spread%0A...x-,%5B13%5D,-1%3A%20comma)
```js
// 개선 버전
const existedIds = new Set(b.map(el => el._id));

const result = [
  ...b,
  ...a
    .filter(id => !existedIds.has(id))
    .map(id => ({ _id: id, postCount: 0 }))
];
```
