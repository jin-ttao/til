# Atomic Commit

<!-- toc -->

- [context](#context)
- [content](#content)
  - [커밋 각각 완전히 동작하는 작은 기능 단위여야 함. 🧐그럼 아직 구현을 마무리 하지 못한 코드들은 전부 제거해두고 커밋을 해야할까?](#%EC%BB%A4%EB%B0%8B-%EA%B0%81%EA%B0%81-%EC%99%84%EC%A0%84%ED%9E%88-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94-%EC%9E%91%EC%9D%80-%EA%B8%B0%EB%8A%A5-%EB%8B%A8%EC%9C%84%EC%97%AC%EC%95%BC-%ED%95%A8-%F0%9F%A7%90%EA%B7%B8%EB%9F%BC-%EC%95%84%EC%A7%81-%EA%B5%AC%ED%98%84%EC%9D%84-%EB%A7%88%EB%AC%B4%EB%A6%AC-%ED%95%98%EC%A7%80-%EB%AA%BB%ED%95%9C-%EC%BD%94%EB%93%9C%EB%93%A4%EC%9D%80-%EC%A0%84%EB%B6%80-%EC%A0%9C%EA%B1%B0%ED%95%B4%EB%91%90%EA%B3%A0-%EC%BB%A4%EB%B0%8B%EC%9D%84-%ED%95%B4%EC%95%BC%ED%95%A0%EA%B9%8C)
  - [이유1. 되돌리기 쉬움 (변화 대응에 유연)](#%EC%9D%B4%EC%9C%A01-%EB%90%98%EB%8F%8C%EB%A6%AC%EA%B8%B0-%EC%89%AC%EC%9B%80-%EB%B3%80%ED%99%94-%EB%8C%80%EC%9D%91%EC%97%90-%EC%9C%A0%EC%97%B0)
  - [1번 이유와 비슷해보이지만, 문제가 생겼을 떄 대응에 대한 것. 1번은 평소 버전 관리를 해두면 언제든 돌아가기 쉽다는 편의성을 이야기 한 것.](#1%EB%B2%88-%EC%9D%B4%EC%9C%A0%EC%99%80-%EB%B9%84%EC%8A%B7%ED%95%B4%EB%B3%B4%EC%9D%B4%EC%A7%80%EB%A7%8C-%EB%AC%B8%EC%A0%9C%EA%B0%80-%EC%83%9D%EA%B2%BC%EC%9D%84-%EB%96%84-%EB%8C%80%EC%9D%91%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B2%83-1%EB%B2%88%EC%9D%80-%ED%8F%89%EC%86%8C-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%A5%BC-%ED%95%B4%EB%91%90%EB%A9%B4-%EC%96%B8%EC%A0%9C%EB%93%A0-%EB%8F%8C%EC%95%84%EA%B0%80%EA%B8%B0-%EC%89%BD%EB%8B%A4%EB%8A%94-%ED%8E%B8%EC%9D%98%EC%84%B1%EC%9D%84-%EC%9D%B4%EC%95%BC%EA%B8%B0-%ED%95%9C-%EA%B2%83)
  - [3번 이유가 인상적. **기능1은 n개의 세부기능들로 이루어져 있을 것. 그 세부기능 단위로, 가능한 작게 커밋을 하는 것이 좋다는 의미.** 그러려면 문제를 잘 쪼개고 해결단계도 잘 쪼갤줄 알아야 함. 커밋 메시지는 그 다음이다. 커밋 메시지는 커밋 내용(코드)을 감싼 ‘포장지’일 뿐이다.](#3%EB%B2%88-%EC%9D%B4%EC%9C%A0%EA%B0%80-%EC%9D%B8%EC%83%81%EC%A0%81-%EA%B8%B0%EB%8A%A51%EC%9D%80-n%EA%B0%9C%EC%9D%98-%EC%84%B8%EB%B6%80%EA%B8%B0%EB%8A%A5%EB%93%A4%EB%A1%9C-%EC%9D%B4%EB%A3%A8%EC%96%B4%EC%A0%B8-%EC%9E%88%EC%9D%84-%EA%B2%83-%EA%B7%B8-%EC%84%B8%EB%B6%80%EA%B8%B0%EB%8A%A5-%EB%8B%A8%EC%9C%84%EB%A1%9C-%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%9E%91%EA%B2%8C-%EC%BB%A4%EB%B0%8B%EC%9D%84-%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EC%A2%8B%EB%8B%A4%EB%8A%94-%EC%9D%98%EB%AF%B8-%EA%B7%B8%EB%9F%AC%EB%A0%A4%EB%A9%B4-%EB%AC%B8%EC%A0%9C%EB%A5%BC-%EC%9E%98-%EC%AA%BC%EA%B0%9C%EA%B3%A0-%ED%95%B4%EA%B2%B0%EB%8B%A8%EA%B3%84%EB%8F%84-%EC%9E%98-%EC%AA%BC%EA%B0%A4%EC%A4%84-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A8-%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80%EB%8A%94-%EA%B7%B8-%EB%8B%A4%EC%9D%8C%EC%9D%B4%EB%8B%A4-%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80%EB%8A%94-%EC%BB%A4%EB%B0%8B-%EB%82%B4%EC%9A%A9%EC%BD%94%EB%93%9C%EC%9D%84-%EA%B0%90%EC%8B%BC-%ED%8F%AC%EC%9E%A5%EC%A7%80%EC%9D%BC-%EB%BF%90%EC%9D%B4%EB%8B%A4)
  - [결국 연습이 중요. **작업 전 커밋 계획을 먼저 세우고, 작업을 진행하는 것이 방법일 수 있겠다. 의사코드를 작성하듯이.** 지금 작성하는 til도 바로 커밋해야지.](#%EA%B2%B0%EA%B5%AD-%EC%97%B0%EC%8A%B5%EC%9D%B4-%EC%A4%91%EC%9A%94-%EC%9E%91%EC%97%85-%EC%A0%84-%EC%BB%A4%EB%B0%8B-%EA%B3%84%ED%9A%8D%EC%9D%84-%EB%A8%BC%EC%A0%80-%EC%84%B8%EC%9A%B0%EA%B3%A0-%EC%9E%91%EC%97%85%EC%9D%84-%EC%A7%84%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EB%B0%A9%EB%B2%95%EC%9D%BC-%EC%88%98-%EC%9E%88%EA%B2%A0%EB%8B%A4-%EC%9D%98%EC%82%AC%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%98%EB%93%AF%EC%9D%B4-%EC%A7%80%EA%B8%88-%EC%9E%91%EC%84%B1%ED%95%98%EB%8A%94-til%EB%8F%84-%EB%B0%94%EB%A1%9C-%EC%BB%A4%EB%B0%8B%ED%95%B4%EC%95%BC%EC%A7%80)

<!-- tocstop -->

## context

- 원문 [How atomic Git commits dramatically increased my productivity - and will increase yours too](https://dev.to/samuelfaure/how-atomic-git-commits-dramatically-increased-my-productivity-and-will-increase-yours-too-4a84)을 번역한 글 [개발 생산성을 높이는 원자적 커밋 (Atomic Commit)](https://devloun.tistory.com/entry/%EC%9B%90%EC%9E%90%EC%A0%81-%EC%BB%A4%EB%B0%8B#google_vignette)을 참고했다.
- 번역글에서 인용 부분은 인용 표시로 구분했고, 내 해석과 의견은 🔻이모지와 함께 명시했다.
- 원문은 도입부에서 '앎 vs 진짜 앎'의 차이를 들면서, 개념은 알지만 실천하지 못하는 것은 엄청난 차이임을 강조한다.
  > This long introduction is here to illustrate a point: you can know what you should do, but you might not know how important it is to actually do it.
  >
  > - So many people out there, just like I did before, know how TDD is great... yet still don't use it. // TDD 얼마나 좋은지 알면서 쓰지 않는 현실..
  > - The simplest concepts can often completely change the way you work... if you would only apply them. Introducing: the atomic git commits. // 단순 커밋 습관이 아니라, 업무 방식을 근본적으로 바꾸는 것에 대한 글임을 시사함. (웅장)

## content

> 원자적 커밋이란?
>
> - 원자적 커밋(또는 Atomic git commit)은 커밋의 크기가 가능한 한 작다는 것을 의미합니다. 각 커밋은 간단한 문장으로 요약할 수 있는 단 하나의 간단한 작업을 수행합니다. 이때, 변경된 코드의 양은 중요하지 않습니다. 한 글자일 수도 있고, 십만 줄이 될 수도 있지만, 변경 내역이 짧고 간단한 하나의 문장으로 설명될 수 있어야 합니다.

### 커밋 각각 완전히 동작하는 작은 기능 단위여야 함. 🧐그럼 아직 구현을 마무리 하지 못한 코드들은 전부 제거해두고 커밋을 해야할까?

> 이상적으로는, 커밋을 할 때 테스트 스위트(Test Suite, 테스트 케이스들을 하나로 묶은 단위)가 '녹색'인 상태가 되는 것입니다. 즉, 원자적 커밋은 변경점은 가능한 작은 크기에서 (테스트를 통과한) 완전한 커밋을 지향한다고 볼 수 있습니다.

### 이유1. 되돌리기 쉬움 (변화 대응에 유연)

> 이유1. 원자적 커밋을 작성함으로써, 우리는 모든 변경사항을 간단하게 되돌릴 수 있습니다. (역자 의견: 작은 단위의 커밋일수록 되돌리기에 더 수월하다는 점을 이야기하는 것 같습니다.)

### 1번 이유와 비슷해보이지만, 문제가 생겼을 떄 대응에 대한 것. 1번은 평소 버전 관리를 해두면 언제든 돌아가기 쉽다는 편의성을 이야기 한 것.

> 이유2. 문제가 발생했을 때, 명료한 git 기록은 마치 불이 나기 전 집의 보험을 드는 것과 같은 의미를 갖습니다.

### 3번 이유가 인상적. **기능1은 n개의 세부기능들로 이루어져 있을 것. 그 세부기능 단위로, 가능한 작게 커밋을 하는 것이 좋다는 의미.** 그러려면 문제를 잘 쪼개고 해결단계도 잘 쪼갤줄 알아야 함. 커밋 메시지는 그 다음이다. 커밋 메시지는 커밋 내용(코드)을 감싼 ‘포장지’일 뿐이다.

> 이유 3. Pull Request 검토에 용이함
>
> - 필자가 생각하는 원자적 커밋을 해야 하는 가장 중요한 이유이기도 한데요. 문제 해결에 접근하는 방식이 완전히 바뀔 수 있다는 점입니다.
> - 크고 복잡한 작업을 완료하기 위해 잘 알려진 방법은 더 작고 관리하고 쉬운 단계로 줄이는 것입니다. 각 단계는 해결해야 하는 해결해야 할 문제입니다.
> - 어쩌면 이미 많이 들어봤을 법한 조언이지만 실제로 업무에서 제대로 실천하고 있는지는 스스로 돌아봐야 할 부분입니다.
> - 그리고 필자는 이를 실천하기 좋은 방법이 바로 원자적 커밋을 작성하는 것이라고 합니다.
>   원자적 커밋에서 더 작은 단계로 단순화하여, 올바른 방식으로 작업에 접근해야 합니다. 결국 복잡성을 단순화하는 것이 핵심입니다.

### 결국 연습이 중요. **작업 전 커밋 계획을 먼저 세우고, 작업을 진행하는 것이 방법일 수 있겠다. 의사코드를 작성하듯이.** 지금 작성하는 til도 바로 커밋해야지.

> 작업을 더 간단히, 더 관리하기 쉽게, 그리고 가장 중요한 '더 쉽게' 만드세요. 스몰 스텝 하세요. 작은 커밋을 작성하세요. 그렇게 일상의 원자적 커밋을 실천해 보길 바랍니다.
