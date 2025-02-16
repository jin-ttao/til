---
icon: '1'
---

# 용어 정의 모음

## Name & Definition

### HTTP

### Client 클라이언트

#### 모바일도 프로그래밍적으로 보면 컴퓨터라고 보면 될까?

![정의-클라이언트](assets/정의-클라이언트.png)

* 공식 문서

DNS

* 공식 문서

## API

### 💡 API 단어의 'Interface', 드디어 조금 이해가 된다.

오늘 정말 문득 깨달음이 왔다. API 단어에서 'Interface'라는 단어가 왜 쓰이는지 이제야 조금 감이 잡힌다. 'API'라는 개념을 대하는 나만의 경험이 생겼다는 점에서 의미가 있었다. API 문서에 request, response 예시를 작성하고 있었다. 이때 문득 '이렇게 작성해두면 백엔드 로직을 작성해볼 수 있겠다' 생각이 들었다. 이 생각이 자연스럽게 아래 생각으로 이어졌다.

UI(User Interface)가 사용자와 시스템 사이의 접점이듯, API(Application Programming Interface)는 프로그램들 사이의 접점. 프론트엔드 개발자가 UI를 보고 코드를 작성하는 것처럼, 백엔드 개발자는 API를 보고 코드 로직을 작성한다. 그래서 UI, API 양쪽에 'Interface'라는 단어를 굳이 사용한 것은 아닐까? 이론으로만 알던 것을 실제 프로젝트에서 API를 정의하고 사용하면서 비로소 체감되기 시작했다. 역시 개발은 직접 부딪혀봐야 제대로 이해가 되는 것 같다.

## Postman

팀 프로젝트를 하며 'Postman' 툴을 처음 사용해봤다. PM으로 일할 때, 엔지니어 분들이 이 툴로 '데이터 호출 결과'를 보셨던 기억이 난다. 프로젝트에서 API, HTTP 통신 개념을 많이 활용할 것이라 모르는 개념을 방치할 수 없다. 그때 그때 이해해보도록 하자⚡⚡

### 이름이 왜 Postman? : 이 자체가 클라이언트 역할해줌.

이름은 왜 Postman일까? 클라이언트와 서버 사이 중간에서 무언가 낚아채주는 역할인가? 어떻게 호출 결과를 볼 수 있는지 궁금했다. 공식 문서를 찾아보니, Postman에는'built-in API client'이 있다고 소개하고 있었다. 이 자체가 클라이언트 역할을 해주고 있는 것이었다.

> Postman's built-in API client enables you to create and send API requests, including HTTP, GraphQL, and gRPC requests.\
> Using Postman, you can send a request to an endpoint, retrieve data from a data source, or test an API's functionality.\
> You don't need to enter commands in a terminal or write any code.\
> When you create a new request and select Send, the API response appears right inside Postman. [공식 문서 "Send your first API request"](https://learning.postman.com/docs/getting-started/first-steps/sending-the-first-request/)

첫 문장이 중요할테니, 여기서 핵심 키워드를 뽑아내보자. `API client`, `create and send API requests`, `HTTP, GraphQL, and gRPC requests`. 이렇게 3개의 덩어리가 보인다.

Postman은 브라우저, 프론트엔드 애플리케이션을 대신해서 서버와 통신하는 클라이언트라고 생각하면 된다. 프론트엔드 코드에서는 `fetch` 메소드로 호출할 것을 Postman을 통해 실제 코드 없이 GUI를 활용해서 간단하게 요청할 수 있다. 그리고 서버의 실제 응답도 받아볼 수 있다.

서버에 요청을 보낼 때 '데이터 요청사항' 뿐 아니라, `Headers`를 설정하는 부분도 아직 생소했다. `Headers`의 Key로 추가 설정이 필요했다. Host, User-Agent, Accept, 그리고 API를 사용하는 NAVER 검색 API Client ID, Secret도 함께 기재해줘야 했다. (아래 이미지 첨부) 이 부분은 아직 모호한 영역이 많아 추가로 챙겨야겠다.

이 도구로 뭘 할 수 있을까? 언제 활용하면 좋은지 익숙해지고 싶다. 추측해보자면 프론트엔드 개발자로서 (1) 데이터를 요청할 방식과 코드를 어떻게 하면 좋을지, (2) 어떻게 데이터가 넘어올지 예상할 목적으로 사용해볼 수 있을 것 같다. 백엔드에서 API가 모두 완성된 상태에서는 쓸 일이 없을까?

오늘 정리를 통해, Postman이 어떻게 API 호출 결과를 보여줄 수 있는지 명확하지 않았는데, 공식 문서를 통해 서버에 요청을 보내는 클라이언트의 역할을 postman이 대신 해준다는 것으로 개념을 세울 수 있었다. Postman이라는 이름도 '우편배달'의 뉘앙스를 품고 있는게 맞는 것 같다.

* Postman 시도 내용 ![postman-api-response](assets/postman-api-response.png)
