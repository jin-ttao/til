# Algorithm checkout

## 374. Guess Number Higher or Lower

- 이진탐색에서 ceil 하는게 좋을까 floor 하는게 좋을까? 마지막 시점에서 판가름 될 것. 작은 단위에 가까워질수록 정교하게 처리해야 함.
- input이 적은 규모일 때 예외처리에서 애먹음.

- 이진탐색이 늘 효율적인 방법은 아닐 것. 숫자가 커질 때 효율적으로 검사하고자 하는 것인데, 적은 숫자일 때는 예외처리가 복잡해지지 않을까?
- 경계 조건 정의, 포인터를 활용하는 면에서 부족한 점이 있다.
    - 알고 보니, 이진탐색 구현에 표준이 있었다.
        - 내 방식처럼 start와 end에 middle를 재할당하는 방식이 아니라 middle + 1 혹은 -1 하는 탐색범위를 확실히 줄이면서, 더 안정적이고 예측이 쉽다.
        - start = middle 방식이 직관적이긴 했지만, 실제로 테스트하다보니 여러 문제가 있었다. (대표적으로 무한루프)
        - 속도 측면에서도 이점이 있을 것이라 생각했는데, 이 생각도 사실 검증된 것이 아니며 속도 보다 중요한 것이 '안정성'이라는 점을 다시 생각해보게 되었다.
    - 참고 https://www.geeksforgeeks.org/binary-search/
- middle이 `Math.floor()`를 통해서만 업데이트 해주었는데 1개의 정수만 반복되면 무한루프로 빠지는 문제가 있었음.
    - 해결방법: middle 분기처리를 통해 이전 값과 동일한 값이 할당될 것으로 보인다면 +1 해주는 방식으로 해결.
- 문제를 풀고 다른 풀이들을 보니 middle 뿐 아니라 start, end 값도 잘 활용했음.
    - 나는 middle을 할당해주는 방식으로 했는데, 이진탐색이라기 보다 범위를 조금씩 좁히는 방식을 채택함.
    - 예: start += 1, end -= 1 처럼 조금씩 좁혀가는 방식 => 효율이 여전히 높을까?
