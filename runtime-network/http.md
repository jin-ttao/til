# HTTP

# Definition

> Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML. <br> It was designed for communication between web browsers and web servers, (...)
> [MDN - HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)

### Hypertext Transfer Protocol (HTTP) : HTML의 'HT(Hypertext)'가 동일한 것으로 보임.

### 웹브라우저와 웹서버의 communication을 위한 것.

### # HTTP 정의에 등장하는 용어들 이해하기 : `hypermedia`, `application-layer`

<br>

# 💡 HTTP 상태 코드, 어떻게 정의할까?

## context

- 이번 프로젝트에서 처음으로 API별 HTTP 상태 코드를 정의하게 되었다.
- 처음에는 단순하게 생각했다. "어떤 API든 에러는 비슷하지 않을까?" 하는 생각에 공통적으로 발생할 수 있는 에러 코드만 제너럴하게 먼저 정리해두었다.
- 하지만 "각 API마다 HTTP 상태 코드가 정의되어야 할 것"이라는 피드백을 받고 [YouTube API](https://developers.google.com/youtube/v3/docs/errors), GitHub의 API 문서를 찾아보게 되었다. 실제 서비스들의 에러 처리 방식을 보니 유용한 부분이 많았다.
- 그리고 나만의 HTTP 상태 코드 작성하는 방법론도 고민하게 되었는데, 자세한 내용은 아래 기재했다.
- 참고
  - [MDN 공식문서: HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
  - [NHN 클라우드: REST API 제대로 알고 사용하기](https://meetup.nhncloud.com/posts/92)
  - [더 자유롭고, 빠르고, 정확하게: 토스페이먼츠 API 문서 엔지니어링](https://velog.io/@tosspayments/%EB%8D%94-%EC%9E%90%EC%9C%A0%EB%A1%AD%EA%B3%A0-%EB%B9%A0%EB%A5%B4%EA%B3%A0-%EC%A0%95%ED%99%95%ED%95%98%EA%B2%8C-%ED%86%A0%EC%8A%A4%ED%8E%98%EC%9D%B4%EB%A8%BC%EC%B8%A0-API-%EB%AC%B8%EC%84%9C-%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81)

## content

#### ⚡ 같은 4xx대 에러도 원인을 세부적으로 구분해서 명시할 것.

단순히 404, 500 같은 숫자 코드만 던지는 게 아니었다. 어떤 상황에서 에러가 발생했는지 구체적으로 설명하고, 같은 4xx대 에러라도 원인을 세부적으로 구분해서 명시하고 있었다!

#### 🤔 의견) 육하원칙으로 클라이언트 request를 먼저 정의해보면, 에러 시나리오를 MECE하게 정의할 수 있지 않을까?

이번에 처음 HTTP 상태 코드를 짜며, 쏠쏠한 요령도 정립해봤다. 바로, API의 정상적인 흐름을 먼저 정리해보는 것이다. 육하원칙으로 클라이언트의 request를 - 누가, 언제, 무엇을, 어떻게, 왜 하는지를 먼저 정의해보는 것이다. 그리고 이 조건들을 충족하지 못하는 경우를 에러로 정의하는 방식이다. 가령, 로그인이 필요한 API면 인증되지 않은 사용자의 접근을 에러로 처리하고, 특정 권한이 필요한 API면 권한이 없는 사용자의 요청을 에러로 처리하는 식이다. 이 방법과 request 데이터 중 의도와 달리 요청이 발생할 상황을 예상해보면서 HTTP 상태 코드 초안을 작성해보았다.

#### 🤔 헷갈렸던 것) 어디까지 서버의 에러 처리로 둬야 하나? (클라이언트의 유효성 검사와 혼동) => 결론: 각각 역할이 다르지만 서로 협업 가능.

서버 입장에서 예기치 않은 상황을 생각해봤다. 그러다보니 자연스럽게 앞단의 request를 보내기 전 클라이언트 단계에서 '마치 에러를 감지하는 듯한 역할을 하는' 유효성 검사가 생각났다. 이 클라이언트 단의 유효성 검사와 서버의 에러 처리를 어떻게 구분해야 할지는 명확하지 않았다.

클라이언트 유효성 검사는 잘못된 이메일 형식 등 대개 '사용자 입력값에 대해 즉각적인 피드백을 주는 것'에 집중한다. (클라이언트 유효성 검사에 대한 MDN 공식문서도 있더라! 신기했다. [MDN 공식 문서: Client-side form validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation))

한편, 서버 측 에러는 데이터가 오염되지 않거나 보안 등을 위해서 최종 방어선 역할을 하는 것으로 보였다. 특히 서버는 "무엇이 잘못되었는지"를 명확하게 알려줘야, 클라이언트에서 적절한 대응이 가능하다는 점을 배웠다. ([프론트엔드에서"만" 유효성 검사가 문제인 이유](https://jojoldu.tistory.com/157)) 앞으로 클라이언트, 서버 양측에서 대응해줘야 할 범위를 생각하면서 구현을 해야겠다.

#### 🤔 아무쪼록 API 문서는 구현 중에도 계속 보완해나가야 할 것. 앞으로도 공신력 있는 실제 서비스들의 예시를 더 찾아보면서 좋은 패턴들을 배워야겠다.
