# Algorithm checkout

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

#### 생성자 함수는 `return`이 없으면 새로 생성된 객체가 반환됨.
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