- '증명 보다 중요한 실제 테스트'를 강조하는 글을 보고.
    > 이제 바이너리 검색에 버그가 없다는 것을 알았죠? 글쎄요, 저희는 그렇게 의심하지만 확실하지는 않습니다. 프로그램이 정확하다는 것을 증명하는 것만으로는 충분하지 않으며 테스트도 해야 합니다. 게다가 프로그램이 올바른지 정말 확신하려면 가능한 모든 입력 값에 대해 테스트해야 하지만 이는 거의 불가능합니다. 동시 프로그램의 경우 상황은 더욱 심각합니다. 모든 내부 상태를 테스트해야 하는데, 이는 현실적으로 불가능합니다. 이진 검색 버그는 병합과 다른 분할 및 정복 알고리즘에도 동일하게 적용됩니다. 이러한 알고리즘 중 하나를 구현하는 코드가 있다면 버그가 터지기 전에 지금 바로 수정하세요. 이 버그에서 얻은 일반적인 교훈은 겸손입니다: 아주 작은 코드 조각도 제대로 작성하기 어렵고, 우리 세상은 크고 복잡한 코드 조각으로 운영된다는 사실입니다. [출처 research.google](https://research.google/blog/extra-extra-read-all-about-it-nearly-all-binary-searches-and-mergesorts-are-broken/)

```js
/**
 * Forward declaration of guess API.
 * @param {number} num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * var guess = function(num) {}
 */

/**
 * @param {number} n
 * @return {number}
 */
const guessNumber = function(n) {
if (n <= 3) {
  for (let i = 1; i <= n; i++) {
    if (guess(i) === 0) {
      return i;
    }
  }
}

let answer = 0;
let start = 1;
let end = n;
let middle = Math.floor((start + end) / 2);

while (answer === 0) {
  if (middle === Math.floor((start + end) / 2)) {
    middle += 1;
  } else {
    middle = Math.floor((start + end) / 2);
  }

  if (guess(middle) === 0) {
    return answer = middle;
  } else if (guess(middle) === 1) {
    start = middle;
  } else if (guess(middle) === -1) {
    end = middle;
  }
}
};
```

## 283. Move Zeroes

```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
const moveZeroes = function(nums) {
  const length = nums.length;
  let countRemove = 0;

  for (let i = 0; i < length; i++) {
    if (nums[i - countRemove] === 0) {
      nums.splice(i - countRemove, 1);
      nums.push(0);
      countRemove += 1;
    }
  }

  return nums;
};
```

### 문제 정의
- input: 정수를 요소로 갖는 배열 nums
- output: nums 원본을 변형하여 값이 0인 요소를 맨 뒤로 옮긴 원본을 반환.

### 접근
- '복사본이 아니라 배열의 원본을 변형하여 반환하도록' 하는 조건을 요구사항 및 힌트로 보고 splice() 메소드를 떠올렸다.
- 특정 요소 삽입에 splice로 삽입을 그대로 사용할 수 있지만, 이 문제는 맨 뒤에 추가하는 것이 요구사항이다. 따라서 splice 보다는 push가 맨 뒤에 특정 요소를 추가한다는 의도와 맥락을 담을 수 있으니 push를 사용하자.

어려웠던 점
#### (고민) 반복문 안에서 배열의 요소를 추가, 삭제하는 작업을 하다보니 꼬여버렸다.
- 의도대로 특정 요소를 정확히 선택하지 못 했다. 외부 값을 변형시키지 않는 함수의 순수성이 중요하다고 리액트에서 배웠는데, 요 대목이 떠올랐다. 값을 변형시켜서 꼬일 수 있는 상황을 최소화 하고 다시 시도해보자.
- 결국 먼저 0이 나온 경우 해당 0을 제거하기 때문에 뒤에 있던 요소들의 index가 -1 씩 발생해서, 반복문으로 0인지 확인하는 대상의 요소가 밀리는 이슈가 발생했다.
- 그래서 index 변동이 몇번 발생하는지, 즉 앞에 있던 요소들이 얼마나 제거되는지 기억하는 변수를 선언해서 0인지 확인하는 요소와 제거하는 index에 반영해서 밀림을 방지했다.
#### (고민) 원본을 반환하라는 조건을 지키면서 해결할 수 있는 더 좋은 방법이 있을까?
- 답안 풀이들을 보니, 0이 아닌 숫자들을 앞으로 이동하게끔 위치를 교체해주는 접근도 있었다. 0인 요소를 제어하는 접근이 아니라, 반대로 0이 아닌 요소를 움직이는 것도 가능했는데 미처 생각하지 못 했다. 다음에는 이런 류의 문제가 보인다면, 직접적으로 제어해야할 요소 외에 나머지 요소를 제어함으로써 문제를 해결할 수 있는지도 점검하는 것도 시도해보자.


## 217. Contains Duplicate

```js
 * @param {number[]} nums
 * @return {boolean}
 */
const containsDuplicate = function(nums) {
    const length = nums.length;
    const size = new Set(nums).size;

    return length !== size;
};
```

### 문제 정의
- input: 정수를 포함한 배열 nums
- output: 배열 안에 중복 요소가 1개라도 있으면 true, 아니라면 false (boolean)

### 접근
- 요소의 개수를 세는 방법도 있겠지만, 최대한 복잡도가 낮은 방법이 뭘까?
- (결정) JS에서 중복 제거를 위해 자주 사용하는 Set 객체를 활용하고, length와 size를 비교해보자.

### 왜 Set 객체를 사용하는 것이 복잡도가 낮은 방법일까?
- 정확히 하자면, 순회하는 과정이 빠를 수 있는 것.
- Set 객체의 특성을 이해하는 데에 'hash table'가 굉장히 중요한 개념.
- Set 객체는 내부적으로 hash table를 사용하는 자료구조임. 이에 따른 trade-off도 발생.
    - 때문에 속도가 array 보다 빠름.
    - hash table를 유지하기 위해 추가적인 정보를 유지해야 할 수 있어서 큰 데이터 집합에서는 array 대비 메모리 사용량 차이가 날 수 있음. (공간 복잡도)

### 그럼 왜 hash table로 구성하면 빠를까? => 해시 함수 덕분.
- 해시 함수 덕분. hash table도 결국 해시 함수로 변환한 값을 index로 해서 key, value를 저장하는 자료 구조.
- 특정 index가 있기 때문에 속도에 장점이 있음. (속도에서 index는 뗄 수 없는 관계인 것 같다. 켄님이 DB 쿼리시 index를 중요하게 활용하라 하셨는데 비슷한 맥락이라고 생각된다)
- "hash meaning" 해시 포테이토가 나옴. 이전 까지는 모호하게 "암호화된 것"이라고 생각했는데, 이건 '해시'라는 기술이 사용된 영역을 보고 내가 해석한 결과였다.
- 오히려 해시는 해시 포테이토 의미 처럼 "작게 다진다"의 의미에 가깝다. 작게 다지는 것을 연상해야 해시 알고리즘의 동작을 연상하기 쉽겠다.

### 그럼 단순하고 작은 데이터에서는 배열을 사용하는 것이 더 나은 선택일 수 있겠다. 늘 Set, Map 같은 hash table 기반 객체가 정답은 아닐 것.
- 함께 비교되는 대상으로 map 객체도 있는데, 애플리케이션에 어떤 자료구조를 쓸지 의사결정을 할 수 있어야 한다고 함. 당연히 trade-off가 있을 수 있으니 근거가 분명해야 함.

참고 https://medium.com/@dm_md/unveiling-the-speed-of-javascript-collections-set-vs-map-vs-array-vs-object-3f6e44f24505

<br>

## 2619. Array Prototype Last

```js
 * @param {number[]} nums
 * @return {number}
 */
const majorityElement = function(nums) {
  const count = {};
  let maxNum = 0;
  let maxCount = 0;

  for (let i = 0; i < nums.length; i++) {
      const key = nums[i].toString();

      if (!count[key]) {
          count[key] = 1;
      } else {
          count[key] += 1;
      }
  }

  for (const c in count) {
      if (maxCount <= count[c]) {
          maxCount = count[c];
          maxNum = c;
      }
  }

  return Number(maxNum);
};
```
### 고민 - 배열을 순회하면서 각 요소가 포함된 개수를 반드시 세어야 하는가? 모두 순회하지 않고 세는 방법은 없을까? 그나저나 순회하는 것이 늘 좋지 않은 방법이라 볼 수 있는가?
- 순회 자체가 나쁜 것이 아니라, 불필요한 순회나 중복 순회가 문제일 수 있는 것 같다.
- 대부분의 알고리즘은 최소 한 번 이상의 순회는 필요했던 것 같기도 하니.

### 접근 - 우선 문제를 푸는 것이 효율적으로 푸는 것 보다 우선임. 의사코드 기록.
- 빈 객체를 선언하고 배열 nums를 순회하면서 각 요소를 객체의 key로 하고, 요소의 개수를 value로 한다.
- 그리고 max value를 갖는 key를 반환하면 됨. 객체를 순회하면서 모두 비교하는 방법.
- 현재 값 보다 큰 값이 나오면 해당 key로 갱신을 반복. 동점이 나와도 무방함.

작동하는 코드 만들고, 개선하는게 답이니.

### 궁극적으로 결과를 도출해야 하는 건 ‘가장 많이 등장하는 요소’를 찾는 것. 개수가 반드시 과반이라는 조건도 나왔는데 힌트일 수 있음.

### 풀고 해설지를 보니 "Boyer-Moore 알고리즘"이라는 것이 있었다. 이게 위 고민들과 연관성이 있었다.
- 개수를 정확히 세지 않고도 과반수 원소를 찾을 수 있도록 하는 알고리즘인데, "개수가 반드시 과반이라는 조건" 덕분에 가능하다고 한다.
- 이렇게 기존에 검증된 알고리즘에 대한 지식을 갖는 것도 개발이나 알고리즘 풀 때 도움이 될 것.

<br>

## 2619. Array Prototype Last

```js
/**
 * @return {null|boolean|number|string|Array|Object}
 */
Array.prototype.last = function() {
    return this[this.length - 1] === undefined ? -1 : this[this.length - 1];
};

/**
 * const arr = [1, 2, 3];
 * arr.last(); // 3
 */
```

#### 문제 복기
- 배열 안의 원시값만 있다면 마지막 요소를 return하면 끝나는데, 테스트 케이스의 `{}`도 동일하게 리턴할 수 있을지 의문.
    - 확인해보니, 그대로 `{}` return 됨. 문제 푸는 핵심과는 연관성 적었음.
- this 키워드가 필요한지 hint를 보고 알았음. (this 리마인드 위해 실험해봄)
    - 여느 알고리즘 문제 처럼 매개변수가 있는 형태가 아니기 때문에, 평소 푸는 방식과 다른 접근이 필요했을 것.
- this 실험해본 것

```js
const obj = {
  a: 1,
  b: function 함수() {
    console.log("함수");
    console.log(this.a); // 1
    this.a = "this로 새로운 값";
    return this.a;
  },
};

console.log(obj.b); // '함수'라는 함수 출력
console.log(obj.b()); // "this로 새로운 값"
console.log(obj.a); // "this로 새로운 값"

```

#### `this` mdn
- 코드가 실행되어야 할 컨텍스트를 의미함(가르킴 refers to). => 다른 객체에서도 재사용할 수 있게 함. prototype 개념과도 연결.
    - 첫 문장: The this keyword refers to the context where a piece of code, such as a function's body, is supposed to run. Most typically, it is used in object methods, where this refers to the object that the method is attached to, thus allowing the same method to be reused on different objects.
- reference in programming(wikipedia): In computer programming, a reference is a value that enables a program to indirectly access a particular datum, such as a variable's value or a record, in the computer's memory or in some other storage device.

- this 가 무엇을 가르키는지 판별할 수 있어야 함
- 결구 'this'가 뭐냐? => “나”라는 단어와 비슷함.
- 똑같은 this임에도 this에 담긴 값이 다름.
    - this를 사용하는 해당 함수를 어떻게 실행하느냐에 따라 this의 값은 바뀜. (log(), obj.log() 내 this는 다름)
- this는 항상 객체임. 왜인지도 궁금하지만, 이것의 의미만 먼저 기억하자. => this.name 처럼 되어야 프로퍼티에 접근할 수 있긴 하겠다.
- 참고 [바닐라코딩 this](https://www.youtube.com/watch?v=ayyuU0xdbIU)

<br>

## 2724. Sort By
```js
 * @param {Array} arr
 * @param {Function} fn
 * @return {Array}
 */
const sortBy = function(arr, fn) {
    return arr.sort((a, b) => fn(a) - fn(b));
};
```

### sort 메소드에 대해 알 수 있었던 문제 (mdn 한 번 더 체크)
gt
#### 왜 sort()는 sort된 원본 배열의 참조를 return하는가?: (새로 알게된 사실) in-place algorithm이라는 알고리즘을 사용하기 때문.
- 컴퓨터과학에서 in-place algorithm는 알고리즘이 입력 자체를 변환하는 것으로, 새롭게 공간을 할당하지 않음. 즉 원본을 직접 조작하는 방식임.
- mdn 원문: The reference to the original array, now sorted. Note that the array is sorted in place, and no copy is made.
- 참고) 원본 영향 없이 sort 하는 방법은 몇가지 있는데, spread 연산자와 함께 sort()를 사용하거나 Array.prototype.toSorted()를 고려하는 방법도 있다.
    - 전자는 원본을 복사해서 새로운 배열을 참조해서 sort 하는 것. 후자는 원본 자체를 참조해도 원본 영향 없이 정렬된 복사본이 반환되도록 하는 것.

#### 참고) Sort stability (2019년 이후 부터). 몰랐는데 이렇게 예상치 못한 결과를 주의하는 관점 중요하겠다.
- 이전에는 동점이 발생하면, sort()가 원본의 정렬 순서를 보장해주지 못하고 동점 요소간의 순서가 바뀌는 경우도 있었다고 한다.
- version 10 (or ECMAScript 2019) 부터는 동점이 발생하면, 정렬 이전의 순서를 보장해준다고 한다.
- mdn 원문: It's important to note that students that have the same grade (for example, Alex and Devlin), will remain in the same order as before calling the sort. This is what a stable sorting algorithm guarantees.

#### 다중 조건으로 정렬도 가능하다. 최근 DB에서 정렬 기능 구현하면서, 데이터 쿼리할 때 사용했었는데 이런 원리와 유사한 맥락으로 보인다.
- data.sort((a, b) => a.가격 - b.가격 || a.이름.localeCompare(b.이름));
    - 위 가격 낮은 순 정렬후, 가격 같으면 이름순 정렬하는 로직

#### sort 내부 동작도 알아두면 좋으니 나중에 체크하기
- 특히 흥미롭게 생각하는 부분은 "브라우저별 sort 함수의 구현체가 다르지만 ECMAScript 명세를 지킨다."의 내용.
- 참고) https://1ilsang.dev/posts/array-prototype-sort

