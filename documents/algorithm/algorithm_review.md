# Two Sum
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
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

## 📜 problem
- input: 정수가 담긴 배열 nums, 정수 target
- output: index들(indices)을 배열에 담아 반환 (배열nums의 원소를 더해서 target이 나오는 경우)
  - 주의: 한 원소를 2번 이상 사용 못함, 정답은 어떤 순서로 반환하든 상관 없음
  - 테스트 케이스 생각
    - 타겟이 절대 나오지 않는 경우라면? => Only one valid answer exists.
    - 음수이거나 0일 떄 다르게 처리할 게 있을까? => 단순 덧셈뺄셈 연산이라 특별히 처리할 부분은 없을 것.

## 💭 approach
### 결정: 주어진 배열 nums를 map 객체로 변환 후, 원소 1개씩 검사하며 target과의 차이값이 내부에 존재하는지 확인한다.

### 결정 까지 생각의 흐름 기록.
#### target도 정수, 배열 nums의 원소도 정수. 정수 2개를 더해서 정수가 나오는 경우 어떻게 효율적으로 접근할 수 있을까?
#### 우선 가장 먼저 떠오르는 방법: 배열 nums의 첫 원소부터 돌면서 target과 차이를 구하고, 해당 차이가 nums의 원소로 있는지 검사해서 해당 index들을 반환하는 방법. => 최악의 경우 배열의 모든 원소를 돌아야 할 수 있으니 다른 방법도 생각해보자.
#### 배열의 특정 요소를 찾을 때, 최대한 효율적으로 할 수 있는 방법은 배열 그대로 찾지 않고 해시 테이블 자료구조를 끼고 활용하는게 나을 것이다. index를 최종 반환하려면 배열, map객체를 활용해야 할 것이고.
#### map객체가 index를 기억할 수 있고, 탐색도 빠르기 떄문에 이 map 객체 자료구조를 활용해보자.
// 여기까지 10분 소요.    

## ➕ one more thing
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