# 매개변수

<!-- toc -->

<!-- tocstop -->

feat. 원시값 & 참조값

```js
function foo(param) {
  console.log(param); // { a: 1, b: 2 }
  param.a = 10; // 외부 스코프 obj 프로퍼티에 영향 있음
  param = null; // 내부에는 영향 있으나, 외부 obj 프로퍼티에 영향 없음
  console.log(param); // null
  param.b = 100; // null로 선언된 데이터에 프로퍼티 세팅 불가
}

const obj = {
  a: 1,
  b: 2,
};
```