#### sort의 매개변수로 들어오는 compareFn은 2개의 인자를 받으며 호출된다. 둘 다 비교대상이 됨.
```
e.g.
const items = [
  { name: "갑", value: 21 },
  { name: "을", value: -37 },
];
items.sort((a, b) => a.value - b.value);
// [
//   { name: '을', value: -37 },
//   { name: '갑', value: 21 },
// ]
```

<br>

## 844. Backspace String Compare
```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
const backspaceCompare = function(s, t) {
    const getStrRemained = function(str) {
        const stack = [];

        for (const char of str) {
            if (char === "#") {
                if (stack.length > 0) {
                    stack.pop();
                }
            } else {
                stack.push(char);
            }
        }

        return stack.join("");
    };

    return getStrRemained(s) === getStrRemained(t);
};
```
### 풀이 복기
#### stack 더 익숙해지기
#### "같다"를 문제 맥락에 맞추어서 재정의 하고 생각해보기
- 두 string이 같은지 여부를 반환하는 문제.
- 이 문제에서는 "같다" 표현을 "# 기준으로 char 제거하고, 동일 index에 동일 char가 있다"로 표현을 바꿀 수 있음.
- 이 접근이 효과가 없는 문제도 있겠지만, 이 문제에서는 덕분에 'index를 찾아내자'는 좋은 시작점을 찾을 수 있었음.
- 문제에 주어진 워딩이나 고유명사를 그대로 생각하기 보다, 맥락에 맞추어서 변환해서 생각이 필요할 수도 있음.
#### 테스트 케이스 중 가장 쉽고 단순한 것 부터 맞출 것. 하나씩 수정ㄱㄱ.
- 테스트 케이스가 총 3가지였는데, 한 번에 모든 케이스를 맞추려고 함.
#### 메소드 의존도 줄일 것. 조건문과 반복문 만으로 알고리즘 문제 풀기에 충분함.
- string에서 특정 index를 제거하고 남은 결과를 반환해야 해서, array의 splice() 역할을 하는 string 메소드가 있는지 찾아봄.
- 공식 문서에서 찾지 못 했는데, 문득 메소드에 의존하고 있다는 느낌을 받아서 직접 구현해야겠다고 생각함.
- string을 초기화 하고, 특정 조건에서만 해당 string에 addition assignment 연산자(`+=`)를 적용하는 방법으로 구현함.
#### `indexOf()`의 optional parameter인 start position을 잘 사용하면, 불필요한 중첩 반복을 피할 수 있음.
- string 메소드 `indexOf()`는 searchString이 여러 개 있어도 그 중 첫 index를 반환한다는 점 유의.


