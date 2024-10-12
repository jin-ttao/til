

### `var`와 `let`, `const` 각각으로 선언된 변수의 스코프: 선언 키워드, 위치에 따라 어디서 쓸 수 있을까?
```js
// #1 var
for (var i = 0; i < 5; i++) {};
console.log(i); // 5 출력

// #2 var
for (let j = 0; j < 5; j++) {
  var 변수 = 1;
};
console.log(변수); // 1 출력
console.log(j); // ReferenceError: j is not defined

// #3 var '함수 스코프' 케이스 살펴보기
function x() {
  y = '함수 안에서 키워드 없이 할당'; // strict 모드에서는 ReferenceError
  var z = 2;
}

x();
// console.log(z); // ReferenceError: z is not defined
console.log(y); // '함수 안에서 키워드 없이 선언' 값이 잘 출력됨. 왜? (아래 확인)
  // 선언되지 않은 변수들은 항상 전역변수이기 때문.
    // 예) 변수 = 1; 작성하고 console.log(변수); 해도 1 출력되긴 함 
  // 한편, 선언된 변수들은 변수 선언된 실행 콘텍스트 안에서 만들어지기 때문에 z는 출력 불가.

// #4 let
for (let k = 0; k < 10; k++) {};
// console.log(k); // ReferenceError: k is not defined

// #5 let & var
for (let i = 0; i < 8; i++) {};
console.log(i); // 5 출력.. 그런데 이 i는 어느 i일까?: 
  // #1에서 튀어나온? 바로 위 #5에서 온?: 
    // 정답 = #1에서 온 i. => #5의 i는 밖으로 나오지 못 한다. 
    // 왜? #4가 정확한 그 예시임. ⚡ let 선언 변수의 스코프는 '가장 가까운 중괄호 내부'이기 때문. (소괄호가 스코프라서가 아님 주의)


```
실험 스크린샷
![변수_var_let_scope](/src/image/변수_var_let_scope.png)

참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/var
- https://www.bangseongbeom.com/javascript-var-let.html
