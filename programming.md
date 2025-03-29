---
icon: '0'
---

# 개발하면서 든 생각들

## 코드 가독성 ⬆︎

엣지 케이스를 항상 별도로 처리하는 것이 최선은 아니다. (25.02.22 알고리즘 풀면서)

* 이번 알고리즘 문제에서는 분기 처리된 로직(`Math.max()`와 유사)이 결국 동일한 결과를 도출하기 때문에, 통합 처리하는 것이 가독성 측면에서 더 유리했었다.
* 예외 케이스는 그 자체로 처리하는 것이 목적일 때만 별도로 다루도록 하자.

<details>

<summary>코드 비교</summary>

```js
// 현재
if (gain.length === 1) {
  return Math.max(0, gain[0]);
}

// 통합해보면? ✅
const largestAltitude = function(gain) {
  let altitude = 0;
  let max = 0;
  
  for (const change of gain) {
      altitude += change;
      max = Math.max(max, altitude);
  }
  
  return max;
}
```

</details>

\
\


## 개발하면서 든 생각들

* 이제 저와 함께 살펴봅시다. 명확한 가치를 자주 배포하는 데 초점을 맞춰 소프트웨어 개발을 더 간결하게 만드는 방법을요. (책 - THE NATURE OF SOFTWARE DEVELOPMENT)
* 가끔은 더 나은 곳으로 가기 위해 하고 있는 모든 것을 내려놓아야만 합니다. 물론 실패할수도 있지만 아닐수도 있습니다. 인생이란 그런 것이니까요. (책 - THE NATURE OF SOFTWARE DEVELOPMENT)

### 내 습관 분석

> 주니어 개발자로서 내가 어떤 개발 습관이 있는지 빠르게 인지 ㄱㄱ
>
> 강점 극대화, 약점 보완하는게 성장 속도 내는 데 중요할 것.

#### 명시적으로 코드를 작성하려는 성향이 자주 발견되는 것 같다. ⇒ 기존에 검증된 다양한 패턴을 학습하는게 필요하겠다.

* 한 가지 발견한 점은 나의 '명시적 코드 작성' 습관. 장단점이 있을 것 같은데, 내가 보기에도 괜히 장황한 코드로 이어지는 경우가 종종 있다. 코드의 동작을 알 수 있어서 좋긴 한데…
  * ⁠while 루프, if 조건문 사용해서 문자열 하나씩 처리하려는 방식으로 문제 풀려고 함
  * str, ⁠substrings 명시적으로 변수 선언하고 조작해서 결과를 얻으려고 함

#### 그럼, 명시적으로 코드 작성하려는 습관은 원인이 뭘까.

* 머리 속에 문제 해결방향이 완벽히 정리가 되지 않아서 하나씩 해보려는 접근에서 나온 걸까.
* 필요한 재료를 모두 준비해두고 그 중 취사선택하려는 심리도 작용했을 것 같다.
* 알고리즘 풀 때 외에도 실제 리액트 앱 구현할 때에도 비슷한 습관이 종종 보였었다.
* 오늘 알고리즘 풀 때 문제를 단계별로 분해, 결과 내려고 중간 과정에서 데이터를 저장하려는 시도는 좋았지만, 결국 문제는 “최대 길이”만 구하면 된다.
  * 문제의 본질은 중간 부분 부분 문자열을 구하는 것과 거리가 멀 수 있다.

**매일 했던 방식으로 개발하면 소용 없다. 그냥 일회성 개발하는 것**

* 외주 개발과 다를 것 없음. 어제와 다르게 하게 된 건 뭔지 기록하기
* 중요한 건 매번 똑같은 방법으로 하지 않고 다른 방법으로 시도해보려고 한 것.
  * 틀린 방법이었을 수 있지만 관점을 확장해나가는 것이 중요함.
* welcome-toast 구현하면서 `Redirect Modal` 컴포넌트 만들고 있었다.
* 예전 같았으면 특수한 맥락이 잔뜩 담긴 모달로 바로 구성하려고 했을 것.
  * 지하철에서 당근 원지혁님 유튜브 Declative UI 보면서 와닿지 않지만 호기심이 생기는 지점들이 많았다. 그래서 얼추 비슷하게 따라해봄.
* 아주 조금 '이걸 왜 하는지' 체감했지만 아직 소화하지는 못 했다.
* 이번 경험에서 중요한 건 매번 똑같은 방법으로 하지 않고 다른 방법으로 시도해보려고 한 것.\\

### 개선해보자

> 더 좋은 코드를 작성할 수 있을 것만 같은

#### 리팩토링 - 상태 업데이트 더 효율적으로 할 수 있는 방법 있을 듯… 우선 상수로 1차 개선

```js
// to-be
const [isOpenModal, setIsOpenModal] = useState(INITIAL_MODAL);

// as-is
const [isOpenModal, setIsOpenModal] = useState({
  create: false,
  install: false,
  delete: false,
});

// ModalBackground 컴포넌트
useEffect(() => {
  function handleModalBackgroundClick(event) {
    if (event?.target === backgroundRef.current) {
      // 개선하고 싶은 부분
      setIsOpenModal({
        create: false,
        install: false,
        delete: false,
      });
    }
  }

  // ...
}, [setIsOpenModal, canCloseBackgroundClick]);
```

\\

#### CSS 공통 모듈로 하는 것 얼른 적용시켜야겠다. 일일이 찾아서 해주기 번거롭네…

\\

### 아이디어

> 그냥 개발하다가 생각나는 아이디어들

#### 리액트에서 컴포넌트 directory 위치 바꾸면 알아서 import path도 업데이트 해주는거 없나…

* "react directory path auto update" 키워드 등으로 검색해봤는데 마땅히 최근 솔루션은 많이 보이지 않음.
* 없으면 내가 만들어볼 수 있을까?