### JavaScript `Iterators`, `next()`

#### 알고리즘 푸는 중 공식 문서를 참고하면서 JavaScript 내부 사정을 들여다보는 기회가 많다. (단, 시간 정해두고 보기)
- 몰랐던 개념들을 자주 발견하게 되어서 흥미로운데, 개인 프로젝트를 하다보면 구현속도에 집중해서 깊게 보지 못하고 넘어가는 개념이 많았던 아쉬움이 조금 해소된다. 이 시간을 활용해서 당연하게 생각했던 코드, 동작 하나 하나 의미를 생각해보도록 하자. 아래는 그 내용들을 정리한 것.
- '배열을 돈다'는 표현으로 의사코드를 쓰다가 '순회한다'는 표현으로 고쳤다. 문득 '순회한다'는 표현이 정확한지 의문이 들어서 검색함. 배열을 순회한다는 표현은 적절했고, 영어로는 `iterate`라는 것을 재확인했다.
- 연관 [MDN 자료 - Iterators and generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_generators)에서 `iterators` 개념이 보였는데 정확히 알지 못해서 잠깐 들여다봤다.
    > Iterators and Generators **bring the concept of iteration** directly into the core language and provide a mechanism **for customizing the behavior of for...of loops**.
    - 자바스크립트에서 '반복'이라는 작업이 동작할 수 있도록 하고, for 루프를 커스텀할 수 있는 것도 이 `Iterators`와 `Generators` 덕분이라는 것. 조건문과 반복문은 모든 프로그래밍 언어에서 처음 부터 당연히 되는 것이라 생각했는데, 이 또한 뒤에서 움직여주는 것이 있었다.

