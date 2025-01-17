# git command

<!-- toc -->

- [context](#context)
  * [git도 '의도'를 먼저 정의하고 사용해야 한다.](#git%EB%8F%84-%EC%9D%98%EB%8F%84%EB%A5%BC-%EB%A8%BC%EC%A0%80-%EC%A0%95%EC%9D%98%ED%95%98%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%9C%EB%8B%A4)
- [content](#content)
  * [`git rebase`](#git-rebase)
    + [맥락: 협업 중 최신 코드 업데이트 후 충돌 해결 중 중복 커밋 발생, `rebase` 중 이전 commit과 동일한 커밋을 남긴 것이 원인.](#%EB%A7%A5%EB%9D%BD-%ED%98%91%EC%97%85-%EC%A4%91-%EC%B5%9C%EC%8B%A0-%EC%BD%94%EB%93%9C-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%ED%9B%84-%EC%B6%A9%EB%8F%8C-%ED%95%B4%EA%B2%B0-%EC%A4%91-%EC%A4%91%EB%B3%B5-%EC%BB%A4%EB%B0%8B-%EB%B0%9C%EC%83%9D-rebase-%EC%A4%91-%EC%9D%B4%EC%A0%84-commit%EA%B3%BC-%EB%8F%99%EC%9D%BC%ED%95%9C-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%82%A8%EA%B8%B4-%EA%B2%83%EC%9D%B4-%EC%9B%90%EC%9D%B8)
    + [왜 `rebase`라고 하는가?](#%EC%99%9C-rebase%EB%9D%BC%EA%B3%A0-%ED%95%98%EB%8A%94%EA%B0%80)
    + [`rebase`를 하지 않으면? 단순 base 지점을 옮겨서 보기 좋게 하는 것 외.](#rebase%EB%A5%BC-%ED%95%98%EC%A7%80-%EC%95%8A%EC%9C%BC%EB%A9%B4-%EB%8B%A8%EC%88%9C-base-%EC%A7%80%EC%A0%90%EC%9D%84-%EC%98%AE%EA%B2%A8%EC%84%9C-%EB%B3%B4%EA%B8%B0-%EC%A2%8B%EA%B2%8C-%ED%95%98%EB%8A%94-%EA%B2%83-%EC%99%B8)

<!-- tocstop -->

## context

### git도 '의도'를 먼저 정의하고 사용해야 한다.

- 커밋을 남기든, 브랜치를 최신 상태로 업데이트 하든 내가 무엇을 하고자 하는지 명확하게 정의하고 그에 맞는 명령어들을 사용할 것.
- 의도를 코드화 하고자 하면, git 명령어도 작은 단위 의사코드로 작성할 수 있을 것. 간단한 예로 "로컬 리포지토리의 작업사항을 원격 리포지토리로 업데이트하고 싶다"는 '의도'가 있다고 하자. 이는 "(1) 현재 변경사항을 저장한다, (2) 커밋할 단위별로 변경사항을 스테이징 한다, (3) 커밋한다, (4) 연결된 원격 저장소로 최신 커밋들을 업데이트 한다"로 쪼갤 수 있다.
- 명확한 의도, 알맞는 명령어를 쓸 수 있게 희미하게 알거나 어려움을 반복했던 것을 기록해볼 것.

## content

### `git rebase`

#### 맥락: 협업 중 최신 코드 업데이트 후 충돌 해결 중 중복 커밋 발생, `rebase` 중 이전 commit과 동일한 커밋을 남긴 것이 원인.

- [문제의 PR](https://github.com/Team-Bloblow/Bloblow-Client/pull/19/commits)

#### 왜 `rebase`라고 하는가?

- 결론: base 지점을 바꾸는 것, 즉 현재 작업하는 브랜치가 출발한 지점을, 최신화된 브랜치(main 혹은 dev 등)로 옮기고 싶은 것. ([참고 - Rebase와 Conflict 해결 방법](https://wonyong-jang.github.io/git/2021/02/05/Github-Rebase.html))

#### `rebase`를 하지 않으면? 단순 base 지점을 옮겨서 보기 좋게 하는 것 외.

- 기능적 문제는 없는가?
