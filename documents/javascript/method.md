# Method

## Array

### `reduce()`
---
#### reduce() 메소드 중간에 멈추기: `break;` 는 당연히 안됨. 
- 누적 연산하다가 중간에 참조하는 배열에 변경 일으켜서, 더 이어서 연산할 요소를 없애버리기 (샘플 코드 첨부)
- (참고) 자바스크립트 reduce() 에 break 거는 법 [링크](https://inpa.tistory.com/entry/JS-%F0%9F%9A%80-reduce-break-%ED%95%98%EB%8A%94-%EB%B2%95-How-to-early-break-reduce)

```js
const sum = [1,2,3].slice(0)
  .reduce((acc, current, i, arr) => {
    if (i === 1) { // index 1 차례에서,
      console.log(arr); // 아직 [ 1, 2, 3 ] 생존.
      arr.splice(0); // 참조되는 arr 배열이 reduce 동작 중간에 영향 받음.
      console.log(arr); // splice 때문에 arr는 [] 됨.
    }

    return acc += current; 
    // index 0, 1 까지는 arr 배열 살아있음. 이제 돌 요소 없으니 끝남.
});

console.log(sum); // 3 
```

### `slice()`: 복사
---

### `splice()`: 삭제, 교체, 추가
---
> The splice() method of Array instances changes the contents of an array **by removing or replacing** existing elements and/or **adding** new elements in place.