#### 흥미가 생겨서 더 살펴보니, 위 역할을 해주는 `iterators`도 객체였다.🫨 (객체는 모든 곳에 존재함...)
- 또 `iterators`가 반복문을 구현할 수 있는 근원은 Iterator protocol 하에서 동작하는 `next()`라는 또다른 메소드 덕분이었다. ([참고 MDN - Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol))
    > **In JavaScript an iterator is an object** which defines a sequence and potentially a return value upon its termination.  <br> Specifically, an iterator is any object which implements the Iterator protocol by having a **next() method** that returns an object with two properties:
- `Generator` 인스턴스의 메소드인 `next()`도 함수인지라 input, output이 명확하다. 파라미터(input)으로 `value`(어떤 특정 값)을 받으며, 결과로 다음 2가지 프로퍼티를 갖는 객체를 return(output)한다. 먼저 `done`(해당 값이 처리가 완료되었는지), `value`(해당 값이 처리된 값은 무엇인지)이다.

<br>

## 35. Search Insert Position
> 1차 풀이: 총 1시간 10분 소요
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
const searchInsert = function(nums, target) {
    const indexOfTarget = nums.indexOf(target);

    if (indexOfTarget >= 0) {
        return indexOfTarget;
    }

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > target) {
            return 0;
        } else {
             if (i === nums.length - 1) {
                return nums.length;
            }

            if (nums[i] < target && nums[i + 1] > target) {
                return i + 1;
            }
        }
    }
};
```
#### 시간 복잡도 O(log n)를 맞추는게 조건인데 어떻게 할 수 있을지 고민.
=> 다 풀고 찾아보니 O(log n)는 '문제 해결에 필요한 단계들이 연산 마다 특정 요인에 의해 줄어든다'는 의미라 이진탐색 처럼 조건을 좁혀나가야 한다고 한다.
=> 다음에는 이진탐색으로 풀어보기**
#### 문제의 핵심 정의, 어떤 자료구조를 활용할지 정하고 방향 고민해도 좋겠음.
#### 첫 시도: 이진 탐색으로 풀어보자. 냅다 중앙값을 정의하려 했는데, 생각해보니 이진탐색의 핵심은 중앙값이라기 보다 단지 중앙값을 '비교할 기준값'으로 활용하는 접근.
- 테스트 케이스에서 충족하지 못하는 케이스 발견해서 다른 접근법 고민. => 테스트 케이스의 중요성! 테스트 케이스가 곧 해결해야할 문제이고 요구사항임.
- 다른 사람 풀이를 보니 이진탐색도 가능한 방법이었음. 내가 지금 이진탐색을 잘 모르는 듯.
#### 두번째 시도: 배열 요소 처음 부터 순회하면서 반복
#### (모순적이게도) 반복은 종료를 위해 하는 것. 목표가 있기 때문에 무언가 반복하는 것이고, 목표가 무엇인지 정의하는 건 당연히 중요.
#### 반복문, 조건문으로 뭘 할지 바로 떠오르지 않았음. 문제에서 잠시 떨어져서 생각해봤다. '반복문은 뭐고 언제 쓰지', '조건은 왜 필요하지'.
- 이렇게 원론적으로 생각하니 명확해졌다. 말 그대로 '반복 하려고', '시작, 끝 등 조건을 규정하려고' 각각을 사용하는 것.
- 이걸 내가 해결하려는 상황, 의도에 대입해서 생각했다.
- 사고 프레임 찾아보고 안풀리면 여쭤보기: while 조건문에 들어가는 것, 블록 안에 넣을 것.
#### 오래 걸린 것: while 조건문 안에 뭘 넣어야 할까, 정렬 기준대로 알맞는 자리에 위치 시키는 방법
=> 즉 언제까지 반복할 것인지 정의. 뭘 반복할지는 비교적 쉬웠는데 반복 조건을 정하지 않은 상태에서 반복 작업을 제대로 정의할 수 있을까.
=> 정렬 알고리즘을 여러개 고민했었는데, bubble sort, Insertion sort, merge sort 등.
#### 알고리즘 흐름이 순서가 명확해야 하고, 정답 까지 최대한 좁혀나가는 사고로 접근해야 함.

<br>

## 104. Maximum Depth of Binary Tree
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
const maxDepth = function(root) {
    if (root == null)  {
        return 0;
    }

    let leftDepth = maxDepth(root.left);
    let rightDepth = maxDepth(root.right);

    return Math.max(leftDepth, rightDepth) + 1;
};
```

