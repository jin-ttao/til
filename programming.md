# programming 하면서

<!-- toc -->

- [내 습관 분석](#%EB%82%B4-%EC%8A%B5%EA%B4%80-%EB%B6%84%EC%84%9D)
  * [명시적으로 코드를 작성하려는 성향이 자주 발견되는 것 같다. ⇒ 기존에 검증된 다양한 패턴을 학습하는게 필요하겠다.](#%EB%AA%85%EC%8B%9C%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%98%EB%A0%A4%EB%8A%94-%EC%84%B1%ED%96%A5%EC%9D%B4-%EC%9E%90%EC%A3%BC-%EB%B0%9C%EA%B2%AC%EB%90%98%EB%8A%94-%EA%B2%83-%EA%B0%99%EB%8B%A4-%E2%87%92-%EA%B8%B0%EC%A1%B4%EC%97%90-%EA%B2%80%EC%A6%9D%EB%90%9C-%EB%8B%A4%EC%96%91%ED%95%9C-%ED%8C%A8%ED%84%B4%EC%9D%84-%ED%95%99%EC%8A%B5%ED%95%98%EB%8A%94%EA%B2%8C-%ED%95%84%EC%9A%94%ED%95%98%EA%B2%A0%EB%8B%A4)
  * [그럼, 명시적으로 코드 작성하려는 습관은 원인이 뭘까.](#%EA%B7%B8%EB%9F%BC-%EB%AA%85%EC%8B%9C%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1%ED%95%98%EB%A0%A4%EB%8A%94-%EC%8A%B5%EA%B4%80%EC%9D%80-%EC%9B%90%EC%9D%B8%EC%9D%B4-%EB%AD%98%EA%B9%8C)
  * [매일 했던 방식으로 개발하면 소용 없다. 그냥 일회성 개발하는 것. 외주 개발과 다를 것 없음. 어제와 다르게 하게 된 건 뭔지 기록하기](#%EB%A7%A4%EC%9D%BC-%ED%96%88%EB%8D%98-%EB%B0%A9%EC%8B%9D%EC%9C%BC%EB%A1%9C-%EA%B0%9C%EB%B0%9C%ED%95%98%EB%A9%B4-%EC%86%8C%EC%9A%A9-%EC%97%86%EB%8B%A4-%EA%B7%B8%EB%83%A5-%EC%9D%BC%ED%9A%8C%EC%84%B1-%EA%B0%9C%EB%B0%9C%ED%95%98%EB%8A%94-%EA%B2%83-%EC%99%B8%EC%A3%BC-%EA%B0%9C%EB%B0%9C%EA%B3%BC-%EB%8B%A4%EB%A5%BC-%EA%B2%83-%EC%97%86%EC%9D%8C-%EC%96%B4%EC%A0%9C%EC%99%80-%EB%8B%A4%EB%A5%B4%EA%B2%8C-%ED%95%98%EA%B2%8C-%EB%90%9C-%EA%B1%B4-%EB%AD%94%EC%A7%80-%EA%B8%B0%EB%A1%9D%ED%95%98%EA%B8%B0)
- [개선해보자](#%EA%B0%9C%EC%84%A0%ED%95%B4%EB%B3%B4%EC%9E%90)
  * [리팩토링 - 상태 업데이트 더 효율적으로 할 수 있는 방법 있을 듯… 우선 상수로 1차 개선](#%EB%A6%AC%ED%8C%A9%ED%86%A0%EB%A7%81---%EC%83%81%ED%83%9C-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EB%8D%94-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9C%BC%EB%A1%9C-%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B0%A9%EB%B2%95-%EC%9E%88%EC%9D%84-%EB%93%AF-%EC%9A%B0%EC%84%A0-%EC%83%81%EC%88%98%EB%A1%9C-1%EC%B0%A8-%EA%B0%9C%EC%84%A0)
  * [CSS 공통 모듈로 하는 것 얼른 적용시켜야겠다. 일일이 찾아서 해주기 번거롭네…](#css-%EA%B3%B5%ED%86%B5-%EB%AA%A8%EB%93%88%EB%A1%9C-%ED%95%98%EB%8A%94-%EA%B2%83-%EC%96%BC%EB%A5%B8-%EC%A0%81%EC%9A%A9%EC%8B%9C%EC%BC%9C%EC%95%BC%EA%B2%A0%EB%8B%A4-%EC%9D%BC%EC%9D%BC%EC%9D%B4-%EC%B0%BE%EC%95%84%EC%84%9C-%ED%95%B4%EC%A3%BC%EA%B8%B0-%EB%B2%88%EA%B1%B0%EB%A1%AD%EB%84%A4)
- [아이디어](#%EC%95%84%EC%9D%B4%EB%94%94%EC%96%B4)
  * [리액트에서 컴포넌트 directory 위치 바꾸면 알아서 import path도 업데이트 해주는거 없나…](#%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-directory-%EC%9C%84%EC%B9%98-%EB%B0%94%EA%BE%B8%EB%A9%B4-%EC%95%8C%EC%95%84%EC%84%9C-import-path%EB%8F%84-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%ED%95%B4%EC%A3%BC%EB%8A%94%EA%B1%B0-%EC%97%86%EB%82%98)

<!-- tocstop -->

<br>

## 내 습관 분석
> 주니어 개발자로서 내가 어떤 개발 습관이 있는지 빠르게 인지하고 강점 극대화, 약점 보완하는게 성장 속도 내는 데 중요하다고 생각한다.

<br>

### 명시적으로 코드를 작성하려는 성향이 자주 발견되는 것 같다. ⇒ 기존에 검증된 다양한 패턴을 학습하는게 필요하겠다.

- 한 가지 발견한 점은 나의 '명시적 코드 작성' 습관. 장단점이 있을 것 같은데, 내가 보기에도 괜히 장황한 코드로 이어지는 경우가 종종 있다. 코드의 동작을 알 수 있어서 좋긴 한데…
  - ⁠while 루프, if 조건문 사용해서 문자열 하나씩 처리하려는 방식으로 문제 풀려고 함
  - str, ⁠substrings 명시적으로 변수 선언하고 조작해서 결과를 얻으려고 함

<br>

### 그럼, 명시적으로 코드 작성하려는 습관은 원인이 뭘까.
- 머리 속에 문제 해결방향이 완벽히 정리가 되지 않아서 하나씩 해보려는 접근에서 나온 걸까.
- 필요한 재료를 모두 준비해두고 그 중 취사선택하려는 심리도 작용했을 것 같다.
- 알고리즘 풀 때 외에도 실제 리액트 앱 구현할 때에도 비슷한 습관이 종종 보였었다.
- 오늘 알고리즘 풀 때 문제를 단계별로 분해, 결과 내려고 중간 과정에서 데이터를 저장하려는 시도는 좋았지만, 결국 문제는 “최대 길이”만 구하면 된다.
  - 문제의 본질은 중간 부분 부분 문자열을 구하는 것과 거리가 멀 수 있다.

<br>

### 매일 했던 방식으로 개발하면 소용 없다. 그냥 일회성 개발하는 것. 외주 개발과 다를 것 없음. 어제와 다르게 하게 된 건 뭔지 기록하기

- 중요한 건 매번 똑같은 방법으로 하지 않고 다른 방법으로 시도해보려고 한 것. 틀린 방법이었을 수 있지만 관점을 확장해나가는 것이 중요함.
- welcome-toast 구현하면서 `Redirect Modal` 컴포넌트 만들고 있었다.
- 예전 같았으면 특수한 맥락이 잔뜩 담긴 모달로 바로 구성하려고 했을 것. 지하철에서 원지혁님 유튜브 Declative UI 보면서 와닿지 않지만 호기심이 생기는 지점들이 많았다. 그래서 얼추 비슷하게 따라해봄.
- 아주 조금 '이걸 왜 하는지' 체감했지만 아직 소화하지는 못 했다.
- 중요한 건 매번 똑같은 방법으로 하지 않고 다른 방법으로 시도해보려고 한 것.

<br>

## 개선해보자
> 더 좋은 코드를 작성할 수 있을 것만 같은

### 리팩토링 - 상태 업데이트 더 효율적으로 할 수 있는 방법 있을 듯… 우선 상수로 1차 개선
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

  if (canCloseBackgroundClick) {
    window.addEventListener("click", handleModalBackgroundClick);
    return () => window.removeEventListener("click", handleModalBackgroundClick);
  }
}, [setIsOpenModal, canCloseBackgroundClick]);
```

<br>

### CSS 공통 모듈로 하는 것 얼른 적용시켜야겠다. 일일이 찾아서 해주기 번거롭네…

<br>

## 아이디어
> 그냥 개발하다가 생각나는 아이디어들

### 리액트에서 컴포넌트 directory 위치 바꾸면 알아서 import path도 업데이트 해주는거 없나…
- "react directory path auto update" 키워드 등으로 검색해봤는데 마땅히 최근 솔루션은 많이 보이지 않음.
- 없으면 내가 만들어볼 수 있을까?
