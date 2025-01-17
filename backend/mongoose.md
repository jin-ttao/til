# mongoose

### 왜 `.exec` 메소드를 사용할까?
- .exec 메소드를 안쓰면
  - Promise가 아니고 thenable 성질을 가짐.
  - 즉 .then 만 쓸 수 있는 반쪽 짜리 promise임. 단순 콜백함수 처럼 그 다음 작업 수행만 제어할 수 있음.
- .exec 메소드를 쓰면
  - 온전한 Promise를 활용할 수 있음
  - 공식 문서 "Mongoose queries are not promises. They have a .then() function for co and async/await as a convenience. If you need a fully-fledged promise, use the .exec() function."
- 그래서 쓸까 말까? => 가급적 .exec 메소드 쓰자!
  - Promise 활용 가능 good
  - 추적하기 좋아서 디버깅 good
  - "쿼리 실행"의 의도를 더 드러낼 수 있고, 코드 가독성 good.
  - 공식 문서 "As far as functionality is concerned, these two are equivalent. However, we recommend using .exec() because that gives you better stack traces."
    - stack traces: 컴퓨팅 관점에서, 프로그램 실행 중 특정 시점을 추적할 수 있는 것을 의미.
- 더 시도해볼 것
  - 모든 상황에서 쓰는지, Qurey 관련 상황에 한하는지 체크

#### `.exec` 실제로 활용해봄 (업데이트 24.11.11)
[BloBlow 프로젝트 Pull Request](https://github.com/Team-Bloblow/Bloblow-Server/pull/15#discussion_r1835308132)
```js
const isDuplicatedKeyword = await groupModel
    .findOne({ _id: req.body.groupId })
    .populate("keywordIdList", "keyword")
    .exec()
    .then((query) => {
      return query.keywordIdList.some((doc) => doc.keyword === req.body.keyword);
    })
    .catch((error) => {
      return res.status(400).send({ message: "[InvalidGroupId] Error occured" });
    });
```
- 왜 `exec()`를 썼는가?
  - 쿼리 빌드(쿼리 조건 설정) 후, 바로 이어서 쿼리 결과를 활용할 의도였다. `groupId`로 쿼리한 결과에서 `keyword` 이름을 비교하는 로직이었다.
  - 복기해보니 `exec()`는 순수한 Promise를 반환하기 때문에, 쿼리 조건 설정과 결과 추출을 분리할 수 있겠다. 수정하고 테스트 해보자. 아래 처럼 해볼 수 있을 것 같은데?!
```js
// to-be
const group = await groupModel
  .findOne({ _id: req.body.groupId })
  .populate("keywordIdList", "keyword")
  .exec();
const isDuplicatedKeyword = group.keywordIdList.some((doc) => doc.keyword === req.body.keyword);
```
