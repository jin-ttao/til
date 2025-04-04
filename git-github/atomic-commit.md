# Atomic Commit을 처음 만나고

## context

* 원문 [How atomic Git commits dramatically increased my productivity - and will increase yours too](https://dev.to/samuelfaure/how-atomic-git-commits-dramatically-increased-my-productivity-and-will-increase-yours-too-4a84)을 번역한 글 [개발 생산성을 높이는 원자적 커밋 (Atomic Commit)](https://devloun.tistory.com/entry/%EC%9B%90%EC%9E%90%EC%A0%81-%EC%BB%A4%EB%B0%8B#google_vignette)을 참고했다.
* 번역글에서 인용 부분은 인용 표시로 구분했고, 내 해석과 의견은 🔻이모지와 함께 명시했다.
*   원문은 도입부에서 '앎 vs 진짜 앎'의 차이를 들면서, 개념은 알지만 실천하지 못하는 것은 엄청난 차이임을 강조한다.

    > This long introduction is here to illustrate a point: you can know what you should do, but you might not know how important it is to actually do it.
    >
    > * So many people out there, just like I did before, know how TDD is great... yet still don't use it. // TDD 얼마나 좋은지 알면서 쓰지 않는 현실..
    > * The simplest concepts can often completely change the way you work... if you would only apply them. Introducing: the atomic git commits. // 단순 커밋 습관이 아니라, 업무 방식을 근본적으로 바꾸는 것에 대한 글임을 시사함. (웅장)

## content

> 원자적 커밋이란?
>
> * 원자적 커밋(또는 Atomic git commit)은 커밋의 크기가 가능한 한 작다는 것을 의미합니다. 각 커밋은 간단한 문장으로 요약할 수 있는 단 하나의 간단한 작업을 수행합니다. 이때, 변경된 코드의 양은 중요하지 않습니다. 한 글자일 수도 있고, 십만 줄이 될 수도 있지만, 변경 내역이 짧고 간단한 하나의 문장으로 설명될 수 있어야 합니다.

### 커밋 각각 완전히 동작하는 작은 기능 단위여야 함. 🧐그럼 아직 구현을 마무리 하지 못한 코드들은 전부 제거해두고 커밋을 해야할까?

> 이상적으로는, 커밋을 할 때 테스트 스위트(Test Suite, 테스트 케이스들을 하나로 묶은 단위)가 '녹색'인 상태가 되는 것입니다. 즉, 원자적 커밋은 변경점은 가능한 작은 크기에서 (테스트를 통과한) 완전한 커밋을 지향한다고 볼 수 있습니다.

### 이유1. 되돌리기 쉬움 (변화 대응에 유연)

> 이유1. 원자적 커밋을 작성함으로써, 우리는 모든 변경사항을 간단하게 되돌릴 수 있습니다. (역자 의견: 작은 단위의 커밋일수록 되돌리기에 더 수월하다는 점을 이야기하는 것 같습니다.)

### 1번 이유와 비슷해보이지만, 문제가 생겼을 떄 대응에 대한 것. 1번은 평소 버전 관리를 해두면 언제든 돌아가기 쉽다는 편의성을 이야기 한 것.

> 이유2. 문제가 발생했을 때, 명료한 git 기록은 마치 불이 나기 전 집의 보험을 드는 것과 같은 의미를 갖습니다.

### 3번 이유가 인상적. **기능1은 n개의 세부기능들로 이루어져 있을 것. 그 세부기능 단위로, 가능한 작게 커밋을 하는 것이 좋다는 의미.** 그러려면 문제를 잘 쪼개고 해결단계도 잘 쪼갤줄 알아야 함. 커밋 메시지는 그 다음이다. 커밋 메시지는 커밋 내용(코드)을 감싼 ‘포장지’일 뿐이다.

> 이유 3. Pull Request 검토에 용이함
>
> * 필자가 생각하는 원자적 커밋을 해야 하는 가장 중요한 이유이기도 한데요. 문제 해결에 접근하는 방식이 완전히 바뀔 수 있다는 점입니다.
> * 크고 복잡한 작업을 완료하기 위해 잘 알려진 방법은 더 작고 관리하고 쉬운 단계로 줄이는 것입니다. 각 단계는 해결해야 하는 해결해야 할 문제입니다.
> * 어쩌면 이미 많이 들어봤을 법한 조언이지만 실제로 업무에서 제대로 실천하고 있는지는 스스로 돌아봐야 할 부분입니다.
> * 그리고 필자는 이를 실천하기 좋은 방법이 바로 원자적 커밋을 작성하는 것이라고 합니다. 원자적 커밋에서 더 작은 단계로 단순화하여, 올바른 방식으로 작업에 접근해야 합니다. 결국 복잡성을 단순화하는 것이 핵심입니다.

### 결국 연습이 중요. **작업 전 커밋 계획을 먼저 세우고, 작업을 진행하는 것이 방법일 수 있겠다. 의사코드를 작성하듯이.** 지금 작성하는 til도 바로 커밋해야지.

> 작업을 더 간단히, 더 관리하기 쉽게, 그리고 가장 중요한 '더 쉽게' 만드세요. 스몰 스텝 하세요. 작은 커밋을 작성하세요. 그렇게 일상의 원자적 커밋을 실천해 보길 바랍니다.
