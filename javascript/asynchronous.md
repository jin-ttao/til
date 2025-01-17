# asynchronous

<!-- toc -->

- [opinion](#opinion)
  * [Promise는 마치 오래 걸리는 작업의 '대변인'이자, 뒷처리 까지 도맡아주는 '행동대장' 같다.](#promise%EB%8A%94-%EB%A7%88%EC%B9%98-%EC%98%A4%EB%9E%98-%EA%B1%B8%EB%A6%AC%EB%8A%94-%EC%9E%91%EC%97%85%EC%9D%98-%EB%8C%80%EB%B3%80%EC%9D%B8%EC%9D%B4%EC%9E%90-%EB%92%B7%EC%B2%98%EB%A6%AC-%EA%B9%8C%EC%A7%80-%EB%8F%84%EB%A7%A1%EC%95%84%EC%A3%BC%EB%8A%94-%ED%96%89%EB%8F%99%EB%8C%80%EC%9E%A5-%EA%B0%99%EB%8B%A4)
  * ['비동기 메서드가 동기 메서드처럼 값을 반환할 수 있게 해준다'는데, 이것이 얼마나 막강한 역할인지 감이 안온다. 그리고 promise가 비동기 작업이 끝나고 이미 반환된 결과 원본을 변경하는 동작은 참조값 개념으로 가능하게 하는 건가?](#%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%A9%94%EC%84%9C%EB%93%9C%EA%B0%80-%EB%8F%99%EA%B8%B0-%EB%A9%94%EC%84%9C%EB%93%9C%EC%B2%98%EB%9F%BC-%EA%B0%92%EC%9D%84-%EB%B0%98%ED%99%98%ED%95%A0-%EC%88%98-%EC%9E%88%EA%B2%8C-%ED%95%B4%EC%A4%80%EB%8B%A4%EB%8A%94%EB%8D%B0-%EC%9D%B4%EA%B2%83%EC%9D%B4-%EC%96%BC%EB%A7%88%EB%82%98-%EB%A7%89%EA%B0%95%ED%95%9C-%EC%97%AD%ED%95%A0%EC%9D%B8%EC%A7%80-%EA%B0%90%EC%9D%B4-%EC%95%88%EC%98%A8%EB%8B%A4-%EA%B7%B8%EB%A6%AC%EA%B3%A0-promise%EA%B0%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%9E%91%EC%97%85%EC%9D%B4-%EB%81%9D%EB%82%98%EA%B3%A0-%EC%9D%B4%EB%AF%B8-%EB%B0%98%ED%99%98%EB%90%9C-%EA%B2%B0%EA%B3%BC-%EC%9B%90%EB%B3%B8%EC%9D%84-%EB%B3%80%EA%B2%BD%ED%95%98%EB%8A%94-%EB%8F%99%EC%9E%91%EC%9D%80-%EC%B0%B8%EC%A1%B0%EA%B0%92-%EA%B0%9C%EB%85%90%EC%9C%BC%EB%A1%9C-%EA%B0%80%EB%8A%A5%ED%95%98%EA%B2%8C-%ED%95%98%EB%8A%94-%EA%B1%B4%EA%B0%80)
- [research](#research)
  * [Promise](#promise)
    + [Promise도 객체. 성공이든 실패든 오래 걸리는 비동기 작업의 결과를 갖고 있는데, Promise는 '오래 걸리는 작업'과 '이어서 할 작업'의 연결다리로써 의미가 있다.](#promise%EB%8F%84-%EA%B0%9D%EC%B2%B4-%EC%84%B1%EA%B3%B5%EC%9D%B4%EB%93%A0-%EC%8B%A4%ED%8C%A8%EB%93%A0-%EC%98%A4%EB%9E%98-%EA%B1%B8%EB%A6%AC%EB%8A%94-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%9E%91%EC%97%85%EC%9D%98-%EA%B2%B0%EA%B3%BC%EB%A5%BC-%EA%B0%96%EA%B3%A0-%EC%9E%88%EB%8A%94%EB%8D%B0-promise%EB%8A%94-%EC%98%A4%EB%9E%98-%EA%B1%B8%EB%A6%AC%EB%8A%94-%EC%9E%91%EC%97%85%EA%B3%BC-%EC%9D%B4%EC%96%B4%EC%84%9C-%ED%95%A0-%EC%9E%91%EC%97%85%EC%9D%98-%EC%97%B0%EA%B2%B0%EB%8B%A4%EB%A6%AC%EB%A1%9C%EC%8D%A8-%EC%9D%98%EB%AF%B8%EA%B0%80-%EC%9E%88%EB%8B%A4)
  * [promise.all()](#promiseall)
    + [promise.all()도 promise 메서드 중 하나. 단 하나의 promise 객체를 반환하는데, `fullfill`일 수도 `reject`일수도.](#promiseall%EB%8F%84-promise-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A4%91-%ED%95%98%EB%82%98-%EB%8B%A8-%ED%95%98%EB%82%98%EC%9D%98-promise-%EA%B0%9D%EC%B2%B4%EB%A5%BC-%EB%B0%98%ED%99%98%ED%95%98%EB%8A%94%EB%8D%B0-fullfill%EC%9D%BC-%EC%88%98%EB%8F%84-reject%EC%9D%BC%EC%88%98%EB%8F%84)
  * [비동기 코드의 실행 흐름을 예측하자](#%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%BD%94%EB%93%9C%EC%9D%98-%EC%8B%A4%ED%96%89-%ED%9D%90%EB%A6%84%EC%9D%84-%EC%98%88%EC%B8%A1%ED%95%98%EC%9E%90)
    + [promise.all()](#promiseall-1)

<!-- tocstop -->

## opinion

### Promise는 마치 오래 걸리는 작업의 '대변인'이자, 뒷처리 까지 도맡아주는 '행동대장' 같다.

### '비동기 메서드가 동기 메서드처럼 값을 반환할 수 있게 해준다'는데, 이것이 얼마나 막강한 역할인지 감이 안온다. 그리고 promise가 비동기 작업이 끝나고 이미 반환된 결과 원본을 변경하는 동작은 참조값 개념으로 가능하게 하는 건가?

## research

### Promise

> The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value. <br> (...) <br> A Promise is a proxy for a value not necessarily known when the promise is created. <br> It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. <br> This lets asynchronous methods **return values** like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future. <br> [공식문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

#### Promise도 객체. 성공이든 실패든 오래 걸리는 비동기 작업의 결과를 갖고 있는데, Promise는 '오래 걸리는 작업'과 '이어서 할 작업'의 연결다리로써 의미가 있다.

- 생성 시점에는 아직 결과를 모를 수 있다. (proxy?: 오래 걸릴 작업의 '대변인' 정도라고 생각하자)
- 이 객체로, 비동기 작업이 성공했을 때의 결과값이나 실패했을 때의 이유 or 관련 처리 방법을 연결할 수 있다.
  - => 오래 걸리는 작업 뒤에 뭘 할지 정의할 수 있게 도와준다는 뜻. (위에서 'associate handlers' 부분)
- 비동기 메서드인데도, 다른 동기 메서드들처럼 '값'을 반환할 수 있게 해준다는 것을 당연하게 생각하면 안됨.
  - 최종 결과값을 즉시 반환하는 대신, 나중에 미래의 언젠가 '그 값 제공할게' 하는 약속을 반환하는 것.
  - 이렇게 하면, 코드 가독성👍, 비동기 작업 흐름 제어도 쉽게👍.
- 예컨대, 서버에서 데이터 가져오는 작업을 Promise로 구현하면?

  - '데이터 언제 도착할지 모르지만', 그 데이터를 어떻게 처리할지 미리 정의 가능!😎 (마치 방에 전등이 나가서 주문했는데, 전등이 언젠가 도착했을 때 그 뒤의 작업을 모두 예약 걸어둘 수 있는 것. 전등 끼워서, 전등 키고, 밥도 먹고 하는 등...)

- 공식문서 예제

```js
const promise1 = Promise.resolve(3);
promise1.then((val) => console.log(val)); // 3
```

### promise.all()

> The Promise.all() static method takes an iterable of promises as input and returns a single Promise. <br> This returned promise fulfills when all of the input's promises fulfill (including when an empty iterable is passed), with an array of the fulfillment values. <br> It rejects when any of the input's promises rejects, with this first rejection reason. <br> [공식문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

#### promise.all()도 promise 메서드 중 하나. 단 하나의 promise 객체를 반환하는데, `fullfill`일 수도 `reject`일수도.

- `input`: iterable한 promises, 보통 promise 배열.
- `return`: a single Promise.
  - `fulfill`: input의 모든 promise들이 fulfill 될때 반환되는 promise가 fullfill 됨.
  - `reject`: input의 promise 중 하나라도 reject 되면 reject 됨.
- 공식문서 예제

```js
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "foo");
});

Promise.all([promise1, promise2, promise3]).then((values) => {
  console.log(values);
});
// Expected output: Array [3, 42, "foo"]
```

### 비동기 코드의 실행 흐름을 예측하자

#### promise.all()

- 퀴즈를 받았다. 아래 코드에서 console.log가 어떤 순서로 출력될까? 나는 `1 > 2 > 3 > 2`를 예상했고, 틀렸다.

```js
async function foo() {
  const p1 = new Promise((resolve) => setTimeout(() => resolve("1"), 1000));
  const p2 = new Promise((_, reject) => setTimeout(() => reject("2"), 500));

  console.log(1);

  const result = await Promise.all([await p1, await p2]);

  console.log(3);

  return result;
}

foo()
  .then((res) => console.log(res, "resolve"))
  .catch((res) => console.log(res, "error"));

console.log(2);
```

- 정답은 `1 > 2 > 2 > error`인데, 왜 이게 정답인지가 더 중요하다.
- 어떻게 된걸까? 비동기 함수 foo가 호출되면,,, #다시보기
  - `await p1`은 1000ms 기다리고, 그 사이에 `p2` reject되지만 아직 처리되지 않는다.
  - `p1`이 resolve된 후, `await p2`가 실행되고 즉시 reject!
  - 이 `p2` 때문에 `Promise.all`이 reject되어서 `console.log(3)`은 실행되지 않는다.
  - 결국 `foo` 함수는 reject된 프로미스를 반환한다.
  - 그 뒤에 `console.log(2)`가 실행된다고 하는데, 왜일까?
  - 마지막에 `foo().then(...).catch(...)`의 catch 블록이 실행되어 `"2" "error"`가 출력된다고 한다.