### param이 `TreeNode`는 어떤 경우인가. TreeNode가 함수로 선언되었음. 리턴이 없어서 반환값이 없지 않은지 점검.

#### 생성자 함수는 `return`이 없으면 새로 생성된 객체가 반환됨. 이 케이스는 설명을 추가로 보아서 알았지만, 다른 케이스에서 어떻게 생성자 함수인지 알 수 있을까?
> If the constructor function returns a non-primitive, this return value becomes the result of the whole new expression. Otherwise, **if the constructor function doesn't return anything or returns a primitive, newInstance is returned instead.** (Normally constructors don't return a value, but they can choose to do so to override the normal object creation process.) [MDN - new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new#description)

실험
```js
const node3 = new TreeNode(3); // 여기서 `new` 제거하면 `node3`는 undefined.
// 출력
TreeNode {
  val: 3,
  left: undefined,
  right: undefined,
  __proto__: { constructor: ƒ TreeNode() }
}
```


## Is Object Empty

```js
const isEmpty = function(obj) {
    if (Array.isArray(obj)) {
        return obj.length === 0;
    }
    return Object.keys(obj).length === 0;
};
```
#### 자바스크립트도 배열을 객체의 특별한 한 형태로 간주한다. 그래서 `Object.keys()`도 배열, 객체 둘다 적용 가능함.

```js
// 배열의 인덱스가 키가 됨.
Object.keys([1, 2, 3]) // ['0', '1', '2']
Object.keys([]) // []

// 빈 배열, 빈 객체는?
const key = Object.keys({});
const value = Object.values({});

console.log(key); // [] ( truthy )
console.log(value); // [] ( truthy )
```

#### Boolean 값을 리턴하는 경우, 연산자를 포함한 표현식으로 리턴하는 것도 가능함.
```js
const isEmpty = function(obj) {
    if (Array.isArray(obj)) {
        return obj.length === 0; // 표현식 return
    }
    return Object.keys(obj).length === 0; // 표현식 return
};
```

<br>

## something

#### 요구사항으로 주어진 정수를 직접 제어(e.g. 감소)하며 추적하는 방식으로 변경하면 더 안전할 수 있음.

#### 특정 데이터를 배열 타입으로 유지하다가 문자열로 변환하는 과정이 반복됨. 불필요한 연산일 수 있어서, 문자열을 직접 조작하는 방식으로 하면 효율성 개선할 수 있음.

#### 삼항연산자도 if 조건문 처럼 여러 조건을 소괄호 통해서 규정할 수 있음.

#### 연산할 때, 메소드 없이 `+` 연산자로 문자열을 바로 이을 수 있음
- 다른 분의 코드를 봤는데 의사코드만으로는 `splice` 메소드를 쓰셨을까 했는데, 연산자 만으로 해결하신게 인상에 남음.

#### `Array.from`으로 문자열을 배열로 변환한 점 (아직 문자열에 `Array.from`을 사용해본 적 없는데 좋은 예시로 보임)

#### 문자열 반복 생성을 위해 배열에 문자열을 `fill`로 채우지 않고, `repeat` 메소드로 문자열 반복 생성 가능

<br>

## Ransom Note
```js
var canConstruct = function(ransomNote, magazine) {
    const letterCount = {};

    for (let letter of magazine) {
        letterCount[letter] = (letterCount[letter] || 0) + 1;
    }

    for (let letter of ransomNote) {
        if (!letterCount[letter]) {
            return false;
        }

        letterCount[letter]--;
    }

    return true;
};
```
### 📜 problem
- input: 문자열1, 문자열2
- output: Boolean (문자열2의 알파벳을 최대 1번만 사용해서 문자열1을 만들 수 있는가?)

### ➕ one more thing

#### 바로 생각나지 않고 헷갈렸던 점: 객체 프로퍼티를 동적으로 생성하기 - 처음에 `obj[key] += 1` 코드로 정확하지 않는 근거로 코드를 작성함. 객체 프로퍼티에 연산할 때, 논리 연산자로 값이 있을 때와 없을 때에 따라 조건 나눠주기. `객체[key] = (객체[key] || 0) + 1;`

#### '단축 평가(short-circuiting)' 개념 짚고 넘어가기: 첫 피연산자로 결론 나면 그걸로 땡!
![short-circuiting](/src/image/short-circuiting.png)
- 단축 평가란 논리 연산의 결과가 첫 피연산자에 의해 확정될 때, 두 번째 피연산자 평가는 굳이 하지 않는 것.

#### 논리 연산자는 결국 피연산자 둘 중 하나의 값을 반환한다. 그래서 Boolean 값에 쓰일 때는 당연히 Boolean 값이 반환되는데, Boolean이 아닌 숫자, 문자열 같은 값에 쓰여도 Boolean이 아닌 결과가 반환될 수 있는 것.
> - The logical OR (||) (logical disjunction) operator for a set of operands is true if and only if one or more of its operands is true.
> - It is typically used with boolean (logical) values. When it is, it returns a Boolean value.
> - However, the || operator actually returns the value of one of the specified operands, so if this operator is used with non-Boolean values, it will return a non-Boolean value.
> [공식 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)


#### 문자열 순회할 때에도 for...of 사용 가능.

#### 아직 익숙하지 않은 것: Hash map 써서 요소의 빈도 카운트 하는 방법 익숙해지자! // 문자열A에 문자열B가 충분히 존재하는지 체크

<br>

## Two Sum
```js
const twoSum = function(nums, target) {
    const numsMap = new Map();

    for (let i = 0; i < nums.length; i++) {
        const pairWithNum = target - nums[i];

        if (numsMap.has(pairWithNum)) {
            return [numsMap.get(pairWithNum), i];
        }

        numsMap.set(nums[i], i);
    }

    return [];
};
```

### 📜 problem
- input: 정수가 담긴 배열 nums, 정수 target
- output: index들(indices)을 배열에 담아 반환 (배열nums의 원소를 더해서 target이 나오는 경우)
  - 주의: 한 원소를 2번 이상 사용 못함, 정답은 어떤 순서로 반환하든 상관 없음
  - 테스트 케이스 생각
    - 타겟이 절대 나오지 않는 경우라면? => Only one valid answer exists.
    - 음수이거나 0일 떄 다르게 처리할 게 있을까? => 단순 덧셈뺄셈 연산이라 특별히 처리할 부분은 없을 것.

### 💭 approach

#### 결정: 주어진 배열 nums를 map 객체로 변환 후, 원소 1개씩 검사하며 target과의 차이값이 내부에 존재하는지 확인한다.

### 결정 까지 생각의 흐름 기록.

#### target도 정수, 배열 nums의 원소도 정수. 정수 2개를 더해서 정수가 나오는 경우 어떻게 효율적으로 접근할 수 있을까?

#### 우선 가장 먼저 떠오르는 방법: 배열 nums의 첫 원소부터 돌면서 target과 차이를 구하고, 해당 차이가 nums의 원소로 있는지 검사해서 해당 index들을 반환하는 방법. => 최악의 경우 배열의 모든 원소를 돌아야 할 수 있으니 다른 방법도 생각해보자.

#### 배열의 특정 요소를 찾을 때, 최대한 효율적으로 할 수 있는 방법은 배열 그대로 찾지 않고 해시 테이블 자료구조를 끼고 활용하는게 나을 것이다. index를 최종 반환하려면 배열, map객체를 활용해야 할 것이고.

#### map객체가 index를 기억할 수 있고, 탐색도 빠르기 떄문에 이 map 객체 자료구조를 활용해보자.
// 여기까지 10분 소요.

### ➕ one more thing

#### 추가) Map.prototype.has(__)는 메소드 파라미터에는 value가 들어가는게 아니라 key가 들어가는거다. 주의!

#### 추가) Map 객체의 key로 '무언가의 value'를 줄 수도 있다. index만 key로써 써야 하는 건 아님. 하지만 Map 특성상 중복된 key는 있을 수 없고, 이전 key가 있으면 덮어쓸 수도 있으니 이 부분을 주의해서 써야 함.

```js
예시:
const map1 = new Map();
map1.set('1', 1);
map1.set('1', 2); // 기존 키1에 2 들어가서 여전히 map1은 1개만 갖고 있음.
```

#### 추가) 왜 해시테이블이 배열 보다 빠른지 정확한 내부동작을 말로 설명할 수 없다. 이 부분을 보완해보자.

#### 추가) 평일 알고리즘 문제는 손으로 하는데 손 없이 머리만으로 생각하는 근육도 길러야 할 것 같다. 머리가 손에만 너무 의지하지 않도록. 개인적인 추측이라, 이런게 실제로도 효과가 있을지 궁금하다.

#### 추가) Map에서 키로 값 당연히 얻을 수 있는데, 반대로 값으로 키 확인할 수 있나?: 찾아보니 메소드는 없고, 기존 메소드나 배열, 객체 등으로 변환하고 키값을 얻는 함수로 추상화, 재사용하는 경우들이 많더라.

#### 추가) 리서치 중 알게된 사실: Map도 당연히 구조분해할당이 되는데 신기하다!
```js
// 구조분해할당
const [a, b] = map;
console.log(a); // [ 0, '1' ]
// console.log(a[0]);
console.log(b); // [ 1, '2' ]
```
